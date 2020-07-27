# WAX Format
The Wax format can hold multi-view, animated sprites meant to be displayed in the 3D world of Dark Forces. It is a "load in place" format, meaning that the format is loaded directly from disk, offsets are converted to pointers and rendering parameters are filled out in place. This adds extra challenges for 64-bit programs or alternate fixed point storage sizes, so TFE converts from WAX to a similar, 64-bit friendly format internally. Being "load in place" also means that some parameters should be zero in the data but is filled out at runtime.

## Nomenclature
s32 = signed 32 bit (4 byte) integer.<br>
u32 = unsigned 32 bit (4 byte) integer.<br>
0x?? = offset in the structure in hexadecimal: 0x00 = 0, 0x10 = 16, 0x20 = 32, ...

## Header
```C++
u32 version     // 0x00: Wax version, should be 0x00100100 for Dark Forces.
u32 animCount   // 0x04: Number of animations
u32 frameCount  // 0x08: Total number of frames?
u32 cellCount   // 0x0C: Number of unique "cells" - which are the images actually displayed.
s32 xScale      // 0x10: 0 in the source data, runtime is Sprite World Scale / anim[0].worldWidth
s32 yScale      // 0x14: 0 in the source data, runtime is Sprite World Scale / anim[0].worldHeight
s32 xtraLight   // 0x18:
s32 pad         // 0x1C: 0 in source data, runtime ?
u32 anim[32]    // 0x20: Offset to each animation from the start of the Wax, in bytes. The list is NULL terminated.
```

## Animation
```C++
s32 widthScale    // 0x00: Sprite width scale, 1.0 = 10 sprite texels / DFU. The value is stored as 16.16 fixed point (65536 = 1.0).
s32 heightScale   // 0x04: Sprite height scale, 1.0 = 10 sprite texels / DFU.
s32 frameRate     // 0x08: Playback speed of the animation in frames per second.
s32 frameCount    // 0x0C: 0 in the source data, runtime is frameCount
s32 pad1          // 0x0C: 0 in the source data, runtime ? 
s32 pad2          // 0x10: 0 in the source data, runtime ?
s32 pad3          // 0x14: 0 in the source data, runtime ?
u32 views[32]     // 0x18: Offset to each view from the start of the Wax, in bytes.
```

## View
```C++
s32 pad1        // 0x00: 0 in the source data, runtime ? 
s32 pad2        // 0x04: 0 in the source data, runtime ? 
s32 pad3        // 0x08: 0 in the source data, runtime ? 
s32 pad4        // 0x0C: 0 in the source data, runtime ? 
u32 frames[32]  // 0x10: Offset to each frame from the start of the Wax, in bytes. The list is NULL terminated.
```

## Frame
```C++
s32 offsetX   // 0x00: Display x offset of the frame from the center, scaled by widthScale at runtime to determine a final offset in DFU.
s32 offsetY   // 0x04: Display y offset of the frame from the center, scaled by heightScale at runtime to determine a final offset in DFU.
s32 flip      // 0x08: Flip frame horizontally (1).
u32 cell      // 0x0C: Offset to the cell from the start of the Wax, in bytes.
s32 widthWS   // 0x10: 0 in the source data, runtime is the final frame width in world space.
s32 heightWS  // 0x14: 0 in the source data, runtime is the final frame height in world space.
s32 pad1      // 0x18: 0 in the source data, runtime ?
s32 pad2      // 0x1C: 0 in the source data, runtime ?
```

## Cell
```C++
s32 width         // 0x00: cell width in pixels.
s32 height        // 0x04: cell height in pixels.
s32 compressed    // 0x08: 0 = raw pixels, 1 = rle compressed.
u32 dataSize      // 0x0C: size of the image data in bytes.
u32 columnOffset[]// 0x10: 0 in source data, runtime holds the offset to each pixel column of the cell from the start of the image data.
s32 pad           // 0x14: 0 in source data, runtime ?
                  // 0x18: image data.
```

## Compression
Cell image data in most WAXs is compressed using an RLE variant optimized for runs of transparent pixels. In Dark Forces (DOS), the Wax data is stored compressed in memory. While rendering, columns are decompressed on the fly as needed into a temporary buffer. So a column offset table is needed to map between a given X (column) value and the start of the compressed data for that column. For a WAX that is not compressed, the column offsets are still filled out, but they are simply imageData[x * height]. Note also that on disk the column offset table is stored before the image data at sizeof(Cell) but for uncompressed WAXs the image data starts immediately.

The following are the two possibilities, where 0x18 = sizeof(Cell).
### Compressed = 0
0x00: Cell Data<br>
0x18: Image Data
### Compressed = 1
0x00: Cell Data<br>
0x18: Column Offsets (u32 x height = 4 * height bytes)<br>
0x18 + 4 * height: Compressed Image Data.<br>

The basic algorithm is as follows:
### Givens
```C++
cellImageOffset = sizeof(Cell)                  // image data offset
compressedData = (u8*)(cell + cellImageOffset)  // the actual image data RLE compressed.
columnPixels[height]                            // output column colors, where 0 = transparent, > 0 = palette index.
```
### Decompression Pseudo-code
```C++
index = cell->columnOffset[x]
for (y = 0, index = 0; y < height;)
{
  data = compressedData[index]
  index++;
  
  if (data & 128)	// If the most significant bit of the data is set, this is a transparent run of 'data - 128' pixels.
  {
	  transPixelCount = data - 128;
	  for (i = 0; i < transPixelCount; i++, y++)
	  {
		  columnPixels[y] = 0;
	  }
  }
  else  // Otherwise this is just a run of raw pixel data, the length of the run is 'data' pixels.
  {
	  pixelCount = data;
	  for (i = 0; i < pixelCount; i++, y++, index++)
	  {
		  columnPixels[y] = compressedData[index];
	  }
  }
}
```
