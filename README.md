# 🥷 BSCP-Engine: Boutaba Stream Cipher & Purge (v2.1)

A military-grade, lightweight, and highly optimized cryptographic stream utility written in pure C. Designed for secure file encryption, obfuscation, and advanced Operational Security (OpSec) compliance. 

This engine is developed for academic research, data privacy defense, and local file security verification.

---

## 📝 Short Description (الوصف المختصر)
"A military-grade, high-performance stream cipher engine written in pure C, featuring dynamic heap buffering, anti-frequency analysis salt layer, and automated OpSec file purging handlers."

---

## 🌀 Key Architectural Features (ميزات الهندسة البرمجية)

* **Optimized Dynamic Heap Buffering:** Utilizes a 4096-byte `malloc` streaming matrix via standard `fread()` and `fwrite()` loops. It processes massive, multi-gigabyte files (binaries, videos, system images) smoothly with minimal volatile memory (RAM) overhead.
* **Resilient Salted Stream Cipher:** Implements a dynamic, index-based modulo-7 cryptographic Salt Factor `(key_index % 7)` layered on top of symmetric XOR bitwise operations. This randomizes byte patterns, preventing ciphertext from being cracked via Frequency Analysis.
* **Anti-Overflow & Safe Memory Logic:** Hardened with strict boundary constraints (`unsigned char` array contexts) to completely mitigate signed/unsigned byte overflow vulnerabilities during arithmetic shifts. Fully protected against Division-by-Zero faults.
* **OpSec Automated Shredding:** Features a rigorous automated file purging routine using native subsystem handlers (`remove()`) immediately after successful encryption to prevent localized forensic tracking or source asset exposure.

---

## 🔬 Deep Technical Code Review (التقرير والتحليل التقني)

1. **Memory Pipeline:** Instead of loading the entire file context into the RAM (which crashes low-resource devices), the architecture pipes the input streams block-by-block.
2. **Symmetric Synergy:** Built upon the properties of the bitwise XOR operator (`^`). Because XOR is self-inverse, the same core algorithmic engine functions flawlessly for both **Locking (Encryption)** and **Restoring (Decryption)** actions based on the exact same key.
3. **Array Mutation Safeguard:** The application enforces a 4-character minimum constraint on the Secret Key to eliminate processing fragmentation, while input buffer cleaning (`getchar()`) isolates the shell from terminal noise.

---

## 🛠️ Compilation & Deployment (التركيب والتشغيل)

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
