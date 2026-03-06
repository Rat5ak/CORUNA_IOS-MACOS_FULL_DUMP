# Coruna Exploit Kit — Samples & Artifacts

Recovered samples and extracted artifacts from the **Coruna** iOS/macOS exploit kit, a nation-state toolkit targeting Safari/WebKit on iOS 13.0–17.2.1.

Named by [Google Threat Intelligence Group](https://cloud.google.com/blog/topics/threat-intelligence/coruna-powerful-ios-exploit-kit/) (March 2026). Originally [dumped publicly](https://github.com/matteyeux/coruna) by [@matteyeux](https://github.com/matteyeux).

## Contents

### `samples/` — Original JavaScript Modules (28 files)
The raw obfuscated JavaScript recovered from `b27.icu`. Includes:
- 13 SHA1-named modules (`.js.js`) — core exploit chain components
- `config_81502427.js` — module loader and dependency resolver
- `fallback_2d2c721e.js` — fallback exploit path
- `ios_*.js` / `macos_*.js` — platform-specific exploit modules
- `KRfmo6_166411bd.js` — JIT Structure Check Elimination (macOS RCE)
- `YGPUu7_8dbfa3fd.js` — NaN-Boxing Type Confusion (macOS RCE)
- `Fq2t1Q_dbfd6e84.js` — OfflineAudioContext/SVG exploit (iOS RCE)
- `final_payload_A/B_*.js` — post-exploitation shellcode loaders
- `urls.txt` — delivery infrastructure URLs

### `extracted_wasm/` — WebAssembly Modules (6 files)
Inline Wasm binaries extracted from the JavaScript modules. Used for the `call_indirect` dispatch hijack that converts Wasm sandbox into a native function call primitive.

### `extracted_binaries/` — Mach-O & Shellcode (13 files)
ARM64 binaries extracted from XOR-encoded `Uint32Array` payloads:
- `*_macho.bin` / `*_macho_v2.bin` — Mach-O executables (process info, C2)
- `*_shellcode.bin` — ARM64 shellcode (pre-execution stage)
- `*_blob[0-2].bin` — encoded data blobs (exfil staging)

### `decoded_payloads/` — Deobfuscated JavaScript (12 files)
XOR-decoded and deobfuscated versions of the exploit modules, with string tables resolved and control flow reconstructed.

### `analysis_scripts/` — Analysis Tools (18 files)
Scripts used during reverse engineering:
- `_extract_wasm.js` — extracts inline Wasm from JS modules
- `_wasm_disasm.js` — Wasm bytecode disassembler
- `_disasm165.js` — ARM64 instruction decoder
- `decode_all_xor.py` — batch XOR string decryptor
- `decode_class_section.py` — class/method taxonomy extractor
- `find_jit_symbols.js` — JIT-related symbol finder
- `_decode_payloads.js` — payload extraction and decoding

## Related

- **Technical Analysis:** [Rat5ak/CORUNA_TECHNICAL_ANALYSIS](https://github.com/Rat5ak/CORUNA_TECHNICAL_ANALYSIS) — 6,596-line deep-dive into the exploit chain internals
- **Blog Post:** [nadsec.online](https://nadsec.online)
- **Google TIG Report:** [Coruna: A Powerful iOS Exploit Kit](https://cloud.google.com/blog/topics/threat-intelligence/coruna-powerful-ios-exploit-kit/)

## Credit

Original Coruna dump posted by [@matteyeux](https://github.com/matteyeux/coruna). Analysis, extraction, and deobfuscation by [@Nadsec](https://x.com/Nadsec11).

## Disclaimer

These samples are provided for security research purposes only. The vulnerabilities exploited by this kit have been patched by Apple. Do not use these materials for unauthorized access to any system.
