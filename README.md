<h1 align="center">ChinnarTuber</h1>

<p align="center">
  <strong>Ultra-lightweight YouTube player for Windows</strong><br/>
  <strong>About 50 MB RAM</strong> &mdash; watch YouTube without a heavy browser<br/>
  超軽量 YouTube プレイヤー &mdash; メモリ約 50MB で YouTube を視聴
</p>

<p align="center">
  <img src="https://img.shields.io/badge/RAM-About%2050MB-2ea44f" alt="RAM About 50MB" />
  <img src="https://img.shields.io/badge/Download-1.8MB-2ea44f" alt="Download 1.8MB" />
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License: MIT" /></a>
  <img src="https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet&logoColor=white" alt=".NET 8" />
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11-0078D4?logo=windows&logoColor=white" alt="Windows 10/11" />
</p>

---

**ChinnarTuber uses about 50 MB of RAM** — a fraction of what Chrome or Edge consumes for a single YouTube tab. Built on Microsoft Edge WebView2, it gives you a dedicated YouTube window with always-on-top, PiP snap, ad blocking, and more, without the overhead of a full browser.

**ChinnarTuber のメモリ使用量はわずか約 50MB。** Chrome や Edge で YouTube タブを1つ開くだけで 300〜500MB 消費するのに対し、圧倒的に軽量です。WebView2 をベースに、常に前面表示・PiP 風スナップ・広告ブロック等を備えた専用プレイヤーです。

### Why ChinnarTuber?

| | Chrome / Edge | ChinnarTuber |
|---|---|---|
| **RAM usage** | 300 - 500 MB per tab | **About 50 MB** |
| **Download size** | 200 - 300 MB | **1.8 MB** |
| **Startup** | Heavy (loads entire browser) | Instant |
| **Purpose** | General browsing | YouTube only, optimized |

## Download

Get the latest build from **[Releases](../../releases)**.

| File | Description |
|------|-------------|
| **`ChinnarTuber-1.0.0-win-x64.zip`** | Portable — extract anywhere and run `ChinnarTuber.exe` |

### Quick start

1. Download and extract the ZIP.
2. Run `ChinnarTuber.exe`.
3. On first launch, settings are created under `%LocalAppData%\ChinnarTuber\`.
4. If supported by your WebView2 runtime, the **AdGuard** browser extension is downloaded automatically (~31 MB, internet required).

## Features

| Feature | Description |
|---------|-------------|
| **Always on top** | Keep the window above other apps (`Ctrl+T`) |
| **Bottom-right snap** | PiP-style 640×360 window in the corner (`Ctrl+R`) |
| **Fullscreen** | Fill the screen (`F11`, `Esc` to exit). Respects toolbar pin setting |
| **Ad blocking** | AdGuard extension when available; built-in filter as fallback |
| **Auto-hide toolbar** | Pin the toolbar or reveal it by moving the mouse to the top edge |
| **YouTube-only navigation** | Address bar accepts YouTube-related URLs only (`youtube.com`, `youtu.be`, etc.) |
| **Keyboard shortcuts** | Browser-style shortcuts for navigation and window control |
| **Bilingual UI** | English / 日本語 (`Ctrl+Shift+L`) |
| **Dark theme** | Dark title bar and UI aligned with YouTube viewing |

## Requirements

| | |
|---|---|
| **OS** | Windows 10 / 11 (x64) |
| **Runtime** | [.NET 8 Desktop Runtime](https://dotnet.microsoft.com/download/dotnet/8.0/runtime) |
| **Browser engine** | [Microsoft Edge WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/) (usually included with Edge) |

> **Note:** If WebView2 extension APIs are unavailable on your system, ChinnarTuber falls back to a built-in ad blocker instead of AdGuard.

## Keyboard shortcuts

| Key | Action |
|-----|--------|
| `Alt+←` / `Alt+→` | Back / Forward |
| `F5` | Reload |
| `Alt+Home` | YouTube Home |
| `Ctrl+W` / `Ctrl+F4` | Close window |
| `Ctrl+T` | Toggle always on top |
| `Ctrl+R` | Toggle bottom-right snap |
| `F11` | Toggle fullscreen |
| `Ctrl+L` / `F6` | Focus address bar |
| `Enter` | Navigate to address bar URL |
| `Esc` | Focus page (exits fullscreen while in fullscreen mode) |
| `Ctrl+Shift+T` | Toggle toolbar pin |
| `Ctrl+Shift+A` | Toggle ad blocker |
| `Ctrl+Shift+L` | Toggle language |
| `F1` | Help |

Press `F1` in the app for the full help screen, including context menu options and disclaimers.

## Build from source

Requires [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) on Windows.

```powershell
dotnet publish ChinnarTuber/ChinnarTuber.csproj -c Release
```

Output directory:

```text
ChinnarTuber/bin/Release/net8.0-windows/win-x64/publish/
```

To create the release ZIP (same layout as GitHub Releases):

```powershell
$publishDir = "ChinnarTuber/bin/Release/net8.0-windows/win-x64/publish"
$staging = "$env:TEMP/ChinnarTuber-staging"
Remove-Item $staging -Recurse -Force -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Path $staging | Out-Null
Copy-Item "$publishDir/ChinnarTuber.exe", "$publishDir/WebView2Loader.dll" $staging
Copy-Item "$publishDir/runtimes" "$staging/runtimes" -Recurse
Copy-Item LICENSE "$staging/LICENSE.txt"
Compress-Archive -Path "$staging/*" -DestinationPath "installer/output/ChinnarTuber-1.0.0-win-x64.zip" -Force
```

## Project structure

```text
ChinnarTuber/
├── ChinnarTuber/          # WPF application (.NET 8)
│   ├── MainWindow.*       # Main browser window
│   ├── HelpWindow.*       # Help dialog
│   ├── Services/          # Settings, WebView2, ad blocker
│   ├── Helpers/           # Window theme, placement, monitors
│   └── Localization/      # English / Japanese strings
├── installer/             # Inno Setup script (optional .exe installer)
└── LICENSE                # MIT
```

## Third-party software

| Component | License | Role |
|-----------|---------|------|
| [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) | Microsoft terms | Browser engine |
| [AdGuard Browser Extension](https://github.com/AdguardTeam/AdguardBrowserExtension) | GPL v3 | Ad blocking (when extension APIs are available) |

ChinnarTuber is **not affiliated with** Google, YouTube, Microsoft, or AdGuard.

## Disclaimer

- ChinnarTuber is **not** an official Google or YouTube product.
- Use of YouTube is subject to the [YouTube Terms of Service](https://www.youtube.com/t/terms).
- Ad blocking may not remove all ads; YouTube changes may affect playback or ad visibility. Use at your own discretion.
- This software is provided **"AS IS"** under the MIT License, without warranty of any kind.

## License

[MIT](LICENSE) © 2026 [Chinna Power LLC](https://github.com/chinnapower)
