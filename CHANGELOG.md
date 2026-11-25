# Changelog

## 1.4.0

### Windows installer

- Per-user setup with Start menu entries, an optional desktop shortcut, and an uninstaller.
- User preferences stored separately from installed program files, preserving settings and project profiles across updates.
- Preferences and exported files retained when uninstalling.
- Portable edition remains available alongside the installer.

### Included app features

- Searchable file-list preview with inclusion decisions, skip reasons, file sizes, and estimated export size.
- Per-project profiles and a searchable recent-project picker.
- System, Light, and Dark themes; text-size choices; startup preferences; and scoped reset controls.
- Local UTF-8 export with default exclusions, protected sensitive-file checks, optional Git ignore handling, and size limits.

### Validation

- 29 automated tests passed.
- Bundled runtime passed a 502-file GUI export with matching preview counts and bytes.
- Isolated installation, shortcut targets, upgrade settings preservation, and uninstall behavior verified.
