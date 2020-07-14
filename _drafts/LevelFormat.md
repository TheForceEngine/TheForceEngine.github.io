---
layout: post
title: Future Level Format
---

When taking breaks from the reverse-engineering work, sometimes I work a bit on the level editor. One area of work is deciding on the editor format and how to expose advanced features to Dark Forces and Outlaws (such as slopes in new Dark Forces levels). So I have been putting together a format "spec" that I am planning on implementing for the level editor at some point before it starts being used for real work.

[TFEM Spec](TFEM_Spec.md)

### Excerpt from the draft

The Force Engine will support the Dark Forces LEV format, Outlaws LVT and LVB formats and a super-set format called TFEM ("TFE Map"). Unfortunately the Jedi Engine reads text based data files in a fairly rigid way, meaning that there is no provision for skipping default parameters or adding new unknown parameters or structure. For this reason, the original formats are not very useful for adding new features or for the level editor. This format has some similarities to the UDMF format and is my attempt to "get ahead" of the format mess and allow the same format to be used while adding new features in the future and for the format to be the master format used by tools.

As a super-set format, TFEM will support the entire feature set of the Dark Forces version of Jedi and the Outlaws version as well as any new features added for The Force Engine. It will remain a text based format, though a binary "compiled" version may also be supported later. Finally it will support default values - in which case the parameter does not have to be specified and map readers must skip unknown values or blocks without giving an error - making the format more robust and making versioning easier. The plan is to use the TFEM format as the level editor format, which can then be exported to other formats as requested. If using Outlaws features in Dark Forces or using new map features not present in vanilla, the TFEM format must be used - in other words there will be no Outlaws in Dark Forces style formats. However when using the TFEM format all of the level features of both Dark Forces and Outlaws will be accessible when using the "TFE" featureset (and any addition TFE specific features).
