# Educational Huffman Coding & Tree Reconstruction Demo (C++)

[![Language: C++17](https://img.shields.io/badge/Language-C%2B%2B17-blue?style=flat-square)]()
[![Docs: Doxygen](https://img.shields.io/badge/Docs-Doxygen%20Live-2ea44f?style=flat-square)](https://usman-irshad1.github.io/Huffman-File-Compressor/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

An educational C++ implementation of **Huffman Coding** (lossless prefix-code data representation) demonstrating character frequency analysis, priority-list binary tree construction, persistent code-table serialization, and exact text reconstruction.

> **Important Technical Scope Note:**  
> 1. **Bitstring Representation vs. Bit-Packed Binary Compression:** To make the prefix codes easy to inspect in plain text, this educational implementation writes the encoded output to [`Encrypted_file.txt`](Encrypted_file.txt) as human-readable ASCII `'0'` and `'1'` characters rather than packing 8 bits into each binary byte (`uint8_t`). Consequently, it demonstrates the **Huffman tree construction and prefix-decoding algorithms**, not physical disk-space reduction.  
> 2. **Terminology Note (`encryption` / `Encrypted_file.txt`):** Several struct and filenames in the source code (`struct encryption`, `Key_for_encryption.txt`, `Encrypted_file.txt`, `Decrypted_file.txt`) use the word *"encryption"* colloquially from the original coursework prompt. Mathematically, **Huffman coding is a lossless entropy encoding (compression) algorithm, not cryptographic encryption.**

- **Live UML & Class Documentation**: [Doxygen Documentation](https://usman-irshad1.github.io/Huffman-File-Compressor/)

---

## Core Algorithmic Workflow

1. **Character Frequency Analysis**: Scans [`OriginalFile.txt`](OriginalFile.txt) (preserving spaces, punctuation, and newline characters) and counts character frequencies in a sorted `priority_list`.
2. **Huffman Binary Tree Construction**: Repeatedly merges the two lowest-frequency nodes into a parent node (`freq = left->freq + right->freq`) until a single root remains, assigning shorter prefix paths to frequent characters.
3. **Prefix Code Table Generation (`Key_for_encryption.txt`)**: Traverses the binary tree (`Left -> '0'`, `Right -> '1'`) and serializes the character-to-bitstring mapping to [`Key_for_encryption.txt`](Key_for_encryption.txt).
4. **Encoding (`Encrypted_file.txt`)**: Maps each character of `OriginalFile.txt` to its variable-length prefix code string in [`Encrypted_file.txt`](Encrypted_file.txt).
5. **Tree Reconstruction & Decoding (`Decrypted_file.txt`)**: Rebuilds the Huffman tree purely from the serialized prefix table (`Key_for_encryption.txt`) and traverses the bitstring to losslessly recover [`Decrypted_file.txt`](Decrypted_file.txt).

---

## Repository File Structure

```text
Huffman-File-Compressor/
├── HUFFMAN_Encoding_1.cpp          # Complete Huffman tree, encoding, and decoding implementation
├── HUFFMAN_Encoding_1.slnx         # Visual Studio 2022 solution file
├── HUFFMAN_Encoding_1.vcxproj      # Visual Studio C++ project file
├── OriginalFile.txt                # Sample input text file to encode
├── Key_for_encryption.txt          # Generated character-to-prefix-code lookup table
├── Encrypted_file.txt              # Generated ASCII '0'/'1' bitstring representation
├── Decrypted_file.txt              # Reconstructed output text file (matches OriginalFile.txt)
├── docs/                           # Generated Doxygen HTML & UML class diagrams
└── LICENSE                         # MIT License
```

---

## Prerequisites & Build / Run Instructions

### Option 1: Command-Line Compilation (`g++` / `clang++` / `cl`)
The project uses only the C++ Standard Library (`<iostream>`, `<fstream>`, `<string>`, `<list>`) with zero external dependencies:

```bash
# 1. Clone the repository
git clone https://github.com/usman-irshad1/Huffman-File-Compressor.git
cd Huffman-File-Compressor

# 2. Compile with C++17
g++ -std=c++17 -O2 HUFFMAN_Encoding_1.cpp -o huffman_demo

# 3. Run (reads OriginalFile.txt and generates Key_for_encryption.txt, Encrypted_file.txt, and Decrypted_file.txt)
./huffman_demo

# 4. Verify lossless reconstruction against the original input
diff -s OriginalFile.txt Decrypted_file.txt
```

### Option 2: Visual Studio 2022 (Windows)
1. Open `HUFFMAN_Encoding_1.slnx` (or `HUFFMAN_Encoding_1.vcxproj`) in **Visual Studio 2022**.
2. Select **`Release | x64`** (or `Debug | x64`) and press **`Ctrl + F5`** to build and execute.

---

## Roadmap for True Binary Compression

- **Bit-Packing I/O Buffer**: Pack 8 ASCII `'0'`/`'1'` decisions into single bytes (`std::bitset<8>` / bitwise shift buffer with padding header) to achieve physical file-size reduction ($\approx 40\text{--}55\%$ on English text).
- **Min-Heap Priority Queue**: Replace the `std::list`-based `priority_list` with `std::priority_queue` for $O(K \log K)$ tree construction over alphabet size $K$.

---

## License

This project is licensed under the [MIT License](LICENSE).
