# README

- [ ] 请确保您正在使用 _Mark Text_ 阅读此文件。使用除了在.RAR文件中包含的 _Mark Text_ 以外的其他Markdown查看器来查看可能会导致格式错误。

## 在移步至其他文件前，请先仔细阅读这个文件！

---

## 目录

1. 项目结构:(Casear-Cipher.rar)

2. 文件注释

3. 介绍

4. 与基本算法比较

5. 配置环境

6. 代码注释(Casear-Cipher.cpp)

---

## 项目结构:(Casear-Cipher.rar)

- README-En.md

- README-Ch.md

- Comment-With-$L^AT_EX$.md

- Mark-Text.exe

- New-Algorithms-to-Decode-the-Casear-Cipher.pptx

- Code
  
  - Casear-Cipher.cpp
  
  - Casear-Cipher.exe

---

## 文件注释

**加粗**的部分是文件名，其他的是注释。

- **README-En.md**
  
  英语版的README

- **README-Ch.md**
  
  中文版的README

- **Mark-Text.exe**
  
  Markdown 文件查看器

- **New-Algorithms-to-Decode-the-Casear-Cipher.pptx**
  
  这个项目的核心文件
  
  包含了所有关于这两个算法的内容

- **Comment-With-$L^AT_EX$**.md
  
  使用$L^AT_EX$的注释

- **Code**
  
  代码文件夹
  
  - **Casear-Cipher.cpp**
    
    基础算法
  
  - **Casear-Cipher.exe**
    
    **Casear-Cipher.cpp** 的可执行文件

---

## 介绍

在这个项目中，我们提出了以下的两个新的算法来解码 _凯撒密码_。

1. 在一段给定的文字中使用基础的计数器来统计每个字母的出现频率，并将其与被解码后的字母一一对应。

2. 使用 _权值更新_ 算法 来更新给定词库里的每一个单词的权值。

普通算法:

代码:(cpp)

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
//这段代码在2022/6/10使用Win10和TDM-GCC 4.9.2 64-bit Release编译通过。
```

---

## 与基本算法比较

| **时间**  | #1     | #2     | #3     | #4   | #5   | #6   | All     |
| ------- | ------ | ------ | ------ | ---- | ---- | ---- | ------- |
| **基础**  | 5422.5 | 5282.5 | 7552.5 | 6185 | 5345 | 5795 | 35582.5 |
| **第一个** | 365    | 454    | 548    | 523  | 322  | 862  | 3074    |
| **第二个** | None   | None   | None   | None | None | None | None    |

---

## 配置环境

**编译器**：TDM-GCC 4.9.2 64-bit Release

**操作系统**:Windows 10 企业版,版本17134.2026

**处理器**:Intel Core i5-7300U CPU @ 2.60GHZ 2.71GHZ

**编辑器**:Red-Panda-Cpp

---

## 代码注释(Casear-Cipher.cpp)

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
//plain_text:要解密/加密的字符串
//mode      :区分解密/加密模式
//STEP      :偏移量
{
    if (STEP >= 26) STEP %= 26;
    string cipher = "";
    for (int i = 0; i < plain_text.size(); i++) {
        if (plain_text[i] >= 48 && plain_text[i] <= 57) {
            cipher.push_back (plain_text[i]);
        } else if (plain_text[i] >= 65 && plain_text[i] <= 90) {
            cipher.push_back ( (char) (65 + (plain_text[i] + mode * STEP - 65) % 26));
            //(1)
        } else {
            cipher.push_back ( (char) (97 + (plain_text[i] + mode * STEP - 97) % 26));
            //(2)
        }
    }
    return cipher;
}
string ceaser_encoding (string plain, int STEP)
//加密
{
    return ceaser (plain, ENCODE, STEP);
}
string ceaser_decoding (string plain, int STEP)
//解密
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
