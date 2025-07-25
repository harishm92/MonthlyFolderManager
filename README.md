# MonthlyFolderManager
A cross-platform command-line utility that creates year-specific month folders ((01)Jan-YYYY … (12)Dec-YYYY) and interactively moves or copies files into the correct month based on dates detected in their filenames.

## Features

- Prompt for target **year** and base directory.
- Generates/renames 12 month folders using format `(MM)Mon-YYYY`.
- Recursively scans any source directory for dates in filenames.
- Supports multiple date formats, e.g. `YYYYMMDD`, `YYYY-MMM-DD`, `DD-MM-YYYY`, and more.
- Interactive preview tables (powered by `prettytable`) show up to 50 matches, with option to display all.
- Choice to **move** or **copy** files, with automatic suffix `-YYYYMMDD` appended.
- Handles name collisions with numeric suffixes (`_1`, `_2`, …).
- Loops until you choose to quit, letting you process multiple years or sources.

## Installation

### 1. Clone the repository
```bash
gh repo clone harishm92/MonthlyFolderManager
cd MonthlyFolderManager
```

### 2. Create virtual environment (recommended)
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

*Only one runtime dependency:* **prettytable** for nice console tables.

## Usage
```bash
python MonthlyFolderManager.py
```
Follow the on-screen prompts:
1. Enter the base directory for `(MM)Mon-YEAR` folders.
2. Enter the **year** to organise.
3. Point the tool at any directory to scan recursively.
4. Review the preview table (optionally list all files).
5. Choose **move** or **copy**, and destination (base dir or another dir).
6. Confirm – the tool processes files and loops for further sorting.

### Building Stand-Alone Executables
Generate single-file binaries with **PyInstaller**:
```bash
pip install pyinstaller
pyinstaller --onefile --hidden-import=prettytable --name "MonthlyFolderManager" MonthlyFolderManager.py
```
The executable will be in `dist/` (Windows `.exe`, Linux/macOS without extension).

## Project Structure
```
MonthlyFolderManager/
├── MonthlyFolderManager.py     # main script
├── requirements.txt            # runtime deps
├── LICENSE                     # MIT License
├── README.md                   # this file
└── .gitignore                  # ignores venvs, build artefacts, etc.
```

## Contributing
Pull requests are welcome! Please open an issue first to discuss major changes.

1. Fork the project & create your feature branch (`git checkout -b feature/my-feature`).
2. Commit your changes (`git commit -m 'Add some feature'`).
3. Push to the branch (`git push origin feature/my-feature`).
4. Open a Pull Request.

## License
This project is licensed under the MIT License – see the `LICENSE` file for details.

## Attribution
Built with the assistance of Perplexity AI’s chat assistant.
"Documentation and feature planning supported by Perplexity AI ChatGPT-style assistant."

Attribution is optional – the MIT License allows reuse without credit – but a note of thanks is always appreciated!
