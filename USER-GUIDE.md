# User guide

[Back to README](README.md)

Codebase Compiler combines the readable source files in a project into one `.txt` file. Each file has a relative-path label so readers can tell where the code belongs. Your project is read, not executed.

## Install and open

### Windows installer

1. Download **Windows installer** from the README or the [latest release](https://github.com/Davecaliamugos/Compiler-Downloads/releases/latest).
2. Run `Codebase-Compiler-Setup.exe` and choose an installation folder, or use the default.
3. Leave **Create a desktop shortcut** selected if you want one.
4. Finish setup and open **Codebase Compiler** from the Start menu or desktop.

Setup installs for your Windows account without administrator access. Python is bundled. The default program folder is `%LOCALAPPDATA%\Programs\Codebase Compiler`. The app targets 64-bit Windows 10 and 11.

### Portable edition

1. Download `Codebase-Compiler-Portable.zip` from the release.
2. Right-click the ZIP and choose **Extract All**.
3. Open the extracted `Codebase Compiler` folder and run `Codebase Compiler.exe`.

Run the extracted app from a writable folder. Keep its settings JSON with the EXE when moving it to another folder or drive.

## Export your first project

### 1. Project

Use **Browse** to select the root of your codebase. Use **Save as** to choose a new `.txt` destination. The app explains missing folders and existing filenames beside the fields.

Use **Recent projects** to reopen a saved project. Search by name or path, use arrow keys to select a row, and press Enter to open it. Escape closes the picker. Click **Review exclusions** when ready.

### 2. Exclusions

Switch between **Folders** and **Files & types**. Each optional rule has one of two states:

| State | Meaning |
| --- | --- |
| **Skip** | Exclude matching items. |
| **Keep** | Disable this optional exclusion. Other matching rules, Git ignore rules, protected checks, and limits still apply. |

Click a rule row or press Space to toggle it. Use search to narrow the list. **Skip shown** and **Keep shown** change only the rows visible in the current search.

Use **+ Folder** to choose a subfolder. Use **+ File rule** to add patterns:

| Rule | Example effect |
| --- | --- |
| `*.csv` | Skip matching CSV files. |
| `README.md` | Skip files with this name. |
| `docs/*.md` | Skip matching Markdown files under `docs`. |
| `private` | Skip folders with this name at any depth. |
| `src/internal` | Skip this path within the selected project. |

**Respect Git ignore rules** asks an installed copy of Git to evaluate the repository's ignore rules. Git is optional. If it is unavailable, the app still applies its own rules and reports that Git ignore rules could not be applied.

To include a file excluded by an optional default, set the relevant rule to **Keep**. Disable Git ignore handling too if it also excludes the file. Protected checks cannot be disabled.

**Size limits** changes the default 1 MiB per source file and 50 MiB of combined file blocks. **Restore defaults** resets exclusion rules, Git ignore handling, and limits for the current project.

### 3. File preview

The app scans when you open this screen. Search the tree or choose **All**, **Included**, or **Skipped**. Select a row to see its full relative path and inclusion reason.

Preview shows file paths, decisions, reasons, sizes, and estimated export size. It does not display source contents or detected secret values. An excluded folder appears once; its contents are not scanned. Skipped folder counts refer to whole trees, rather than every file inside them.

Use **Refresh preview** after changing source files. Export always scans again, so counts can change if the project changes after preview.

### 4. Export

Review the project, output path, and exclusion counts, then choose **Export text file**. After completion, use **Open exported file** or **Open folder**.

Review the summary for skipped files, size limits, and warnings. Existing exports are never overwritten; a remembered destination is adjusted to suggest a fresh filename. Processing runs in the background, and relevant controls are locked until it finishes.

## Project profiles

Each project folder remembers its output path, folder and file rules, custom rules, Git ignore preference, and size limits. Switching folders saves the current profile and loads the selected folder's profile. A new folder starts with recommended defaults.

Recent projects are ordered by recent use. Profiles are saved automatically after a short delay and again when the app closes. If a folder has moved or a drive is disconnected, browse to an available location.

## Appearance and startup

Open **Settings** at the bottom of the sidebar. These options apply across projects.

| Setting | Options and behavior |
| --- | --- |
| Theme | **System**, **Light**, or **Dark**. System follows Windows' app appearance and checks for changes while running. |
| Text size | **100%**, **115%**, or **130%**, applied immediately. |
| Reopen last project | Restore the last folder at startup, or start with an empty selection while keeping saved profiles. |
| Remember window | Restore size and position, adjusted to an available monitor. |
| Reset appearance | Restore System theme and 100% text size. |
| Reset startup | Restore the startup defaults. |
| Reset project | Confirm before restoring the current project's exclusion and size defaults. Paths, other projects, and app appearance stay saved. |

Forms scroll when their content exceeds the window. Native Windows file pickers and standard message boxes follow Windows appearance. Custom app screens and dialogs follow the selected app theme.

## Settings storage and backup

| Edition | Preferences file |
| --- | --- |
| Installed | `%LOCALAPPDATA%\Codebase Compiler\User Data\codebase-compiler.settings.json` |
| Portable | `codebase-compiler.settings.json` beside the executable |

Close the app before backing up or restoring the JSON. It contains app settings, project profiles, and local paths. Keep it private unless you intend to share that information. App preference files are always excluded from codebase exports.

## Update or uninstall

**Installed:** close the app and run the newer installer. It recognizes the existing installation and preserves user data. Uninstall from Windows **Settings → Apps → Installed apps** or **Uninstall Codebase Compiler** in the Start menu. Uninstalling removes program files and shortcuts while keeping preferences and exported files.

**Portable:** close all copies of the app. Extract the new download separately, then replace the old EXE in your existing portable folder. Keep `codebase-compiler.settings.json`. Avoid running old and new editions at the same time against a shared settings file.

### Move from portable to installed

1. Close both editions.
2. Copy the portable `codebase-compiler.settings.json`.
3. Press Win+R, enter `%LOCALAPPDATA%`, and open or create `Codebase Compiler`, then its `User Data` subfolder.
4. Paste the JSON into `User Data`. Back up an existing settings file before replacing it.
5. Open the installed app and confirm your settings and recent projects.

Installed and portable editions otherwise use separate settings files.

### Verify a download

Download `SHA256SUMS.txt` from the same release as the app. In PowerShell, run:

```powershell
Get-FileHash "$HOME\Downloads\Codebase-Compiler-Setup.exe" -Algorithm SHA256
Get-FileHash "$HOME\Downloads\Codebase-Compiler-Portable.zip" -Algorithm SHA256
```

Run the command for the edition you downloaded and compare its hash to the matching filename in `SHA256SUMS.txt`. Letter case does not affect the comparison. A matching hash confirms the file matches the release checksum; it is not a publisher signature.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| Documentation downloaded instead of the app | Use the release download buttons. GitHub's **Download ZIP** downloads this repository's documentation. |
| Windows shows an unknown-publisher warning | Current builds are unsigned. Confirm you used this repository's release and verify its checksum. |
| Git ignore warning | Install Git and select a usable Git repository, or use the app's own folder/file rules. |
| A file is missing from the export | Check its preview reason, optional rules, Git ignore rules, size limits, encoding, and protected checks. |
| Preview and export counts differ | Source files may have changed. Refresh preview; export scans the current files. |
| Output already exists | Choose a new filename. Existing exports are not overwritten. |
| Only part of the project was exported | Review size-limit exclusions and other skip reasons in the summary. Increase limits if appropriate. |
| Portable settings do not save | Extract the ZIP and use a writable folder. Keep the JSON beside the EXE. |
| A recent project will not open | Reconnect its drive or browse to an available folder. |
| A file is non-UTF-8 | Convert it to UTF-8 before exporting. UTF-16 and other encodings are skipped. |

For an unresolved problem, [open an issue](https://github.com/Davecaliamugos/Compiler-Downloads/issues) with the app version, Windows version, steps, and relevant error text. Remove private paths, source code, and credentials before posting.

## Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| Ctrl+O | Choose a project folder. |
| Alt+1 / Alt+2 / Alt+3 / Alt+4 | Switch between Project, Exclusions, File preview, and Export. |
| Ctrl+Enter | Start an export after validation. |
| Space | Toggle the selected exclusion rule. |
| Enter / Escape | Open a selected recent project / close the picker. |

## Privacy and file handling

Source files are read locally. The app does not upload your code or execute your project. Git may be invoked locally to evaluate ignore rules.

Environment files, private keys, known credential files, protected folders, detected secrets, symbolic links, junctions, and binary content are skipped. Automatic detection can miss sensitive information and can skip harmless examples. Review every export before sharing; filenames, paths, and code comments can also reveal private information.
