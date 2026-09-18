# Changelog

All notable changes to SauceBridge are documented here.

The project uses release tags in the `vMAJOR.MINOR.PATCH` format.

## [1.0.1] — 2026-09-17

### Added
- Portable Windows release based on PyInstaller `onedir`.
- Multi-repository extension catalog management.
- Built-in repository library with PT-BR and community presets.
- Install, update, and uninstall workflows for Android extension APKs.
- Batch installation using ADB multi-package mode.
- Reader Manager with detection for Mihon/Tachiyomi-compatible applications.
- Generic reader discovery through compatible `tachiyomi://` and `aniyomi://` handlers.
- Repository bridging to supported readers.
- Reader release/update checks for known projects.
- Managed Android Platform-Tools installation and update workflow.
- Offline catalog cache.
- Extension icons, detail panel, multi-language metadata, and source links.
- Advanced search and sortable extension tables.
- Persistent rotating logs and portable diagnostic reports.
- Atomic settings writes, backups, and corrupt-settings recovery.
- SauceBridge branding and creator signature `WBCS`.

### Fixed
- Reader Manager no longer identifies extension APKs as reader applications.
- PyInstaller resource paths correctly separate bundled assets from writable portable data.
- CustomTkinter startup crash caused by invalid `width=None` header configuration.
- Windows temporary APK file locking during installation.
- HyperOS USB-install error handling.
- Multi-language repository entries no longer lose PT-BR visibility.

## [1.0.0] — 2026-09-17

Initial stable release milestone.

---

Earlier development builds (`0.x`) were iterative internal/pre-release versions leading to the 1.0 line.
