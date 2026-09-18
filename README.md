<div align="center">

<img src="assets/app_icon.png" width="128" alt="SauceBridge icon">

# SauceBridge

### A Windows extension manager for Mihon/Tachiyomi-compatible Android readers

Manage extension repositories, install and update source APKs, detect compatible readers, keep Android Platform-Tools under control, and bridge everything through a clean ADB-powered desktop interface.

<br>

[![Version](https://img.shields.io/badge/version-1.0.1-4C8BF5?style=for-the-badge)](#)
[![Platform](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D4?style=for-the-badge&logo=windows11&logoColor=white)](#)
[![Android](https://img.shields.io/badge/ADB-Platform--Tools-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#)
[![Creator](https://img.shields.io/badge/Created%20by-WBCS-7C3AED?style=for-the-badge)](#)

**English** · [Português (Brasil)](README.pt-BR.md)

</div>

---

## What is SauceBridge?

**SauceBridge** is a Windows desktop application that manages Android manga-reader extension APKs through ADB.

It was built to solve a simple problem: extensions, repositories, reader compatibility, updates, and ADB tooling are usually scattered across different places. SauceBridge brings them into one interface.

Instead of manually downloading APKs, tracking repositories, checking reader versions, and maintaining Platform-Tools yourself, SauceBridge centralizes the workflow.

> **One desktop app. Multiple readers. Multiple repositories. One extension workflow.**

---

## Why SauceBridge?

The Mihon/Tachiyomi extension ecosystem is powerful, but managing it manually can become repetitive.

SauceBridge focuses on the parts that benefit from deterministic tooling:

- **Repository aggregation** — load multiple compatible extension repositories at once.
- **Package-aware deduplication** — avoid blindly replacing the same Android package across repositories.
- **ADB-based device state** — installed versions come from the connected Android device, not stale local assumptions.
- **Reader detection** — detect known readers and compatible forks.
- **Repository bridging** — send repository URLs to readers that support compatible deep links.
- **Portable Platform-Tools** — manage ADB without requiring a full Android Studio installation.
- **Diagnostics and recovery** — persistent logs, settings backup, crash reports, and a portable diagnostic report.

---

## Highlights

| Feature | What it does |
|---|---|
| **Install** | Install extension APKs directly to the connected Android device |
| **Update** | Detect installed extensions with a newer repository version |
| **Uninstall** | Remove installed extensions from the device |
| **Batch operations** | Install multiple APKs using ADB multi-package mode |
| **Multiple repositories** | Merge several compatible extension catalogs |
| **PT-BR repositories** | Built-in presets include repositories focused on Brazilian Portuguese sources |
| **Reader Manager** | Detect Mihon, Komikku, Aniyomi, DropSauce and compatible forks |
| **Repository bridge** | Send compatible repository URLs to detected readers |
| **Reader updates** | Check the latest known release for supported readers |
| **Platform-Tools Manager** | Install, update, reinstall, or use an external ADB |
| **Offline cache** | Fall back to cached catalogs when a repository is unavailable |
| **Advanced search** | Search by name, Android package, source, site, language, or repository |
| **Persistent diagnostics** | Rotating logs, crash report, settings recovery, and diagnostic export |

---

## Supported reader families

SauceBridge currently includes detection logic for readers and forks in the Mihon/Tachiyomi ecosystem, including:

| Reader / family | Extension workflow | Repository bridge |
|---|---:|---:|
| **Mihon** | APK extensions | `tachiyomi://` when supported |
| **Komikku** | APK extensions | `tachiyomi://` |
| **TachiyomiJ2K** | APK extensions | `tachiyomi://` |
| **TachiyomiSY** | APK extensions | `tachiyomi://` |
| **TachiyomiAZ** | APK extensions | `tachiyomi://` |
| **Aniyomi** | Manga / anime APK extensions | `aniyomi://` / compatible fallback |
| **Animiru** | Compatible APK extensions | compatible deep-link workflow |
| **Nekoyomi** | Extension repositories | compatible deep-link workflow |
| **Reikai / Yōkai family** | Compatible APK extensions | compatible deep-link workflow |
| **Blueth Yokai** | Compatible APK extensions | compatible deep-link workflow |
| **DropSauce** | Mihon APK / related extension formats | safe manual URL fallback |
| **Tachiyomi legacy** | Legacy APK extensions | legacy compatibility |

Unknown forks that advertise a compatible `tachiyomi://` or `aniyomi://` handler can also be discovered automatically.

> Extension APKs themselves are explicitly filtered out and never shown as readers.

---

## Built-in repository library

SauceBridge ships with a repository library so users do not have to search for repository URLs manually.

Examples include:

- Keiyoushi
- Yūzōnō
- Cursed Yūzōnō
- FelipeGFA · PT-BR
- Project Nox · PT-BR
- Mihon Nexus · PT-BR
- MHExtensions
- filtered / legacy presets available on demand

Repositories can be enabled, disabled, reordered, edited, or added manually.

### Package conflict strategy

If multiple repositories expose the same Android package, SauceBridge keeps repository priority deterministic instead of silently swapping packages based only on a higher `versionCode`.

This reduces the chance of Android signature conflicts between forks.

---

## Quick start

1. Download the latest portable ZIP from **Releases**.
2. Extract the `SauceBridge` folder.
3. Open `SauceBridge.exe`.
4. Connect your Android device over USB.
5. Enable **USB debugging** and authorize the computer.
6. If needed, open **Platform-Tools** inside SauceBridge and install the managed ADB package.
7. Select the extensions you want and install.

> SauceBridge is portable. No Python installation is required.

---

## Portable data layout
---

## Portable data layout

Writable data stays beside `SauceBridge.exe`:

```text
SauceBridge/
├── SauceBridge.exe
├── settings.json
├── settings.json.bak
├── cache/
├── diagnostics/
├── logs/
├── platform-tools/
├── profiles/
└── _internal/
```

Bundled read-only assets are loaded from the PyInstaller resource directory.

---

## Platform-Tools management

SauceBridge can manage its own copy of Android Platform-Tools.

Available actions include:

- check for updates;
- install;
- update;
- reinstall;
- switch to the managed ADB;
- select an external `adb.exe`;
- open the Platform-Tools folder;
- open official release notes.

Automatic checks are non-destructive: SauceBridge never installs a Platform-Tools update without user confirmation.

External ADB installations are never overwritten.

---

## Safety and reliability

SauceBridge avoids fragile automation where possible.

### Reader repositories

When a reader supports a compatible repository deep link, SauceBridge sends the URL through Android's intent system and lets the reader confirm it.

When no stable public deep link is known, SauceBridge falls back to:

```text
Copy repository URL → Open reader → User confirms manually
```

It does **not** modify private reader databases directly.

### Settings

`settings.json` is written atomically and automatically backed up.

If the settings file becomes malformed:

```text
settings.json
        ↓
settings.corrupt-YYYYMMDD-HHMMSS.json
        ↓
safe defaults
```

The application remains startable and reports the recovery in its log.

---

## Diagnostics

SauceBridge includes several troubleshooting layers:

```text
logs/SauceBridge.log
saucebridge-crash.log
diagnostics/diagnostic-*.txt
run-debug.bat
```

The diagnostic report can include:

- SauceBridge version;
- Windows and Python information;
- ADB / Platform-Tools version;
- connected device state;
- active repositories;
- loaded extensions;
- installed extensions;
- available updates;
- detected readers;
- cache information;
- runtime paths.

---

## Project structure

```text
SauceBridge/
├── assets/
│   ├── app_icon.ico
│   ├── app_icon.png
│   └── creator_signature.png
│
├── core/
│   ├── adb.py
│   ├── cache.py
│   ├── models.py
│   ├── platform_tools.py
│   ├── readers.py
│   ├── repo.py
│   ├── repositories.py
│   └── runtime.py
│
├── main.py
├── preflight.py
├── SauceBridge.spec
├── requirements.txt
├── build.bat
├── run.bat
├── run-debug.bat
├── PORTABLE.txt
└── README.md
```

---

## Design principles

SauceBridge follows a few simple rules:

### Device state is authoritative

Installed package/version information should come from Android through ADB whenever possible.

### Repository actions are explicit

Repository priority and package conflicts should be predictable.

### External tools remain replaceable

Users may use SauceBridge-managed Platform-Tools or their own `adb.exe`.

### Reader internals stay private

SauceBridge prefers public Android intents and documented interfaces instead of directly modifying private app databases.

### Portable means portable

Runtime data should stay with the application folder and remain easy to back up, inspect, or remove.

---

## Roadmap

Post-1.0 development can focus on:

- richer reader profiles;
- additional repository formats;
- improved update providers;
- optional automated reader APK updating with signature validation;
- repository health checks;
- extension compatibility reports;
- localization.

---

## Contributing

Issues, testing reports, repository compatibility findings, and pull requests are welcome.

When reporting a problem, include the generated diagnostic report whenever possible.

Please **do not** include personal files, account credentials, API keys, or other private information in an issue.

---

## Disclaimer

SauceBridge is an independent project.

It is not an official client of Mihon, Tachiyomi, Aniyomi, Komikku, DropSauce, or any extension repository listed by the application.

Third-party project names and trademarks belong to their respective owners.

SauceBridge only manages repository metadata, extension packages, reader integration, and ADB workflows selected by the user.

---

<div align="center">

<img src="assets/creator_signature.png" width="220" alt="WBCS signature">

### Created by WBCS

**SauceBridge · Windows ↔ Android extension bridge**

</div>
