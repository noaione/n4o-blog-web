---
weight: 3
title: "Ripping: OCR Hardsubbed Video"
date: 2019-02-08T16:52:00+07:00
lastmod: 2021-01-19T13:41:00+07:00
description: "Mencuri takarir anda sejak abad ke-20"
subtitle: "Mencuri takarir anda sejak abad ke-20"
featuredImage: "/assets/img/ocrhard/thumb.jpg"
images: ["/assets/img/ocrhard/thumb.jpg"]

tags: ["fansub", "ripping", "tutorial"]
categories: ["Fansubbing", "Ripping", "Tutorial"]

lightgallery: true
---

Stealing your subtitle since 20th century

<!--more-->

Yang dibutuhin:
- PC
- Vapoursynth
- FFMpeg
- YoloCR

Silakan ikuti instalasi Vapoursynth terlebih dahulu:
{{< gist noaione 6f8583c32a8f23e367688ebac0c9d0e0 >}}

## Install YoloCR

**Langkah dengan gambar: [Imgur](https://imgur.com/a/oBFP5Mg)**

1. Download YoloCR dari sini: [https://bitbucket.org/YuriZero/yolocr/downloads/](https://bitbucket.org/YuriZero/yolocr/downloads/)
2. Extract ke suatu folder
3. Install Cygwin: [https://cygwin.com/setup-x86_64.exe](https://cygwin.com/setup-x86_64.exe)
4. Ketika install, pilih hal berikut:
    - bc
    - gnupg
    - links
    - make
    - perl
    - wget
    - tesseract-ocr (pilih versi 4.0+)
    - tesseract-ocr-eng (pilih versi 4.0+)
5. Buka Cygwin
6. Install `GNU Parallel` dari Terminal Cygwin:
    * `wget -O - pi.dk/3 | bash`
    * `if [ -f ~/bin/parallel ]; then mv ~/bin/parallel /usr/local/bin/; fi`
7. Tambahkan tessdata indonesia
    - Download: [ind.traineddata](https://github.com/tesseract-ocr/tessdata_best/blob/master/ind.traineddata)
    - Copy ke: `\cygwin64\usr\share\tessdata`

## Menggunakan
Download salah satu file hardsub manapun dan taruh satu folder dengan YoloCR

Buka `YoloResize.vpy` dan modifikasi `FichierSource=r'Vidéo_Source.mkv'` ke video situ. (Yang tak pake `oploverz BnHA movie 720.mkv`)

Karena yang tak pake 720p ubah `DimensionCropBox=[1344,150]` sesuai resolusinya.

`DimensionCropBox=[width,height]` jadi maksimal width adalah `1280` yang tak tulis adalah `[1100,150]`

{{< image src="/assets/img/ocrhard/01.png" caption="Atur cropping">}}

Terlihat tidak pas sama sekali, jadi sekarang kita mainkan `HauteurCropBox=46`.

Agar terlihat mendingan, ini tak ubah ke `HauteurCropBox=10`

{{< image src="/assets/img/ocrhard/02.png" caption="Atur cropping (2)">}}

Sudah pas sekarang?, tutup file lalu buka `YoloCR.vpy`

Copy-Paste `FichierSource=r'Vidéo_Source.mkv'`, `DimensionCropBox=[1344,150]`, dan `HauteurCropBox=46` dari file `YoloResize.vpy`

Klik F5 lalu atur `SeuilI=230` dan `SeuilO=80` agar teks sub terlihat enak.

Yang tak pake adalah `SeuilI=225` dan `SeuilO=70`.

Setelah itu kasih `#` di sebelum `FichierSource=r'Vidéo_Source.mkv` jadi kayak gini: `#FichierSource=r'Vidéo_Source.mkv`, save & exit `YoloCR.vpy`.

---

Setelah itu, buka Cygwin dan ubah directory ke directory YoloCR. Cygwin menggunakan prefix `/cygdrive/` untuk harddisk kita, jika situ save di `C:` maka ketik `cd /cygdrive/c/` kalo `D:` ketik `cd /cygdrive/d/` dst.

Karena folder saya ada di `D:\VideoStuff\OCRTest\YoloCR` maka kita akan tulis `cd /cygdrive/d/VideoStuff/OCRTest/YoloCR`

Jika file yang mau diubah berakhiran selain .mp4, ubah dengan ffmpeg: `ffmpeg -i input.ext -c copy output.mp4`  

Setelah itu ketik `for file in *.mp4; do filef="${file%.*}_filtered.mp4"; vspipe -y --arg FichierSource="$file" YoloCR.vpy - | ffmpeg -i - -c:v mpeg4 -qscale:v 3 -y "$filef"; ./YoloCR.sh "$filef"; done` dan tunggu sebentar

{{< image src="/assets/img/ocrhard/05.png" caption="Proses OCR">}}

Jika sudah, selamat! sekarang waktunya buat versi yang ada di posisi atas.

Caranya sama aja, tinggal buka `YoloCR.vpy` lalu ubah `HauteurCropBox=10` menjadi lebih tinggi misal `HauteurCropBox=570`

Sebelum mulai ngetik command untuk OCR di Cygwin, ubah nama file sebelumnya agar tidak di overwrite, misal jadi `bnha.an2.srt`

Gabungin kedua file bisa pake Aegisub

*Selamat mencoba*