# JP Unzip

A single-file desktop tool for extracting ZIP archives that contain Japanese filenames. Handles the encoding mismatches that cause standard unzip tools to produce garbled or corrupted filenames when unpacking Japanese ZIP files. No installation required — just run the `.exe`.

---

## Features

- Extracts ZIP files while correctly preserving Japanese filenames
- Follows an encoding priority chain to handle different filename encodings
- Simple GUI — no command line required

---

## Requirements

- Windows

---

## Usage

1. Run `JP_Unzip.exe`
2. Drag and drop a ZIP file onto the window, or use the file picker
3. Click **Extract**

Files are extracted into the same folder as the ZIP file. A progress bar tracks extraction status.

---

## How Encoding Detection Works

The original ZIP format did not standardize filename encoding, so Japanese ZIP files can use several different encodings depending on where and when they were created. JP Unzip handles this through a priority chain:

1. **UTF-8** — If the ZIP entry has its UTF-8 flag set, the filename is decoded as UTF-8. Modern ZIP tools set this flag explicitly, making detection unambiguous.
2. **cp932** — If no UTF-8 flag is present, the tool assumes cp932 (Microsoft's superset of Shift-JIS, the standard encoding for Japanese Windows systems). This covers the vast majority of Japanese ZIP files in the wild.
3. **cp437** — If cp932 decoding fails, the tool falls back to cp437, the original IBM PC encoding that the ZIP format defaulted to in the 1980s.

---

## Known Limitations

### No automatic encoding detection for ambiguous files
The tool follows the priority chain above rather than attempting to heuristically detect encoding. Files that are neither flagged UTF-8 nor cp932 but happen to decode without errors under cp932 will be decoded as cp932, which may produce wrong results in rare edge cases.

### cp437 fallback is a last resort
cp437 cannot represent Japanese characters. If a filename reaches the cp437 fallback stage, it means the file was not encoded in UTF-8 or cp932, and the extracted filename will likely not be in Japanese. The file contents themselves are unaffected.

### Windows only
The executable is built for Windows. It is not compatible with macOS or Linux.

---

## Suggestions

If you have ideas for features, improvements, or encoding edge cases this tool doesn't handle well, feel free to open an issue. Feedback is welcome.

---

## License

This project is licensed under the MIT License. You are free to use, copy, modify, merge, publish, distribute, and sublicense it, provided the original copyright notice is kept intact.

---

Built with the assistance of [Claude](https://claude.ai), an AI assistant by [Anthropic](https://www.anthropic.com).
