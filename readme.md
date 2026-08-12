# VS Code Zed-Like Minimal Setup

> Konfigurasi VS Code minimalis terinspirasi Zed Editor — clean UI, smooth scroll, terminal split-view, dan Discord Rich Presence tanpa status bar berisik.

![VS Code Zed Theme](https://img.shields.io/badge/Theme-ZED%20One%20Dark-1a1b26?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Windows-0078d4?style=flat-square)
![License](https://img.shields.io/badge/License-Personal%20Config-green?style=flat-square)

---

## Preview UI

> 📁 Semua screenshot disimpan di folder [`./images/`](./images/)

### Tampilan Utama — Clean Editor + Minimap Auto-Hide

![Main UI](image/main-ui.png)

**Ciri khas:**
- ❌ Tidak ada tab bar (`workbench.editor.showTabs: "none"`)
- ❌ Tidak ada status bar di bawah (`workbench.statusBar.visible: false`)
- ✅ Minimap hanya blok warna, muncul jelas saat hover
- ✅ Scrollbar 6px, auto-hide saat tidak aktif
- ✅ Line numbers normal (bukan relative yang membingungkan)

## Fitur Utama

| Kategori | Fitur |
| :--- | :--- |
| **UI Declutter** | No status bar, no tabs, no minimap text, compact menu bar |
| **Scroll Enhanced** | Smooth scrolling, fast scroll (Alt+wheel), minimap click-to-jump |
| **Terminal** | Split-view di samping code (Zed-style), FiraCode Nerd Font |
| **Discord Presence** | Rich Presence aktif tanpa indikator status bar, custom idle text |
| **Editor** | Line numbers normal, auto-save, bracket pair disabled, indent guides off |
| **Navigation** | File nesting, auto-reveal focus, compact explorer |

---

## Prasyarat

### Extension Wajib

| Extension | ID Marketplace | Fungsi |
| :--- | :--- | :--- |
| **ZED One Theme Dark** | *(search "ZED One Theme")* | Tema utama |
| **Material Icon Theme** | `PKief.material-icon-theme` | Icon file/folder |
| **VSCord** | `LeonardSSH.vscord` | Discord Rich Presence |
| **vscode-pets** | `tonybaloney.vscode-pets` | Pet putih di editor (opsional) |
| **Bongocat Icons** | *(search "bongocat product icon")* | Product icon theme |

### Extension Pendukung (Opsional)

- `ritwickdey.LiveServer` — Live preview HTML
- `formulahendry.code-runner` — Run code snippet
- `ms-vscode.cpptools` — C/C++ IntelliSense
- `ms-vscode.cmake-tools` — CMake integration
- `redhat.vscode-community-server-connector` — Server connector
- `RooVeterinaryInc.roo-cline` — AI coding assistant

### Font

- **[FiraCode Nerd Font](https://www.nerdfonts.com/font-downloads)** — untuk terminal dengan icon support

### External Tools (Windows)

- [Git for Windows](https://git-scm.com/download/win)
- [MSYS2](https://www.msys2.org/) — untuk bash profile tambahan
- MinGW-w64 via MSYS2 (`ucrt64`) — compiler C/C++

---

## Instalasi

### 1. Backup Settings Lama (Opsional tapi Direkomendasikan)

```powershell
Copy-Item "$env:APPDATA\Code\User\settings.json" "$env:APPDATA\Code\User\settings.json.bak"
```

### 2. Buka User Settings JSON

Di VS Code:
- `Ctrl + Shift + P` → ketik **"Preferences: Open User Settings (JSON)"** → Enter

### 3. Paste Konfigurasi

Copy seluruh isi [`settings.json`](./settings.json) di repo ini → paste ke file settings VS Code Anda → Save (`Ctrl+S`).

### 4. Install Extension

```powershell
# Via CLI (jika code command tersedia di PATH)
code --install-extension PKief.material-icon-theme
code --install-extension LeonardSSH.vscord
code --install-extension tonybaloney.vscode-pets

# Atau via UI: Ctrl+Shift+X → search nama extension → Install
```

### 5. Reload Window

`Ctrl + Shift + P` → **"Developer: Reload Window"**

### 6. Setup Discord Presence

1. Buka **Discord Desktop** → User Settings → **Activity Privacy**
2. Aktifkan **"Display current activity as a status message"**
3. Di VS Code, pastikan VSCord sudah enabled (cek Output Panel → VSCord)

---

## Penjelasan Konfigurasi Penting

### Zed-Like Declutter

```jsonc
"workbench.statusBar.visible": false,      // Status bar hidden penuh
"workbench.editor.showTabs": "none",       // No tab bar
"workbench.layoutControl.enabled": false,    // No navigation control
"window.commandCenter": false,             // No command center di title bar
"window.menuBarVisibility": "compact"      // Menu bar menyatu dengan title bar
```

### Enhanced Scroll

```jsonc
"editor.scrollbar.verticalScrollbarSize": 6,           // Scrollbar super tipis (6px)
"editor.mouseWheelScrollSensitivity": 1.5,             // Scroll 1.5x lebih responsif
"editor.fastScrollSensitivity": 5,                     // Alt + scroll = 5x lebih cepat ⚡
"editor.smoothScrolling": true,                        // Scroll halus tidak patah-patah
"editor.minimap.renderCharacters": false,              // Minimap hanya blok warna (clean)
"editor.minimap.showSlider": "mouseover",              // Slider muncul hanya saat hover
"editor.minimap.autohide": true                        // Auto-hide saat tidak aktif
```

> **Tips:** Tahan **`Alt`** saat scroll mouse untuk lompat 5x lebih cepat di file panjang!

### Terminal di Kanan (Zed-Style Split View)

```jsonc
"panel.defaultLocation": "right",                      // Panel default di kanan
"terminal.integrated.defaultLocation": "editor",       // 🔥 Terminal sebagai split editor
"terminal.integrated.fontFamily": "FiraCode Nerd Font",
"terminal.integrated.fontSize": 12
```

> **Alternatif:** Jika prefer terminal di panel kanan (bukan split editor), ganti `"editor"` menjadi `"view"`.

### 🎮 Discord Rich Presence (No Idle Mode)

```jsonc
"vscord.statusBar.enabled": false,                     // Hide indikator status bar
"vscord.details.idle": "📝 Editing {file_name}",       // Samakan dengan editing → tidak pernah "idle"
"vscord.details.editing": "📝 Editing {file_name}",
"vscord.idle.timeout": 86400000,                       // Timeout 24 jam → praktis tidak pernah idle
"vscord.details.notFound": "📓 Jupyter Notebook"       // Fallback untuk file type tidak dikenali
```

### C/C++ Compiler Path (Windows MSYS2)

```jsonc
"C_Cpp.default.compilerPath": "C:\\msys64\\ucrt64\\bin\\gcc.exe"
```

Pastikan MSYS2 terinstall di `C:\msys64` dan package `mingw-w64-ucrt-x86_64-gcc` sudah terinstall:

```bash
pacman -S mingw-w64-ucrt-x86_64-gcc
```

---

## Shortcut Penting

| Shortcut | Fungsi |
| :--- | :--- |
| `` Ctrl+` `` | Toggle terminal (split view) |
| `Ctrl+Shift+P` | Command Palette |
| `Ctrl+P` | Quick Open file |
| `Ctrl+G` | Go to line number |
| `Ctrl+Shift+O` | Go to symbol in file |
| `Alt+↑` / `Alt+↓` | Move line up/down |
| `Ctrl+↑` / `Ctrl+↓` | Scroll without moving cursor |
| `Alt+Scroll` | Fast scroll (5x speed) |
| `Ctrl+Shift+R` | Reload window |

---

> **Tips mengambil screenshot yang konsisten:**
> - Gunakan resolusi lebar 1280px atau 1920px untuk semua gambar
> - Crop rapi — hilangkan taskbar Windows, fokus hanya window VS Code
> - Pastikan tema ZED One Dark aktif saat mengambil screenshot
> - Untuk GIF demo scroll, gunakan [ScreenToGif](https://www.screentogif.com/) (gratis, open source)

---

## Troubleshooting

### Discord Presence Tidak Muncul

1. Pastikan **Discord Desktop** berjalan (bukan web version)
2. Cek Discord Settings → Activity Privacy → aktifkan "Display current activity"
3. Restart Discord sepenuhnya (Quit dari system tray → buka lagi)
4. Cek Output Panel di VS Code: `View → Output → VSCord`
5. Pastikan tidak ada ekstensi Discord lain yang terinstall (konflik IPC)

### File `.ipynb` Tetap Menampilkan "Idle" di Discord

Ini **limitasi arsitektur VS Code** — custom editors (notebook) tidak trigger event `onDidChangeActiveTextEditor` yang dipakai ekstensi Discord [[ref]](https://github.com/iCrawl/discord-vscode/issues/802).

**Workaround:**
- Buka file `.py` apa saja di tab samping → klik sekali → trigger "editing"
- Dengan `vscord.idle.timeout: 86400000`, status akan bertahan 24 jam
- Atau buka notebook sebagai plain text: klik kanan `.ipynb` → "Open With..." → "Text Editor"

### Terminal Masih Muncul di Bawah

Layout panel tersimpan per-workspace. Reset manual sekali:
- `Ctrl+Shift+P` → **"View: Move Panel Right"**
- Atau drag header panel "TERMINAL" ke sisi kanan editor

### Scrollbar Tidak Muncul

Setting `"editor.scrollbar.vertical": "auto"` membuat scrollbar hanya muncul saat scroll/hover. Ini intentional untuk UI clean. Jika ingin selalu visible:

```jsonc
"editor.scrollbar.vertical": "visible"
```

### Gambar Tidak Tampil di README

- Pastikan path file di `./images/` sesuai dengan nama file aktual (case-sensitive di Linux/GitHub)
- Pastikan file gambar sudah di-commit ke repository (jika pakai Git)
- Untuk GitHub, pastikan total ukuran folder `images/` < 50MB agar repo tidak berat

---

## Struktur File Lengkap

```
%APPDATA%\Code\User\
├── settings.json          ← File konfigurasi utama
├── keybindings.json       ← Custom keyboard shortcuts (opsional)
├── snippets\              ← Custom code snippets
└── globalStorage\         ← Data ekstensi

Repo ini:
├── README.md              ← Dokumentasi (file ini)
├── settings.json          ← Konfigurasi siap pakai
└── images\                ← Screenshot UI untuk dokumentasi
    ├── main-ui.png
```

---

## Update Konfigurasi

Jika ada update di repo ini:

```powershell
# Backup dulu
Copy-Item "$env:APPDATA\Code\User\settings.json" "$env:APPDATA\Code\User\settings.json.bak.$(Get-Date -Format 'yyyyMMdd')"

# Copy file baru
Copy-Item ".\settings.json" "$env:APPDATA\Code\User\settings.json" -Force

# Reload VS Code
# Ctrl+Shift+P → Developer: Reload Window
```

---

## Catatan Limitasi

| Fitur | Status | Keterangan |
| :--- | :--- | :--- |
| Discord presence di `.ipynb` | ⚠️ Terbatas | Limitasi VS Code Custom Editor API |
| Status bar fully hidden + Discord | ✅ Works | VSCord pakai IPC langsung, tidak butuh status bar |
| Terminal split view | ✅ Works | Native VS Code feature sejak v1.64 |
| Minimap auto-hide | ✅ Works | Native setting `minimap.autohide` |

---

## Kredit & Referensi

- **Zed Editor** — inspirasi desain UI minimalis
- **VSCord** by [LeonardSSH](https://github.com/LeonardSSH/vscord) — Discord Rich Presence
- **Material Icon Theme** by [PKief](https://github.com/PKief/vscode-material-icon-theme)
- **FiraCode Nerd Font** — [nerdfonts.com](https://www.nerdfonts.com/)
- Komunitas VS Code — dokumentasi custom layout & settings

---

## License

Personal configuration — free to use, modify, and share. No warranty provided.

---

<div align="center">

**Made with ❤️ for productive minimal coding**

*Last updated: August 2026*

</div>