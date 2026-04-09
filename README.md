**Huffman Compression Engine**



This project is a complete C++ implementation of the Huffman Coding algorithm. It provides a full pipeline for compressing and decompressing text files by analyzing character frequency and generating an optimal prefix-based binary tree.



The system supports both encryption (compression) and decryption (reconstruction) using a persistent key file, ensuring data can be recovered across different program executions.

To view the UML, click this link https://usman-irshad1.github.io/Huffman-File-Compressor/

**Core Features**



* **Frequency Analysis**
* Dynamically calculates the occurrence of each character in the input file to determine optimal encoding weights.
* **Huffman Tree Construction**
* Builds a binary tree using a priority-based list, where characters with lower frequency are placed deeper, and frequent characters get shorter codes.
* **Full Formatting Support**
* Preserves spaces, special characters, and newline formatting, ensuring the decrypted output matches the original file exactly
* **Persistent Key Storage**
* Stores the generated Huffman codes in a key file, allowing reconstruction of the tree without needing the original input.
* **Tree Reconstruction**
* Rebuilds the Huffman tree from the saved key file using pointer-based traversal logic.
* **Memory Management**
* Implements recursive deletion of tree nodes to prevent memory leaks.



**How It Works**



**1. Input Processing**

The program reads the entire text file, including newline characters.



**2. Frequency Calculation**

Each character is counted and stored in a custom list structure.



**3. Tree Construction**

The two least frequent nodes are repeatedly combined to form a parent node until a single root remains.



**4. Encoding**

Each character is assigned a unique binary code based on its path in the tree:



Left → 0

Right → 1



**5. Key Generation**

The character-to-code mapping is saved in a file (Key\_for\_encryption.txt).



**6. Encryption**

The original text is converted into a string of 0s and 1s and stored in Encrypted\_file.txt.



**7. Reconstruction**

The tree is rebuilt from the key file using the stored codes.



**8. Decryption**

The encoded bitstream is traversed through the reconstructed tree to recover the original text, saved in Decrypted\_file.txt.



**Technical Implementation**



* Language
* C++



**Core Data Structures**



* Custom tree node (encryption)
* Inherited STL list as a priority structure
* Pointer-based binary tree



**Key Techniques**



1. Recursion (tree traversal, deletion, encoding)
2. File handling using ifstream and ofstream
3. Operator overloading (for frequency increment)
4. Custom sorting for priority handling



**Project Workflow** 



1. Read and encode original file
2. Build Huffman tree
3. Save key file
4. Rebuild tree from key
5. Save encrypted file
6. Decrypt file using rebuilt tree



**Current Limitations**



* Encoded data is stored as strings ("0" and "1") instead of actual bits
* This does not reduce physical file size significantly
* Uses list instead of a more efficient priority\_queue



**Future Improvements**



1. **Bit Packing**
Convert binary strings into actual bits for real compression and reduced file size.

2. **Performance Optimization**
Replace list-based priority handling with a priority\_queue (min-heap).

3. **User Interface**
Add a command-line menu for file selection and operation control.

4. **Error Handling**

&#x20;  Improve robustness for missing files and invalid inputs.

