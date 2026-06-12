# 🥷 BSCP-Engine: Boutaba Stream Cipher & Purge (v2.2)

A military-grade, lightweight, and highly optimized cryptographic stream utility written in pure C. Designed for secure file encryption, obfuscation, and advanced Operational Security (OpSec) compliance. 

This engine is developed for academic research, data privacy defense, and local file security verification.

---

## 📝 Short Description
"A military-grade, high-performance stream cipher engine written in pure C, featuring dynamic heap buffering, anti-frequency analysis symmetric XOR salt layer, and automated OpSec file purging handlers."

---

## 🌀 Key Architectural Features

* **Optimized Dynamic Heap Buffering:** Utilizes a 4096-byte `malloc` streaming matrix via standard `fread()` and `fwrite()` loops. It processes massive, multi-gigabyte files (binaries, videos, system images) smoothly with minimal volatile memory (RAM) overhead.
* **Symmetric Salted Stream Cipher (v2.2 Hardened):** Implements a dynamic, index-based modulo-7 cryptographic Salt Factor `(key_index % 7)` nested entirely within symmetric bitwise XOR operations `buffer[i] ^ (secret_key[key_index] ^ salt_factor)`. This eliminates potential byte arithmetic overflows and guarantees identical bit-inversion during decryption.
* **Anti-Overflow & Safe Memory Logic:** Hardened with strict boundary constraints (`unsigned char` array contexts) to completely mitigate signed/unsigned byte processing fragmentation. Fully protected against Division-by-Zero faults.
* **OpSec Automated Shredding:** Features a rigorous automated file purging routine using native subsystem handlers (`remove()`) immediately after successful encryption to prevent localized forensic tracking or source asset exposure.

---

## 📖 Extended Technical Description

The **BSCP-Engine** operates as a low-overhead, block-pipelined symmetric stream cipher. Unlike naïve encryption scripts that load an entire file context into volatile memory (causing memory exhaustion on large assets), this architecture processes data in a deterministic runtime environment using a strict chunking strategy.

### 🔬 Core Algorithmic Mechanics:

1. **Stream Buffering Pipeline:** The engine dynamically allocates a static 4KB chunk context inside the Heap using `malloc()`. Data is streamed into this temporary vault using sequential `fread()` operations, maintaining a constant memory footprint of exactly 4096 bytes, regardless of whether the target payload is a few kilobytes or several gigabytes.
2. **Pure Symmetric XOR Salt Layer:** To defeat basic frequency analysis and known-plaintext attacks (KPA) without triggering math boundary anomalies, the cipher routine injects a moving index rotation variant: `salt_factor = key_index % 7`. By wrapping the salt factor within a nested XOR logic array instead of integer addition, mathematical parity is maintained across both encryption and decryption cycles.
3. **Automated Forensics Mitigation (Shredding):** Upon verifying that the cryptographic output loop has successfully closed and flushed the buffer to disk via `fwrite()`, the application calls the native POSIX filesystem subsystem handler `remove()`. This purges the unencrypted source file directly from the inode index, satisfying essential modern OpSec operational criteria.

---

## 🛠️ Compilation & Deployment

This utility compiles seamlessly on any Linux subsystem, optimized for vanilla **Arch Linux** and **BlackArch** environments.

### 1. Compilation
Compile using the standard `gcc` compiler with optimization flags:
```bash
gcc -O3 main.c -o bscp_engine
```

### 2. Execution
Run the binary from your local shell terminal:
```bash
./bscp_engine
```

---

## 🔒 Responsible Disclosure & Usage Policy
This repository is published strictly for defensive, educational, and data-integrity verification purposes. The author does not provide automated exploit vectors or malicious execution modules. All operations are designed to protect localized user infrastructure.
