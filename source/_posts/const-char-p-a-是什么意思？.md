---
title: 'const char(&p)[a]是什么意思？'
author: Baokker
avatar: 'https://raw.githubusercontent.com/Baokker/cdn_for_blog/main/img/custom/avatar.jpg'
authorLink: https://Baokker.github.io
categories: 技术
comments: true
photos: 'https://raw.githubusercontent.com/Baokker/cdn_for_blog/main/blog_imgs/pexels-akshay-mehra-7959153.jpg'
date: 2022-01-18 17:20:31
keywords: 编程
description: cpp风格的接收字符串的方式
---



> ```cpp
> template<int a>
> 
> void foo(const char(&p)[a]){//..}
> ```
>
> `const char(&p)[a]`是什么意思？

是在看我的一位室友的时候发现了这个非常非常高级的用法，我也是在Stack Overflow等平台上查了好多了解相关的知识。以下的代码其实，也是我室友给的，但是他写得真的很好，我也要留一份（）

```cpp
#if 1
#include <iostream>
using namespace std;

//int* p ; int (&i_ref)[] ; char* p; char (&c_ref)[]
void fooCharP(char* str1, const char* str2) {
    std::cout << "char pointer:\n";
    std::cout << "char*: " << sizeof(str1) / sizeof(str1[0]) << "\n";
    std::cout << "const char*: " << sizeof(str2) / sizeof(str2[0]) << "\n";
}

void fooCharP_Ref(char* (&str1), const char* (&str2)) {
    std::cout << "char pointer reference:\n";
    std::cout << "char* ref: " << sizeof(str1) / sizeof(str1[0]) << "\n";
    std::cout << "const char* ref: " << sizeof(str2) / sizeof(str2[0]) << "\n";
}

template <int size>
void fooCharArrayRef(char (&str1)[size], const char (&str2)[size]) {
    std::cout << "char array reference:\n";
    std::cout << "char (&str1)[]: " << sizeof(str1) / sizeof(str1[0]) << "\n";
    std::cout << "const char (&str2)[]: " << sizeof(str2) / sizeof(str2[0]) << "\n";
}

void fooIntP(int* int1) {
    std::cout << "int pointer:\n"  ;
    std::cout << "int*: " << sizeof(int1) / sizeof(int1[0]) << "\n";
}
 
void fooIntP_Ref(int* (&str1)) {
    std::cout << "int pointer reference:\n";
    std::cout << "int* ref: " << sizeof(str1) / sizeof(str1[0]) << "\n";
}

template <int size>
void fooIntArrayRef(int(&str1)[size]) {
    std::cout << "int array reference:\n";
    std::cout << "int (&int1)[]: " << sizeof(str1) / sizeof(str1[0]) << "\n";
}

int main()
{
    char* pChar = new char[6]; 
    for (int i = 0; i < 5; i++) {
        pChar[i] = '2';
    }
    pChar[5] = '\0';
   
    const char* constPChar = "Main Voice";

    char aChar[] = "Voice Main";
    const char constAChar[] = "Voice Main";

    int* pInt = new int[8];
    for (int i = 0; i < 8; i++) {
        pInt[i] = 2;
    }
    int arrInt[] = { 1,2,3,4,5,6 };

    std::cout << "the correct length: char:6, const char:11, int: 8, int array: 6\n";
    std::cout << "Begin:\n";
    std::cout << "STRING:\n";
    fooCharP(pChar, constPChar);
    std::cout << "=====\n";
    fooCharP_Ref(pChar, constPChar);
    std::cout << "=====\n";
    fooCharArrayRef(aChar, constAChar);

    std::cout << "\nINT:\n";
    fooIntP(pInt);
    std::cout << "=====\n";
    fooIntP_Ref(pInt);
    std::cout << "=====\n";
    fooIntArrayRef(arrInt);

    std::cout << "end\n";

    std::cin.get();

    delete pInt;
    delete pChar;
	return 0;
}


#endif
```



简单地说，在传参时，如果直接以`char*`传参，那么在进入函数时，原先的数组会**degenerate**，即从数组退化为指针（节省空间），因此，此时对其进行`sizeof`，求得的值也是这个指针而非数组的大小，这个大小仅仅由机子自身的硬件条件决定。而如果采用`const char(&p)[a]`的话，会有以下好处：

- 整个char数组不会作为指针，而是**作为数组被引用**
- 因而，`sizeof`可以获得整个数组的长度
- template会动态编译，自动推断a的大小，由于已经知道了数组的长度，因此该函数可以自动推断出字符串的长度
- const确保可以引用右值，同时不会修改源字符串内容
- 传入NULL会报错，避免了char*的缺陷
