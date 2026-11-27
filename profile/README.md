<p align="center"><img src="https://raw.githubusercontent.com/go-binfmt/brand/main/social/go-binfmt.png" alt="go-binfmt" width="640"></p>

<h1 align="center">go-binfmt</h1>
<p align="center">Pure-Go tooling for <strong>binary formats</strong>, starting with <strong>ELF</strong> — read and edit executables and shared objects with <strong>no cgo</strong> and <strong>no patchelf / binutils</strong>.</p>
<p align="center">
  <img src="https://img.shields.io/badge/Go-1.26-00ADD8?style=flat-square&logo=go&logoColor=white">
  <img src="https://img.shields.io/badge/license-BSD--3--Clause-0A6E96?style=flat-square">
  <a href="https://go-binfmt.github.io/"><img src="https://img.shields.io/badge/site-go--binfmt.github.io-0079A8?style=flat-square"></a>
  <a href="https://go-binfmt.github.io/docs/"><img src="https://img.shields.io/badge/docs-hextra-0079A8?style=flat-square"></a>
</p>

## What this is

go-binfmt holds pure-Go tools for binary object and executable formats. Today
that is **ELF**, the format of Linux and the BSDs: change an executable's
interpreter, its `RUNPATH`/`RPATH` or its `DT_NEEDED` entries without a C
toolchain, on any host Go runs on. The PE/COFF and UEFI side lives in
[go-coff](https://github.com/go-coff).

## Repositories

| Repo | What it is |
| --- | --- |
| [`elfpatch`](https://github.com/go-binfmt/elfpatch) | A pure-Go replacement for the subset of [NixOS patchelf](https://github.com/NixOS/patchelf) that package builders use, with patchelf's flag names. Edits the interpreter, `RUNPATH`/`RPATH` and `DT_NEEDED` **in place**; writes are atomic, and every write is re-parsed and checked so that only the targeted field changed. A value that does not fit is refused, never truncated. `--dry-run` prints the change and writes nothing. Differential tests run against patchelf in CI. Growing `.dynstr`/`PT_INTERP` is phase 2. |
| [`fwimg`](https://github.com/go-binfmt/fwimg) | Converts an ELF executable into the image a bootloader or ROM loads at a fixed address: a flat binary (`objcopy -O binary`), a Motorola S-record, Intel HEX, a U-Boot uImage (gzip or lz4 too), a UF2 file or a Verilog hex memory file, with no binutils or `mkimage`. An image size taken from attacker-controlled addresses, a segment outside the input, an address range that wraps and data past 4 GiB are refused, never truncated. Moved here from `go-coff/peln/fwimg`. |
| [`fdt`](https://github.com/go-binfmt/fdt) | A pure-Go reader and writer for **devicetree blobs** (DTB v17), the format of `dtc -O dtb` and of the FIT images U-Boot loads. Every bound of untrusted input is checked, and the output is byte-identical to `dtc`. No cgo, no libfdt. |

## Links

- Landing — <https://go-binfmt.github.io/>
- Docs — <https://go-binfmt.github.io/docs/>
- Brand assets — <https://github.com/go-binfmt/brand>

---
<p align="center"><sub>Branding in <a href="https://github.com/go-binfmt/brand">go-binfmt/brand</a>. BSD-3-Clause.</sub></p>
