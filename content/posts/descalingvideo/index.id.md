---
weight: 3
title: "Encoding: Descaling"
date: 2019-01-20T14:56:00+07:00
lastmod: 2021-01-19T13:41:00+07:00
description: "Resizing ❌ | Descaling ✔️"
subtitle: "Resizing ❌ | Descaling ✔️"

tags: ["fansub", "encoding", "tutorial"]
categories: ["Fansubbing", "Encoding", "Tutorial"]

lightgallery: true
---

*insert generic intro here*

<!--more-->

Yang dibutuhin:
- Mata
- PC & Monitor
- Vapoursynth dan segalanyas
- x264

Silakan cek tutorial install ini: [https://gist.github.com/noaione/6f8583c32a8f23e367688ebac0c9d0e0](https://gist.github.com/noaione/6f8583c32a8f23e367688ebac0c9d0e0)

## Intro

Resizing Anime sama Descaling Anime menghasilkan hal yang berbeda, Descaling menggunakan algoritma lain agar
Anime dapat dikembalikan ke resolusi asli (Native Resolution).

Ada beberapa macam kernel yang dipakai sama Web streaming, atau studio animasinya.

Kernel yang sering dipakai biasanya Bicubic (1/3 1/3) untuk upscale Anime dari resolusi asli.

Untuk permulaan, buatlah file baru dan tambah kode seperti ini (Ekstensi file: `.vpy`)
```py
import vapoursynth as vs
from vapoursynth import core

import fvsfunc as fvf
import descale
import MaskDetail as maskD
```

{{< image src="/blog/assets/img/descale1.png" caption="Import script ke file manaria01descale.vpy">}}

Selanjutnya import video yang ada dan buat outputnya dan coba klik `F5`

```py
import vapoursynth as vs
from vapoursynth import core

import fvsfunc as fvf
import descale
import MaskDetail as maskD

src = core.ffms2.Source('Manaria Friends - 01v2 (AbemaTV 1080p).mkv')
src = fvf.Depth(src, 16)

src.set_output()
```

{{< image src="/blog/assets/img/descale2.png" caption="Import video (src) + dithering ke 16bit">}}
{{< image src="/blog/assets/img/descale3.png" caption="Output dari frameserver (F5)">}}

Itu basic dari importing video dan sebagainya, sekarang kita mulai mencoba descaling.

## Descaling: For real

Video yang tak gunakan merupakan Manaria Friends, resolusi aslinya jika nggak salah itu 810p, jadi sekarang kita coba descale ke 810p.

```py
import vapoursynth as vs
from vapoursynth import core

import fvsfunc as fvf
import descale
import MaskDetail as maskD

src = core.ffms2.Source('Manaria Friends - 01v2 (AbemaTV 1080p).mkv')
src = fvf.Depth(src, 16)

v = descale.Debicubic(src, width=1440, height=810, b=1/3, c=1/3, yuv444=True)

v.set_output()
```

{{< image src="/blog/assets/img/manaria01-1080p.png" caption="Source 1080p">}}
{{< image src="/blog/assets/img/manaria01-810p.png" caption="Descaled 810p">}}

Silakan gambarnya di buka di Tab baru agar lebih enak.

Selesai sudah, cukup segitu aja kalo emang cuma mau descaling video, gak ribet gak lama karena dah ada orang yang buat script descaling gini biar mempermudah orang lain.

Tapi kadang descaling gak bekerja dengan baik karena studio animasi suka nempel 1080p overlay (teks credit, dsb.) ke resolusi aslinya, jadi semua overlay 1080p pasti ancur.

{{< image src="/blog/assets/img/manaria01-810pbroken.png" caption="Zoom in ke teks jepang, bisa diliat ada artifact halo/ringing">}}

Ada satu cara menghilangkannya, yaitu pake **MaskDetail**.

**MaskDetail** akan ngebuat mask pada teks credit dan sebagainya agar teks credit itu bisa menggunakan resizer biasa dibanding descaler agar tidak ada artifact

```py
import vapoursynth as vs
from vapoursynth import core

import fvsfunc as fvf
import descale
import MaskDetail as maskD

src = core.ffms2.Source('Manaria Friends - 01v2 (AbemaTV 1080p).mkv')
src = fvf.Depth(src, 16)

v = descale.Debicubic(src, width=1440, height=810, b=1/3, c=1/3, yuv444=True) # Descaler
mask = maskD.maskDetail(src, 1440, 810, kernel='bicubic')
resizer = core.resize.Bicubic(src, width=1440, height=810, format=vs.YUV444P16) # Resizer, silakan ganti YUV444P16 menjadi YUV420P16 jika `yuv444=False`

mask.set_output()
```

{{< image src="/blog/assets/img/manaria01-810pmask.png" caption="Hasil mask">}}