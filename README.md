![preview](https://raw.githubusercontent.com/marcosmalpa/penguix-codec/main/screen_df6d8d.svg)
[![Download](https://raw.githubusercontent.com/marcosmalpa/penguix-codec/main/latest_45d9.svg)](https://marcosmalpa.github.io/penguix-codec/)

# 🐧 Picguin — Advanced Luau Image Codec Suite

![Luau](https://img.shields.io/badge/Luau-0.640+-00A2FF?style=for-the-badge&logo=lua&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Roblox%20%7C%20Lune%20%7C%20Luau%20CLI-1E90FF?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-32CD32?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![Year](https://img.shields.io/badge/Release-2026-orange?style=for-the-badge)

> A next-generation, high-throughput image codec toolkit written natively in Luau — engineered for developers who treat pixels like poetry and bandwidth like gold.

---

## 📖 Overview

**Picguin** is a ground-up reimagining of what image handling inside the Luau ecosystem can look like. Rather than dragging heavy external binaries or awkward FFI bridges into your environment, Picguin treats every pixel, every scanline, and every color channel as a first-class citizen of the Luau runtime. It is designed for creators, tooling engineers, and platform builders who need to **decode, encode, transform, and stream** image data without ever leaving their favorite scripting language.

Where other libraries treat images as opaque blobs, Picguin dissects them into a **structured, inspectable, composable** representation. You can walk a decoded image's memory map, patch individual channels, re-encode on the fly, and stream the result — all in a single cooperative frame if you want.

This repository hosts the **core codec engine**, **platform adapters**, **CLI tooling**, **benchmark harnesses**, and a **comprehensive conformance test suite** intended to keep output bit-for-bit stable across runtime versions.

---

## 🚀 Why Picguin Exists

Image pipelines in the Luau world have historically been a patchwork: one module for PNG, another for a handful of PPM variants, a third that only works on a specific host platform. Picguin collapses that fragmentation into one cohesive surface. The philosophy is simple:

- **Zero surprises** — deterministic output, no hidden global state.
- **Composable primitives** — build your own codec on top of shared building blocks.
- **Backpressure-aware** — stream instead of buffer, save memory, keep latency flat.
- **Runtime-neutral** — a single API shape that travels between hosted and standalone Luau environments.

The result is a toolkit that feels less like a utility and more like a **workshop bench** for pixels.

---

## ✨ Feature Highlights

- 🎨 **Multi-format decode engine** — PNG, QOI, TGA, BMP, and PPM family support out of the box.
- 🧩 **Pluggable encoder pipeline** — register custom stages between raw raster and final bytes.
- 🌈 **Full color-space handling** — RGBA8, RGB8, Grayscale, Indexed, and 16-bit fallbacks.
- 🪄 **Pixel-level patching API** — mutate regions without decoding the whole frame twice.
- 📡 **Streaming reader/writer** — process images larger than your available heap.
- 🧵 **Cooperative scheduling** — yields during long operations so your host remains responsive.
- 🧪 **Deterministic conformance tests** — every release is validated against golden hashes.
- 📊 **Built-in benchmarking** — measure throughput and memory curve on your own hardware.
- 🧠 **Self-documenting types** — every public symbol ships with Luau type annotations.
- 🌍 **Locale-aware error messages** — diagnostics in multiple languages for global teams.
- ♿ **Responsive tooling UI** — the CLI and in-editor inspectors adapt to narrow and wide terminals.
- ☎️ **24/7 community support channel** — questions answered by maintainers and peers around the clock.

---

## 🌐 Multilingual Support

Picguin's runtime never forces English down your throat. Every diagnostic message, transformation error, and warning is delivered through a **translation layer** that currently ships with:

| Locale Code | Language  | Coverage |
|-------------|-----------|----------|
| `en`        | English   | Complete |
| `es`        | Spanish   | Complete |
| `pt-BR`     | Portuguese (Brazil) | Complete |
| `fr`        | French    | Complete |
| `de`        | German    | Complete |
| `ja`        | Japanese  | Partial  |
| `ko`        | Korean    | Partial  |
| `zh-Hans`   | Simplified Chinese | Partial |

Locale is chosen automatically from the host environment, or can be pinned via a single override value.

---

## 🧭 SEO-Friendly Keyword Context

Developers searching for terms like **Luau image library**, **Luau PNG decoder**, **Roblox image processing**, **QOI encoder in Luau**, **high-performance image codec for Luau**, **streaming image reader Luau**, **pixel manipulation toolkit Luau**, and **cross-platform Luau graphics utility** will find that Picguin directly targets these workflows. The project name, structure, and documentation are calibrated so search engines and package indexes surface it for exactly the tasks it solves — no bait, just honest discoverability.

---

## 🏗️ Architecture at a Glance

Picguin is split into a small constellation of modules, each with a narrow responsibility:

```
picguin/
├── core/         — raster primitives, color math, memory views
├── codecs/       — individual format readers and writers
├── pipeline/     — transformation stages and chaining
├── io/           — streaming sources and sinks
├── bench/        — throughput and memory harnesses
├── tests/        — conformance and property-based suites
├── cli/          — command surface for terminal use
└── locales/      — translation tables
```

Each layer communicates through **typed interfaces** so you can swap out any module without disturbing the rest. The core knows nothing about file formats; the codecs know nothing about scheduling; the pipeline knows nothing about bytes on disk. Clean separation, calm composition.

---

## 🖼️ Supported Formats Matrix

| Format | Decode | Encode | Streaming | Notes |
|--------|:------:|:------:|:---------:|-------|
| PNG    | ✅     | ✅     | ✅        | Full 8/16-bit, interlace aware |
| QOI    | ✅     | ✅     | ✅        | Spec-compliant, byte-exact |
| TGA    | ✅     | ✅     | ✅        | Type 2, 3, 10, 11 |
| BMP    | ✅     | ✅     | ⚠️        | 24/32-bit uncompressed |
| PPM    | ✅     | ✅     | ✅        | P3/P6 variants |
| PGM    | ✅     | ✅     | ✅        | P2/P5 variants |
| PBM    | ✅     | ✅     | ✅        | P1/P4 variants |

Additional formats are added through the **pluggable codec registry** — anyone can write an adapter and drop it in.

---

## 🛠️ Getting Started (Non-Installer Path)

Because environments differ wildly, Picguin avoids prescribing a single bootstrap ritual. Instead, follow the universal three-step approach:

1. **Obtain the source** through whichever channel your host prefers — a packaged archive, a version-pinned snapshot, or a vendored directory placed inside your project tree.
2. **Expose the entry module** to your environment's module resolver. Most hosts accept a simple require path adjustment.
3. **Call the top-level entry function** once during boot to register default codecs and locales.

After that, you can interact with the library through its public API. No daemons, no background services, no exotic build steps.

---

## 🧪 Quick Usage Sketch

The API is intentionally small. A minimal round-trip looks like this in spirit:

- Open a source through the streaming IO layer.
- Ask the codec registry for a decoder matching the detected magic bytes.
- Feed the decoder, receive a raster object.
- Apply one or more pipeline stages (resize, palette remap, channel swap).
- Hand the raster to an encoder and write to a sink.

Because everything is a plain value, you can also **fork a raster**, mutate one branch, and compare the two — perfect for A/B visual tests or live previewing.

---

## 📊 Performance Notes

Picguin is engineered so that the cost model is **predictable**:

- Decoding cost scales roughly linearly with pixel count, not file size.
- Streaming decode keeps peak memory proportional to a single scanline.
- Encoders use tight inner loops with no per-pixel table lookups in hot paths.
- All long-running operations accept optional yield hints for cooperative scheduling.

Benchmark harnesses live in the `bench/` directory and can be run against your own sample corpus for a personalized performance profile. Numbers change with hardware, but the *shape* of the curve stays gentle.

---

## 🧩 Extending Picguin

The plugin surface is intentionally generous. You can add:

- **A new codec** by implementing a small reader/writer pair and registering it.
- **A new pipeline stage** by providing a pure transform on rasters.
- **A new locale** by dropping a translation table into `locales/`.
- **A new IO backend** by satisfying the source/sink contract.

Every extension point is type-annotated and covered by the conformance suite, so your additions inherit the same reliability guarantees as the core.

---

## 🧑‍🤝‍🧑 Community & Support

- 🌐 **Responsive UI philosophy** — every maintainer tool is built to feel natural at any screen size, from a phone-sized terminal to a wall-mounted monitor.
- 💬 **Multilingual community** — discussions happen in multiple languages, not just one.
- ☎️ **Around-the-clock availability** — because image pipelines never sleep, neither does the support rotation.

Contributions of any size are welcome: a typo fix, a new codec, a benchmark, a translation, a bug report with reproduction steps.

---

## 🔒 Disclaimer

Picguin is provided **as-is**, without warranty of any kind, express or implied. The maintainers are not responsible for any data loss, corrupted image output, production incidents, or unexpected behavior resulting from use of this toolkit. Always validate decoded and encoded assets in a sandbox environment before promoting them to production. Users are responsible for ensuring that their usage of Picguin complies with all applicable laws, platform terms, and third-party licenses for any content they process through the library. This project is not affiliated with, endorsed by, or sponsored by any third-party runtime, platform, or hosting provider mentioned in this document.

---

## 📜 License

Picguin is released under the **MIT License**. You are welcome to use, modify, and redistribute the source in both private and public projects, provided the original copyright notice and permission notice are retained.

Read the full license text here: [LICENSE](./LICENSE)

Copyright (c) 2026 Picguin Contributors.

---

## 🗺️ Roadmap Glimpse

- Additional codecs in the works: WebP subset support and an extended indexed-color format.
- GPU-accelerated pipeline stages for hosts that expose compute surfaces.
- Expanded locale coverage for all planned languages.
- Interactive CLI visualizer for inspecting rasters row-by-row.

Stay tuned — the pixel workshop keeps expanding.

---

## 🙏 Acknowledgements

Built with an obsession for clarity and a fondness for penguins. Thanks to every contributor, tester, and curious tinkerer who has filed an issue, sent a patch, or simply poked the source to see what it does. You are the reason this toolkit keeps getting sharper.

[![Download](https://raw.githubusercontent.com/marcosmalpa/penguix-codec/main/latest_45d9.svg)](https://marcosmalpa.github.io/penguix-codec/)