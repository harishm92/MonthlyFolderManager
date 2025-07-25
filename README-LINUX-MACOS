<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# Installing the “Monthly Folder Manager” on Linux \& macOS

Below are step-by-step, platform-specific workflows that take you from source code to a readyto-run command-line tool.  Two distribution models are covered:

1. A **stand-alone native executable** built with PyInstaller (no Python required for end-users).
2. A **pipx-managed CLI package** (best for Python-savvy users who prefer isolation without manual virtual-env work).

## 1. Building \& Installing a Stand-Alone Executable with PyInstaller

### 1.1  Common Prerequisites

- Python 3.8-3.13 and pip installed on the build machine (not needed on the target once the binary is built).
- PyInstaller ≥ 6.0 (`pip install --upgrade pyinstaller`)[^1][^2].

> PyInstaller is **not** cross-compiling—build each target on the same OS you intend to ship for[^3].

### 1.2  Linux Build \& Deploy

1. **Clone the project**

```bash
git clone https://github.com/harishm92/MonthlyFolderManager.git
cd MonthlyFolderManager
```

2. **Create the single-file executable**

```bash
pyinstaller --onefile monthly_folder_manager.py \
            --name MonthlyFolderManager
```

    - The binary appears in `dist/MonthlyFolderManager`.
3. **Strip executable \& mark as runnable (optional)**

```bash
strip dist/MonthlyFolderManager        # smaller size
chmod +x dist/MonthlyFolderManager[^4]
```

4. **Distribute**
Copy or tar/zip the file and place it anywhere on the user’s `PATH` (e.g., `/usr/local/bin`).

```bash
sudo mv MonthlyFolderManager /usr/local/bin/
```

5. **Run**

```bash
MonthlyFolderManager
```


### 1.3  macOS Build, Sign \& Notarise (Optional)

1. **Install PyInstaller as above** (`pip install pyinstaller`)[^1].
2. **Create the binary**

```bash
pyinstaller --onefile MonthlyFolderManager.py \
            --name MonthlyFolderManager
```

3. **(Recommended) Sign the binary**

```bash
codesign --deep --force \
         --sign "Developer ID Application: Your Name (TEAMID)" \
         dist/MonthlyFolderManager[^38][^40]
```

4. **(Optional) Notarise for Gatekeeper**

```bash
xcrun notarytool submit dist/MonthlyFolderManager.zip \
      --keychain-profile "<profile-name>" --wait[^7][^12]
xcrun stapler staple dist/MonthlyFolderManager
```

5. **Distribute \& first-run instructions**
Copy to `/usr/local/bin`, then tell users to bypass Gatekeeper for unsigned builds:

```bash
sudo spctl --master-disable   # enable “Anywhere” temporarily[^10]
```

6. **Run**

```bash
MonthlyFolderManager
```


## 2. Shipping via pipx (Python 3.8+ already present)

`pipx` installs each CLI in its own virtual-env and shim, so updates and removal never collide with system Python[^4][^5][^6].

### 2.1  Quick-Install pipx

| Platform | Command |
| :-- | :-- |
| macOS | `brew install pipx && pipx ensurepath`[^5][^7] |
| Ubuntu ≥ 23.04 | `sudo apt install pipx && pipx ensurepath`[^5][^7] |
| Fedora | `sudo dnf install pipx && pipx ensurepath`[^7] |
| Any Linux | `python3 -m pip install --user pipx && python3 -m pipx ensurepath`[^5] |

Restart the terminal so that `$PATH` picks up `~/.local/bin`.

### 2.2  Publish Your Package to PyPI (once)

1. Add a minimal `setup.py`/`pyproject.toml` with an **entry-point**:

```toml
[project]
name = "MonthlyFolderManager"
version = "1.0.0"
description = "CLI to create year-month folders and sort files"
dependencies = ["prettytable"]

[project.scripts]
mfmanager = "MonthlyFolderManager:main"
```

2. Build \& upload:

```bash
python -m pip install --upgrade build twine
python -m build
twine upload dist/*
```


### 2.3  End-User Installation

```bash
pipx install MonthlyFolderManager
mfmanager   # alias created by entry-point
```

Upgrade later with:

```bash
pipx upgrade MonthlyFolderManager
```

Uninstall cleanly:

```bash
pipx uninstall MonthlyFolderManager
```


## 3. Choosing Between the Two Methods

