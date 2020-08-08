---
layout: post
title: Fixed Point and Higher Resolutions
---

## The Problem
So for a while I was working with two different "modes" for fixed point in the Classic Renderer - the original (DOS) 16.16 and then a higher precision, but also larger 44.20 format. The larger format fixes all of the overflow issues that happen in the renderer when rendering at above 320x200 and the smaller format matches the DOS original. However, when trying to reconcile these different modes which would have to exist at the same time in order to switch dynamically - without duplicating code - things were proving to be problematic. So I took a closer look at what Outlaws and the Mac version were doing and realized that they use the same precision for most operations, the same size type and still use fixed-point. This is obvious in hindsight. So what is the difference? Mainly that certain operations were handled more carefully in those versions of the engine. This is what I suspected but what I didn't immediately realize that only a few places in the code need to change, most of the time 16.16 format is enough even at higher resolutions. The only time it is truly insufficient is when rendering textured scanlines (when rendering flats or textured models).

*Note the code shown here isn't complete but shows the relevant parts. And yes I realize the mul16() should be offseting the 64-bit result by HALF (32768 for 16.16) before the shift for proper rounding, but this follows the original code in that regard.*

So what do I mean about being more careful? To answer that, I will show some problematic code found in the DOS renderer and explain the problem.<br>
```C++
x0proj = div16(mul16(x0, focalLength), z0) + halfWidth;
```

div16() is fixed point division. It upcasts the fixed point values to 64-bits, scales the numerator by __ONE__ (65536 in 16.16 fixed point) and then divides by the denominator.
```C++
fixed16 div16(fixed16 num, fixed16 den)
{
  s64 num64 = s64(num);
  s64 den64 = s64(denom);
  return (num64 << 16) / den;
}
```

mul16() is fixed point multiplication. It upcasts the fixed point values to 64-bits, multiplies the values and then scales by 1 / __ONE__ (65536 in 16.16 fixed point).
```C++
fixed16 mul16(fixed16 x, fixed16 y)
{
  s64 x64 = s64(x);
  s64 y64 = s64(y);
  return (x * y) >> 16;
}
```

So what happens when we chain these operations - ```div16(mul16(a,b),c)```? We will look at two cases, one at 320x200 and another at 640x400 and use the same X and Z values.<br>
* We will assign ```x = intToFixed(200);``` - since __ONE__ is 65536, this means the fixed point equivalent is 13,107,200.<br>
* Let's assign ```z = intToFixed(200);``` as well, this vertex will be on the edge of the screen after projection.<br>
* If we are rendering at 320x200, ```focalLength=intToFixed(160)``` (which is 320/2 for a 90 degree field of view) and at 640x400 ```focalLength=intToFixed(320)```, which are 10,485,760 and 20,971,520 respectively.

Here is the situation when rendering at 320x200:
```C++
div16(mul16(13107200, 10485760), 13107200):
Multiply: s32(13107200 * 10485760 / 65536) = 2,097,152,000
Divide: s32(2097152000 * 65536 / 13107200) = 10,485,760
```
This is fixed point, where __ONE__ = 65536, so this represents: 160.0 - exactly what we expect for being on the right side of the screen. No problems here.

Now remember that an s32 (32-bit integer) can hold a maximum value of 2,147,483,647; you will probably notice how close we got to overflowing this value in the multiply above. Much bigger and things would start behaving weird. So let's see what happens when we bump up the resolution to 640x400:<br>
```C++
div16(mul16(13107200, 20971520), 13107200):
Multiply: s32(13107200 * 20971520 / 65536) = 4,194,304,000 -- OVERFLOW
...
```
Here the value overflows during the multiplication so when we get to the divide its already very wrong. But wait, the final answer should be 20,971,520 - so there should be plenty of precision! And indeed that is true.

## The Solution
The problem with the original code is that the multiplication and division operations should be "fused" - in other words we should do them as one operation in 64-bits before dropping back from 64-bits to 32-bits.

So we replace mul16() and div16() with a single function fusedMulDiv(a, b, c), which computes ```(a * b) / c``` as one operation. Let's see what that looks like:<br>
```C++
fixed16 fusedMulDiv(fixed16 a, fixed16 b, fixed16 c)
{
  s64 a64 = s64(a);
  s64 b64 = s64(b);
  s64 c64 = s64(c);
  
  return ((a * b) / c) >> 16;
}
```

In other words (a * b) / c is computed in 64-bits - essentially 48.16 fixed point - and only converted to 32 bits once it is done. So let's look at the results:<br>
```C++
fusedMulDiv(13107200, 20971520, 13107200):
s32(13107200 * 20971520 / 13107200) = 20,971,520 -- No more overflow!
```
And since __ONE__ = 65536, this represents 320.0 - exactly what we expect at 640x400 at the right edge of the screen.

## Reality
Of course this, while being the most prominenent issue, is not the only one. The way scanlines are handled had to be fixed up as well. And there we really do need more precision, the original DOS game used 10-bits of fractional precision during scanline drawing for the texture coordinates, which is barely enough at 320x200. At higher resolutions we really need twice that (20-bits) to avoid artifacts, though 16-bits is tolerable (and most likely the solution used on the MAC). But this is a limited area of the code and so using specialized fixed point types for scanlines only affects a small amount of code, instead of the whole renderer.

## Classic Renderer Release
So what does this mean for the release? To put it simply the renderer will detect if you are running at 320x200 or a higher resolution. If you are running at 320x200 the original code will be used as-is, flaws and all, in order to maintain the original limits. If you are running at any higher resolution or widescreen, then the code will instead use the improved, proper calculations as described here - just like the MAC port of Dark Forces and Outlaws - resulting in cleaner visuals, higher limits and a renderer that works well at higher resolutions.
