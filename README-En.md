# README

- [ ] Make sure you are reading this file with _Mark Text_ . Using other Markdown viewer instead of *Mark Text* given in the .RAR file may cause a style failure.

## Please read this carefully before you move on to other files!

---

## Content of this file

1. Structure:(Casear-Cipher.rar)

2. Comment of the files

3. Introduction

4. Compare with ordinary algorithm

5. Comment of the cpp code(Casear-Cipher.cpp)

---

## Structure:(Casear-Cipher.rar)

- README-En.md

- README-Ch.md

- Mark-Text.exe

- New-Algorithms-to-Decode-the-Casear-Cipher.pptx

- Comment-With-$L^AT_EX$.md

- Code
  
  - Casear-Cipher.cpp
  
  - Casear-Cipher.exe

---

## Comment of the files

The **Bolded** part is the file name,and the normal part is the comment.

- **README-En.md**
  
  The English version of this README

- **README-Ch.md**
  
  The Chinese version of this README

- **Mark-Text.exe**
  
  Markdown viewer

- **New-Algorithms-to-Decode-the-Casear-Cipher.pptx**
  
  The main work of this project
  
  It included everything of the two algorithms.

- **Comment-With-$L^AT_EX$.md**
  
  The comment with $L^AT_EX$

- **Code**
  
  The folder of the cpp code
  
  - **Casear-Cipher.cpp**
    
    The ordinary algorithm
  
  - **Casear-Cipher.exe**
    
    The executeable application of **Casear-Cipher.cpp**

---

## Introduction

This is a project in which two of the new algorithm to decode the _Casear Cipher_ are published below.

1. Use the basic counter of every single letter to decide which is the right letter of the decoded text by the frequency of the letters appearing in a given text.

2. Use the _Weight Updating_ algorithm to update the value of every word in the given list.

The ordinary alogorithm: 

Code:(cpp)

```cpp
string ceaser (string plain_text, int mode, int STEP)
{
    if (STEP >= 26) STEP %= 26;
    string cipher = "";
    for (int i = 0; i < plain_text.size(); i++) {
        if (plain_text[i] >= 48 && plain_text[i] <= 57) {
            cipher.push_back (plain_text[i]);
        } else if (plain_text[i] >= 65 && plain_text[i] <= 90) {
            cipher.push_back ( (char) (65 + (plain_text[i] + mode * STEP - 65) % 26));
        } else {
            cipher.push_back ( (char) (97 + (plain_text[i] + mode * STEP - 97) % 26));
        }
    }
    return cipher;
}
//This code is previously compiled on 2022/6/10 under Win10 and TDM-GCC 4.9.2 64-bit Release.
```

---

## Compare with ordinary algorithm

| Time         | #1     | #2     | #3     | #4   | #5   | #6   | All     |
| ------------ | ------ | ------ | ------ | ---- | ---- | ---- | ------- |
| **Ordinary** | 5422.5 | 5282.5 | 7552.5 | 6185 | 5345 | 5795 | 35582.5 |
| **First**    | 365    | 454    | 548    | 523  | 322  | 862  | 3074    |
| **Second**   | None   | None   | None   | None | None | None | None    |

---

## IDE environment

**Compiler**：TDM-GCC 4.9.2 64-bit Release

**OS version**:Windows 10,Version17134.2026

**Processor**:Intel Core i5-7300U CPU @ 2.60GHZ 2.71GHZ

---

## Comment of the cpp code(Casear-Cipher.cpp)

```cpp
#include<iostream>
#include<string>
using namespace std;
enum MODE
{
    ENCODE = 1,
    DECODE = -1
};
string ceaser (string plain_text, int mode, int STEP)
//plain_text:The string you want to decode/encode
//mode      :The integer to differ decode/encode
//STEP      :The integer of deviation
{
    if (STEP >= 26) STEP %= 26;
    string cipher = "";
    for (int i = 0; i < plain_text.size(); i++) {
        if (plain_text[i] >= 48 && plain_text[i] <= 57) {
            cipher.push_back (plain_text[i]);
        } else if (plain_text[i] >= 65 && plain_text[i] <= 90) {
            cipher.push_back ( (char) (65 + (plain_text[i] + mode * STEP - 65) % 26));
        } else {
            cipher.push_back ( (char) (97 + (plain_text[i] + mode * STEP - 97) % 26));
        }
    }
    return cipher;
}
string ceaser_encoding (string plain, int STEP)
//encode
{
    return ceaser (plain, ENCODE, STEP);
}
string ceaser_decoding (string plain, int STEP)
//decode
{
    return ceaser (plain, DECODE, STEP);
}
int main()
{
    string cipher;
    int n=1;
    //getline (cin, cipher);
    cipher="helloworld";
    string res = ceaser_encoding (cipher, n);
    cout << "密文：" << res << endl;
    cout << "明文：" << ceaser_decoding (res, n) << endl;
    return 0;
}
```
