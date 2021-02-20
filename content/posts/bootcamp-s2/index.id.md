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

{% capture images %}
	https://p.ihateani.me/nhwysqem.png
{% endcapture %}
{% include gallery images=images caption="Extension 05" cols=1 %}

#### 6. Polacode {#vscode-ext-polacode}

Membuat screenshot code yang dibuat. (Dokumentasi)

Link Instalasi: [pnp.polacode](https://marketplace.visualstudio.com/items?itemName=pnp.polacode)

{% capture images %}
	https://p.ihateani.me/bykdqhqx.png
{% endcapture %}
{% include gallery images=images caption="Extension 06" cols=1 %}

#### 7. GitLens — Git supercharged {#vscode-ext-gitlens}

Extension terbaik untuk Integrasi Git(Hub/Lab).

Link Instalasi: [eamodio.gitlens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

{% capture images %}
	https://p.ihateani.me/pasjvpfa.png
{% endcapture %}
{% include gallery images=images caption="Extension 07" cols=1 %}

#### 8. vscode-icons {#vscode-ext-vsicons}

Menambahkan Icon untuk extension File dengan tema yang ada.

Link Instalasi: [vscode-icons-team.vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)

{% capture images %}
	https://p.ihateani.me/uuynlpsb.png
{% endcapture %}
{% include gallery images=images caption="Extension 08" cols=1 %}