| Criterion | PyInstaller Binary | pipx Package |
| :-- | :-- | :-- |
| Python required on target | **No** | Yes (≥3.8) |
| Footprint | Larger single file | Small venv |
| Auto-updates | Manual replace | `pipx upgrade` |
| macOS Gatekeeper hassle | Must sign/notarise | Same as any PyPI tool |
| Ideal audience | Non-technical users | Developers / power users |

## 4. Attribution


> Documentation assistance courtesy of *Perplexity AI ChatGPT-style assistant*.

No additional licence text is required.

### Enjoy effortless month-wise organisation on every platform!

<div style="text-align: center">⁂</div>

[^1]: https://pyinstaller.org/en/v5.1/installation.html

[^2]: https://pypi.org/project/pyinstaller/

[^3]: https://www.pyinstaller.org

[^4]: https://dev.to/bowmanjd/how-do-i-install-a-python-command-line-tool-or-script-hint-pipx-3i2

[^5]: https://pipx.pypa.io/stable/installation/

[^6]: https://github.com/pypa/pipx

[^7]: https://pipx.pypa.io/stable/

[^8]: https://haim.dev/posts/2020-08-08-python-macos-app/

[^9]: https://www.warp.dev/terminus/chmod-x

[^10]: https://people.ohio.edu/hadizadm/blog_files/tag-how-to-allow-apps-from-anywhere-in-macos-gatekeeper-.html

[^11]: https://stackoverflow.com/questions/64652704/how-to-notarize-an-macos-command-line-tool-created-outside-of-xcode

[^12]: https://www.kali.org/tools/python-pipx/

[^13]: https://apple.stackexchange.com/questions/303563/are-the-files-given-permission-with-chmod-x-saved-somewhere

[^14]: https://osxdaily.com/2016/09/27/allow-apps-from-anywhere-macos-gatekeeper/

[^15]: https://pyinstaller.org/en/stable/installation.html

[^16]: https://blog.csdn.net/Le_1M/article/details/142355651

[^17]: https://superuser.com/questions/1358390/how-to-add-chmod-x-on-a-file-from-right-click-menu-service-in-mac

[^18]: https://support.apple.com/guide/apple-business-essentials/gatekeeper-settings-axmd2430181c/web

[^19]: https://developer.apple.com/forums/thread/698565

[^20]: https://stackoverflow.com/questions/8409946/how-do-i-make-this-file-sh-executable-via-double-click

[^21]: https://www.techradar.com/how-to/computing/apple/how-to-let-gatekeeper-open-mac-apps-from-unidentified-developers-1299143

[^22]: https://www.youtube.com/watch?v=S_Bus_FNjpg

[^23]: https://www.youtube.com/watch?v=AS4F_qGkcUk

[^24]: https://www.youtube.com/watch?v=gsSjIx_uFG4

[^25]: https://www.youtube.com/watch?v=n4camz0YRqU

[^26]: https://www.youtube.com/watch?v=JRACIWndz20

[^27]: https://www.youtube.com/watch?v=t51bT7WbeCM

[^28]: https://www.youtube.com/watch?v=6Os_Quocuyc

[^29]: https://www.youtube.com/watch?v=e5mJuVcwoA4

[^30]: https://github.com/pyinstaller/pyinstaller/issues/5434

[^31]: https://realpython.com/python-pipx/

[^32]: https://linuxconfig.org/how-to-install-python-applications-in-isolated-environments-with-pipx

[^33]: https://github.com/pypa/pipx/issues/1481

[^34]: https://gist.github.com/txoof/0636835d3cc65245c6288b2374799c43

[^35]: https://web.archive.org/web/20230605082020/https:/github.com/pypa/pipx

[^36]: https://itsfoss.com/install-pipx-ubuntu/

[^37]: https://blog.csdn.net/hiliang521/article/details/140476445

[^38]: https://dev.to/waylonwalker/installing-pipx-on-ubuntu-2cdl

[^39]: https://blog.csdn.net/yuanya/article/details/23599665

[^40]: https://libraries.io/pypi/pipx

[^41]: https://forum.xojo.com/t/simple-command-line-code-sign/32619

[^42]: https://askubuntu.com/questions/1481763/importing-python-packages-installed-with-pipx

[^43]: https://github.com/pyinstaller/pyinstaller/wiki/Recipe-OSX-Code-Signing

[^44]: https://github.com/msaldivar/pipx-feature-enhancement

