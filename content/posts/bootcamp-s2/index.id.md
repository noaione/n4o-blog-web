---
weight: 3
title: "Algorithm Bootcamp Season 2 - Electric Boogaloo"
date: 2020-09-09T11:43:00+07:00
description: "Langkah preparasi Algorithm Bootcamp Season 2"
subtitle: "Langkah preparasi Algorithm Bootcamp Season 2"

tags: ["tutorial", "coding"]
categories: ["Tutorial", "Coding"]

lightgallery: true
enableVideoJS: true
---

<div align="center">
<i>Ditulis karena bosan, dan biar gak ribet bantu-bantunya nanti</i>
</div>

<!--more-->
<br>
{{< admonition type=warning title="Bagi pengguna OS lain" open=true >}}
Tutorial ini dibuat khusus untuk pengguna **Windows 10**<br>
Jika pengguna OS lain, ada beberapa langkah yang dilewati.
{{< /admonition >}}

## Setup WSL {#wsl}
Ikuti tutorial ini: [Microsoft Docs - WSL Install](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

{{< admonition type=warning title="Versi Distro" open=true >}}
Disarankan memilih **Ubuntu 20.04 LTS**<br>
Bisa di klik link ini: [Microsoft Store](https://www.microsoft.com/store/apps/9n6svws3rx71)<br>
Silakan Ikuti **Step 1 dan** langsung lompat ke **Step 6-7.**<br>
Jika situ menggunakan Windows 10 2004, bisa ikuti Step 2-5 kalau mau tapi tidak tak rekomendasikan untuk sekarang.
{{< /admonition >}}

{{< admonition type=info title="Jika tidak bisa install via MS Store" open=true >}}
Ikuti cara install melalui LxRunOffline di sini: [WSL dengan LxRunOffline](/posts/lxrunoffline)
{{< /admonition >}}

Jika sudah muncul kurang lebih seperti ini, WSL siap dipakai
{{< image src="/assets/img/bootcamps2/wsl_ready.png" caption="WSL Ready">}}

{{< admonition type=danger title="Jika User adalah Root" open=true >}}
**NOTE:**<br>
Pastikan WSL/Ubuntu tidak jalan sebagai `root`, jika WSL/Ubuntu jalan sebagai `root` tolong Uninstall Ubuntu lalu Install kembali.<br>
**Contoh jalan sebagai root adalah tanda: `root@HOSTNAME:~$` di Terminal/Console/CMD**
{{< /admonition >}}

## Toolchain GCC/G++ + Git {#toolchain}
Jalankan command berikut:<br>
```bash
sudo apt update && sudo apt install build-essential git
```

Masukan password user jika diminta.<br>
Jika sudah terinstall, bisa dicoba dengan:
```bash
git --version
gcc --version
```
<br>
{{< image src="/assets/img/bootcamps2/wsl_gccgit_test.png" caption="GCC/Git Test Command">}}

## Homebrew on Linux {#linuxbrew}
Langkah pertama adalah menginstall Homebrew terlebih dahulu dengan command berikut
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
<br>
{{< image src="/assets/img/bootcamps2/brew_start.png" caption="Install Homebrew">}}

{{< admonition type=info title="Waktu Instalasi" open=true >}}
Akan memakan waktu cukup lama, sekitar 30 menit lebih.<br>
Dikarenakan harus mengunduh 300mb+ dari Git.
{{< /admonition >}}

---

Jika sudah, silakan jalankan commmand berikut
```bash
test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >> ~/.bash_profile
echo "eval \$($(brew --prefix)/bin/brew shellenv)" >> ~/.profile
source ~/.profile
source ~/.bash_profile
```

Jika `source ~/.bash_profile` error, abaikan saja.

Lalu tes dengan menjalankan command berikut
```bash
brew install hello
```
<br>
{{< image src="/assets/img/bootcamps2/brew_hello.png" caption="Tes Homebrew">}}
<br>

**Video version:**
<br>
{{< videojs url="https://p.ihateani.me/cerxeavc.mp4" >}}

## VSCode ❤️ WSL {#vscode-wsl}

Saatnya integrasi VSCode dengan WSL! Silakan install [VSCode](https://code.visualstudio.com/) jika belum.

Buka VSCode dan klik Extension di bagian kiri. (`CTRL+SHIFT+X`)

Lalu cari `Remote - WSL` dan klik Install.

{{< image src="https://p.ihateani.me/cdsquggy.png" caption="Remote - WSL">}}

Restart VSCode dan sekarang harusnya ada `Remote Explorer` dibagian Kiri.<br>
Ubah `Containers` ke `WSL Targets` jika belum, lalu klik kanan salah satu distro WSL
dan klik `Connect to WSL`

Seharusnya akan muncul Window baru dan dipojok kiri bawah terdapat tulisan `WSL: NamaDistro`

{{< image src="https://p.ihateani.me/pbjxgnzu.gif" caption="Remote - WSL (GIF)">}}

VSCode telah sukses terkoneksi dengan WSL. 🎉

### VSCode ❤️ WSL - Extensions {#vscode-extensions}

VSCode jika berpindah Remote akan menggunakan Extensions yang sudah terinstall masing-masing.<br>
Beberapa extension bersifat global, beberapa tidak.

Berikut adalah Extensions yang disarankan.

{{< admonition type=warning title="Note" open=true >}}
Mohon install ketika VSCode sudah terhubung dengan WSL.
{{< /admonition >}}

#### 1. Code Runner {#vscode-ext-crun}

Berguna untuk menjalankan code lebih simpel.

Link instalasi: [formulahendry.code-runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner)

Lalu buka Settings untuk mengubah salah satu settings untuk `Code Runner`<br>
Gunanya agar bisa memberikan input ketika run code. (REPL support)<br>
Settings terletak di: `File -> Preferences -> Settings`

Pilih `Remote [WSL: NamaDistro]` lalu ketik `code-runner.runInTerminal` di kolom pencarian, setelah itu centang `Code-runner: Run In Terminal`

Sekarang tinggal klik tombol `▶️` di pojok kanan atas atau shortcutnya `CTRL+ALT+N`

{{< admonition type=warning title="Jika gagal" open=true >}}
Pastikan sudah terinstall G++/GCC Toolchain dan sudah terconnect dengan WSL.<br>
Jika masih tidak bisa, bisa menjalankan codenya secara manual dengan cara<br>
```bash
g++ ./namaFile.cpp -o ./namaFile && ./namaFile
```
{{< /admonition >}}

{{< image src="https://p.ihateani.me/kpjhhkkm.gif" caption="Code Runner in Terminal Options">}}

#### 2. C/C++ {#vscode-ext-ccpp}

Sebagai helper utama C/C++

Link Instalasi: [ms-vscode.cpptools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

{{< image src="https://p.ihateani.me/xmhvdbyu.png" caption="Extension 02">}}

#### 3. Visual Studio IntelliCode {#vscode-ext-vscintellicode}

Sebagai code completion untuk berbagai macam bahasa.

Link Instalasi: [VisualStudioExptTeam.vscodeintellicode](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode)

{{< image src="https://p.ihateani.me/kqolciuc.png" caption="Extension 03">}}

#### 4. Prettier - Code formatter {#vscode-ext-prettier}

Sebagai code formatter biar lebih rapih.

Link Instalasi: [esbenp.prettier-vscode](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

{{< image src="https://p.ihateani.me/mlashzri.png" caption="Extension 04">}}

#### 5. Bracket Pair Colorizer {#vscode-ext-brackerpair}

Mempermudah membedakan code didalam bracket.

Link Instalasi: [CoenraadS.bracket-pair-colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer)

{{< image src="https://p.ihateani.me/nhwysqem.png" caption="Extension 05">}}

#### 6. Polacode {#vscode-ext-polacode}

Membuat screenshot code yang dibuat. (Dokumentasi)

Link Instalasi: [pnp.polacode](https://marketplace.visualstudio.com/items?itemName=pnp.polacode)

{{< image src="https://p.ihateani.me/bykdqhqx.png" caption="Extension 06">}}

#### 7. GitLens — Git supercharged {#vscode-ext-gitlens}

Extension terbaik untuk Integrasi Git(Hub/Lab).

Link Instalasi: [eamodio.gitlens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

{{< image src="https://p.ihateani.me/pasjvpfa.png" caption="Extension 07">}}

#### 8. vscode-icons {#vscode-ext-vsicons}

Menambahkan Icon untuk extension File dengan tema yang ada.

Link Instalasi: [vscode-icons-team.vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)

{{< image src="https://p.ihateani.me/uuynlpsb.png" caption="Extension 08">}}

## Run code di WSL+VSCode {#vscode-coderun}

Pastikan [VSCode telah terhubung dengan WSL](#vscode-wsl)<br>
Dan pastikan telah menginstall [extension Code Runner](#vscode-ext-crun).

Biar mempermudah, bisa membuat folder baru di bagian direktori Home WSL `(~/)`.

Cara membuat folder baru adalah:
```bash
mkdir namaFolder
```
Jalankan code tersebut di WSL.

{{< image src="https://p.ihateani.me/mtqorces.gif" caption="Membuat folder baru">}}

Di VSCode, connect ke WSL dan pilih `Open Folder`, lalu silakan buat file baru di folder tersebut. (misalkan `helloworld.cpp`)

```cpp
#include <stdio.h>

int main() {
	puts("Hello world!");
	return 0;
}
```

Save filenya, dan klik tombol Play di pojok kanan atas (Akan ada jika sudah menginstall [extension Code Runner](#vscode-ext-crun)).<br>
Jika codenya sukses di run, selamat WSL dan VSCode sudah benar-benar siap dipakai!

{{< admonition type=info title="Note" open=true >}}
Disarankan menaruh code yang ingin di run di folder WSL.<br>
Dikarenkan WSL tidak support `cd` (change directory) ke folder windows.
{{< /admonition >}}

{{< image src="https://p.ihateani.me/qpkhfswk.gif" caption="Run Code @ WSL">}}

## Git Integrations {#vscode-git}

*Git is hard...*

### Preparasi {#vscode-git-preface}

Mari buat akun baru di GitHub jika belum: [Sign Up](https://github.com/join).

Jika sudah, mari buat Repository baru di GitHub!

Buka halaman utama [GitHub](https://github.com) dan klik tanda `+` di pojok kanan atas, lalu klik `New Repository`<br>
Isi `Repository Name` bebas mau kayak gimana, isi `Description` jika mau.<br>
Disarankan memilih `Public` untuk visibility.

Setelah itu klik `Create repository`, repo baru telah siap!

**Video tutorial:**<br>
{{< videojs url="https://p.ihateani.me/uzomrkrx.mp4" >}}

#### Konfigurasi Git {#git-config}

Sebelum memulai project, buka WSL terlebih dahulu.<br>
Kita harus atur config untuk email dan user, caranya:
```bash
git config --global user.name "USERNAME GITHUB"
git config --global user.email "email@provider.tld"
```
Jalankan kedua command tersebut di WSL.

{{< admonition type=info title="Note" open=true >}}
Gunakan username github dan email yang dipake di github.
{{< /admonition >}}

{{< image src="https://p.ihateani.me/asqjkyxf.gif" caption="Config git">}}

Saatnya memulai project!, jika sudah ada folder bisa langsung ke [Sudah ada Folder](#vscode-git-fd-exists)<br>
Jika belum silakan ke [Tidak ada Folder](#vscode-git-clone)

{{< admonition type=warning title="Saran!" open=true >}}
**Disarankan jangan membuat folder terlebih dahulu untuk mempermudah**
{{< /admonition >}}

### Git Integrations - Remote Add {#vscode-git-fd-exists}

Jika folder yang dibuat ada di Windows, silakan ke [Tidak ada Folder](#vscode-git-clone).<br>
Folder harus berada di direktori WSL. (ex: `/home/USERNAME/bootcamp-s2/`)

Pertama, connect ke WSL terlebih dahulu.<br>
Lalu, pilih `Open Folder` dan buka folder yang dipakai (ex: `/home/USERNAME/bootcamp-s2/`)

Pilih `Source Control` di sidebar kiri atau pencet `CTRL+SHIFT+G`.<br>
Klik `Initialize Repository`<br>
Klik `…` -> `Remote` -> `Add Remote`.

Di sini bisa kita provide clone URL HTTPS atau `Add remote from GitHub`, disarankan pilih `Add remote from GitHub`.

Jika belum pernah terhubung dengan GitHub akan muncul pop-up message, klik `Allow`.

VSCode lalu akan berusaha menghubungkan VSCode dengan GitHub, silakan ikuti petunjuk di browser (Continue -> Authorize github -> Masukan password -> Open in Visual Studio Code)<br>
Di VSCode lalu klik `Open` untuk menyelesaikan proses OAuth. Silakan tunggu sebentar selagi repository sedang di load.

Lalu pilih repository yang sudah dibuat sebelumnya, masukan `origin` sebagai `Remote Name`.

GitHub telah sukses terhubung dengan project VSCode.

**Note** Jika repo tersebut sudah ada Isinya, silakan ikuti langkah [Remote Add (Checkout)](#vscode-git-fd-checkout)

**Instruksi dalam bentuk Video**:
{{< videojs url="https://p.ihateani.me/wdlxsjjq.mp4" >}}

#### Git Integrations - Remote Add (Checkout) {#vscode-git-fd-checkout}

Jika Repository yang ditambah ada isinya, silakan ikuti langka ini, jika tidak bisa loncat ke [Git - Commit/Push/Pull](#git-hell)

Setelah menambahkan remote di langkah atas, buka `Source Control`<br>
Klik `…` -> `Pull, Push` -> `Fetch`.

VSCode akan mengambil seluruh informasi dari GitHub dan menyimpannya di local disk kita.

Selanjutnya klik `…` -> `Checkout to`.

Akan muncul beberapa pilihan, silakan pilih `origin/master`.<br>
Folder akan terisi dengan file yang ada di GitHub.

**Instruksi dalam bentuk Video**:
{{< videojs url="https://p.ihateani.me/qitwmtob.mp4" >}}

### Git Integrations - Remote Clone {#vscode-git-clone}

Pertama, connect ke WSL terlebih dahulu.<br>
Lalu, pilih `Clone Repository`.

Copy link clone repository, format URL repository git adalah:
```
https://github.com/USERNAME/REPONAME.git
```

Contohnya: `https://github.com/noaione/code-bootcamp-s2.git`

{{< admonition type=info title="Note" open=true >}}
Jika repository itu bersifat Private, tambahkan Username dan Password akun ke URL repository.<br>
Formatnya jadi: `https://USERNAME:PASSWORD@github.com/USERNAME/REPONAME.git`
{{< /admonition >}}

Jika repo tidak ada apa-apa dan ada teks `Quick setup`, copy link yang disediakan.<br>
Jika repo sudah ada isi klik tombol `Clone or Download` yang berwarna hijau dan klik tombol copy di kolom `Clone with HTTPS`.

Kembali ke VSCode, masukan url tersebut dan enter.<br>
Pilih kemana folder akan di clone (saran: `/home/USERNAME`) lalu klik `OK`.

Silakan tunggu, dan jika ada notifikasi `Would you like to open cloned repository?`<br>
klik `Open`.

GitHub telah sukses terhubung dengan project VSCode.

**Instruksi dalam bentuk Video**:
{{< videojs url="https://p.ihateani.me/zxoleuzs.mp4" >}}

## Git - Commit/Push/Pull {#git-hell}

Dibagian ini, kita akan sedikit belajar tentang Commit, Push, dan Pull serta mengatasi File Conflict.

Sebelum kita mulai commit-commit ke repo, disarankan kita setup file `.gitignore`, file ini berguna agar tidak ada "sampah" yang ikutan ke commit/push ke remote repository.

### .gitignore File {#git-ignore}

Silakan buka website ini: [gitignore.io](https://www.toptal.com/developers/gitignore)

Di kolom pencarian, ketik `C` lalu `C++` lalu `Code`.<br>
Ketiga itu akan generate file .gitignore untuk bahasa C, C++ serta IDE VSCode.

Lalu klik Create.

Copy hasilnya, lalu buat file `.gitignore` dan paste lalu save.

**Instruksi dalam bentuk Video**:
{{< videojs url="https://p.ihateani.me/jwecruts.mp4" >}}

### Commit Changes {#git-commit}

Sebelum kita bisa menambah file baru maupun modifikasi ke Repo Github kita, kita harus melakukan: stage changes, commit lalu push.

Dibagian ini, akan dijelaskan gimana cara Stage Changes dan Commit.

Pertama klik `Source Control` lalu pilih file yang ingin di Stage dengan klik tanda `+` di samping nama file. Atau jika ingin semuanya, bisa klik Tanda `+` di sebelah teks `Changes`.

Lalu klik `✓` di bagian Source Control, isi "Message"-nya, disarankan messagenya sesuai dengan apa yang diubah biar mudah diingat.

Setelah itu cukup Enter, dan Perubahanmu telah di commit dan siap untuk di Push.

{{< image src="https://p.ihateani.me/zpzcdvck.gif" caption="Commit changes">}}

### Push Changes {#git-push}

Jika sudah membuat commit baru, kita tinggal melakukan yang namanya Push, yaitu "mendorong" perubahan menuju remote repository.

Pertama klik `Source Control` lalu klik `...` di sebelah teks `Source Control`, dan klik Push.

Sudah, hanya seperti itu, perubahan telah masuk ke GitHub.

{{< image src="https://p.ihateani.me/tbgmtidf.gif" caption="Push Changes">}}

### Pull Changes {#git-pull}

Ternyata projek kita lakukan dikerjakan bersama kolaborator lain?!, dan ketika kita ingin Push Changes kita, ada error message.

{{< image src="https://p.ihateani.me/mexnhtvp.png" caption="Push Error">}}

Cara membenarkannya lumayan simpel, cukup Pull Changes saja atau menarik perubahan dari Remote Repo ke Local Repo.

Pertama klik `Source Control` lalu klik `...` di sebelah teks `Source Control`, dan klik Pull.

Semua perubahan dari Remote repo akan masuk ke Local repo, dan situ bisa lanjut Push Changes situ.

{{< image src="https://p.ihateani.me/xrvsisul.gif" caption="Pull Changes">}}

### Merge Conflicting Changes {#git-conflict-hell}

Ternyata, pas situ Pull Changes kolaborator rlain dan situ mengubah line yang sama dan muncul error ketika Pull Changes.

Sabar dulu, cara benerinnya agak sulit karena kita harus memilih mana yang ingin kita simpan dan yang tidak.

Jika muncul error `Please clean your changes` atau semacamnya.<br>
Silakan commit semua perubahan terlebih dahulu baru Pull Changes.

{{< image src="https://p.ihateani.me/cluzjbfo.gif" caption="Pull Error #1">}}

Setelah Pull Changes, ternyata ada Merge Conflict.

{{< image src="https://p.ihateani.me/cntmfean.png" caption="Pull Merge Conflicts">}}

Git sendiri bisa mengabungkan perubahan otomatis, tapi jika tidak bisa, maka git akan menandakannya dengan

```diff
<<<<<<< HEAD
	perubahan dari kita
=======
	perubahan dari remote/pull
>>>>>>> commit ID
```

Di VSCode, situ akan mendapatkan highlighting otomatis, dengan 2 warna. `Hijau` untuk Commit kita, `Biru` untuk Commit dari Repo.

Dan kita akan mendapatkan beberapa tombol, yaitu:
- Accept Current Change<br>
	Gunakan perubahan kita.
- Accept Incoming Change<br>
	Gunakan perubahaan dari Pull Changes
- Accept Both Changes<br>
	Gunakan kedua perubahan (Perubahan kita diatas, perubahan dari Remote dibawahnya)
- Compare Changes<br>
	Membuka window baru untuk membandingkan perubahan.

Situ bebas mau memilih yang mana, silakan diskusikan sendiri, jika sudah silakan Commit perubahan tersebut dan silakan Push jika mau.

**Contoh dalam bentuk Video**:
{{< videojs url="https://p.ihateani.me/vdnbjhsp.mp4" >}}

Jika kita menggunakan contoh ini:
```diff
<<<<<<< HEAD
	perubahan dari kita
=======
	perubahan dari remote/pull
>>>>>>> commit ID
```

Jika kita klik `Accept Current Change` maka akan menjadi
```
	perubahan dari kita
```

Jika kita klik `Accept Incoming Change` maka akan menjadi
```
	perubahan dari remote/pull
```

Jika kita klik `Accept Both Changes` maka akan menjadi
```
	perubahan dari kita
	perubahan dari remote/pull
```

## Penutup {#godhelpmeimtiredwritingthisanduploadingittomycdn}
Close halaman ini dan kembalilah ngoding.<br>
Jika ada masalah (atau kurang ngerti) bisa kontak/mention **N4O#8868** di Discord.

**Hal yang mungkin berguna**:<br>
**Belajar git lebih lanjut**: [Git for dummies](https://medium.com/@yoyomade/github-for-dummies-96f753f96a59) [link provided by `code wizard`]<br>
**Akses folder WSL**: Ketik `\\wsl$` di File Explorer.<br>
**Pemandangan alam**: [Klik](https://duckduckgo.com/?q=pemandangan+alam&t=h_&iax=images&ia=images) biar segar dikit matanya ~~(karena gk akan bertemu dunia luar untuk waktu yang lama)~~

**Referensi**:
1. `#announcement` channel di Server
2. [brew.sh](http://brew.sh/)
3. Pengalaman pribadi.
