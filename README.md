Word for Windows Password Recovery
==================================

This repository preserves two vintage utilities that strip or recover passwords from Word for Windows 2.0 and 6.0 documents. It is a fork of Marc Thibault's public-domain **Word Unprotect** tool, with light updates so it builds cleanly on modern macOS/Linux systems, plus the original DOS/Windows binaries and a freeware password cracker.

## What changed in this fork
- Updated `wu.cpp` (version `1.2rd`) so it compiles with current g++ on macOS/Linux; kept the original algorithm intact.
- Documented how to build and run the tool without needing a DOS emulator.
- Collected the original DOS/Windows binaries, docs, and signature files in one place for easy reference.

## Project layout
- `wu/` — Source for Word Unprotect plus the original DOS (`DOSWU.EXE`), Windows (`WINWU.EXE`) binaries, and `WU.DOC`.
- `wfwcd/` — Fauzan Mirza's 1995 Word for Windows Password Cracker demo (`wfwcd.exe`) and accompanying text.
- `LICENSE` — Original public-domain notice from Marc Thibault.

## Build and run Word Unprotect on macOS/Linux
Word Unprotect removes the protection flag from Word 2.0/6.0 documents by extracting the embedded XOR key (it does not recover the human-readable password).

```
gh repo clone rdubar/WordUnprotect
cd WordUnprotect/wu
g++ -o wu wu.cpp
./wu path/to/encrypted.doc path/to/output.doc
```

- The output file is decrypted in-place while the source remains unchanged.
- Exit codes: `1` missing args, `2` input open error, `3` output open error, `4` key not found, `5` file too short, `6` write error.

If you prefer the original binaries, `DOSWU.EXE` and `WINWU.EXE` still work in DOSBox/Windows; `DOSWU.SIG` can be used with the PGP key in `WU.DOC`.

## Using WFWCD (password recovery demo)
`wfwcd/wfwcd.exe` is a freeware demo that attempts to recover the actual password (instead of just decrypting) for Word 2.0 and 6.0 documents. It was built for DOS; run it in DOSBox or another DOS environment:

```
WFWCD <DocumentPath>
```

It assumes mostly lowercase English text and can fail on very short or non-text-heavy documents. See `wfwcd/wfwcd.txt` for the author's technical notes and license.

## Credits and provenance
- **Word Unprotect** — Marc Thibault, 26 Jan 1993, public domain. See comments in `wu/wu.cpp` and `WU.DOC`.
- **Word for Windows Password Cracker (R8)** — Fauzan Mirza, 1995, freeware without source. See `wfwcd/wfwcd.txt`.

Please use these tools responsibly and only on documents you are authorized to access. The goal of this fork is preservation and making the utilities runnable on modern platforms without altering their behavior.
