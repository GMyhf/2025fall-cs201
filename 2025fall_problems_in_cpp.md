#  Problems in OJ, CF & others

*Updated 2025-11-01 17:50 GMT+8*
 *Compiled by Hongfei Yan (2025 Fall)*



> Logs:
>
> 2025/10/15: 加了些 数算、计概 【张梓康 元培】、【潘彦璋 物院】、【李沁遥25医学预科办】、【王乾旭 信科】、【刘思哲 25工学院】、【张真铭25元陪】、【李傲挺 物院】、【李沁遥25医学预科】、【罗锐，25工学院，】、【海博治 城市与环境学院】同学的CPP代码。
>
> 鉴于每学期都有同学偏好C++编程，本学期除维护Python题解外，也开始提供C++题解支持。



# Easy

## E01003: Hangover

math, http://cs101.openjudge.cn/pctbook/E01003/

How far can you make a stack of cards overhang a table? If you have one card, you can create a maximum overhang of half a card length. (We're assuming that the cards must be perpendicular to the table.) With two cards you can make the top card overhang the bottom one by half a card length, and the bottom one overhang the table by a third of a card length, for a total maximum overhang of 1/2 `+` 1/3 `=` 5/6 card lengths. In general you can make *n* cards overhang by 1/2 `+`1/3 `+` 1/4 `+` ... `+` 1/(*n* `+` 1) card lengths, where the top card overhangs the second by 1/2, the second overhangs tha third by 1/3, the third overhangs the fourth by 1/4, etc., and the bottom card overhangs the table by 1/(*n* `+` 1). This is illustrated in the figure below.

![img](http://media.openjudge.cn/images/1003/hangover.jpg)

**输入**

The input consists of one or more test cases, followed by a line containing the number 0.00 that signals the end of the input. Each test case is a single line containing a positive floating-point number c whose value is at least 0.01 and at most 5.20; c will contain exactly three digits.

**输出**

For each test case, output the minimum number of cards necessary to achieve an overhang of at least c card lengths. Use the exact output format shown in the examples.

样例输入

```
1.00
3.71
0.04
5.19
0.00
```

样例输出

```
3 card(s)
61 card(s)
1 card(s)
273 card(s)
```

来源

Mid-Central USA 2001



这个问题要求我们找到最少的卡片数，使得它们的叠加悬空距离至少为给定的 `c` 值。

**思路分析**：

每增加一张卡片，叠加的总过hang值是一个调和数列的部分和：

- 第 1 张卡片过hang `1/2` 长度。
- 第 2 张卡片过hang `1/3` 长度。
- 第 3 张卡片过hang `1/4` 长度。
- 依此类推。

所以，当卡片数量为 `n` 时，叠加的总过hang值为：

`Hn=1/2+1/3+1/4+⋯+1/n+1`

我们需要找到最小的 `n`，使得：

`Hn ≥ c`

这就变成了一个计算调和数列部分和的问题。



```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    double c;
    while (cin >> c) {
        if (c == 0.00) {
            break;
        }
        
        double overhang = 0.0;
        int cards = 0;

        // 增加卡片，直到总过hang值大于等于c
        while (overhang < c) {
            cards++;
            overhang += 1.0 / (cards + 1);  // 每张卡片的过hang值
        }

        // 输出结果，卡片数量
        cout << cards << " card(s)" << endl;
    }

    return 0;
}
```

> `<iomanip>` 是 C++ 标准库中的一个头文件，主要用于处理输入输出的格式化。它提供了一些控制输入输出格式的工具，例如设置数字的精度、宽度、对齐方式等。
>
> **常见的 `iomanip` 功能：**
>
> 1. **设置输出的精度（`setprecision`）**：
>    `setprecision` 用来指定浮点数输出的精度，即输出小数点后保留的位数。
>
>    ```cpp
>    #include <iostream>
>    #include <iomanip>
>    using namespace std;
>                                                                                                 
>    int main() {
>        double pi = 3.14159265358979;
>        cout << setprecision(5) << pi << endl; // 输出 3.1416
>        return 0;
>    }
>    ```
>
>    这个例子中，`setprecision(5)` 设置了输出精度为 5 位数字。
>
> 2. **固定小数点输出（`fixed`）**：
>    默认情况下，C++ 会根据数字的大小自动决定浮点数是以科学计数法（例如 `1.23e+4`）还是普通的十进制形式输出。如果你希望强制浮点数以小数点形式输出，可以使用 `fixed`。
>
>    ```cpp
>    #include <iostream>
>    #include <iomanip>
>    using namespace std;
>                                                                                                 
>    int main() {
>        double pi = 3.14159265358979;
>        cout << fixed << setprecision(4) << pi << endl; // 输出 3.1416
>        return 0;
>    }
>    ```
>
>    这段代码会强制 `pi` 以小数点形式输出，保留 4 位小数。
>
> 3. **设置输出宽度（`setw`）**：
>    `setw` 用来设置输出字段的宽度。如果输出的数据宽度小于 `setw` 设置的宽度，C++ 会自动填充空格来补齐。
>
>    ```cpp
>    #include <iostream>
>    #include <iomanip>
>    using namespace std;
>                                                                                                 
>    int main() {
>        int x = 42;
>        cout << setw(5) << x << endl;  // 输出 "   42"（宽度为5）
>        return 0;
>    }
>    ```
>
> 4. **对齐设置（`left`, `right`, `internal`）**：
>    通过 `left`, `right`, 和 `internal` 来控制输出对齐方式：
>
>    - `left`：左对齐
>    - `right`：右对齐（默认）
>    - `internal`：将符号位（正负号）对齐到输出字段的内部（即数字右侧，符号前）
>
>    ```cpp
>    #include <iostream>
>    #include <iomanip>
>    using namespace std;
>                                                                                                 
>    int main() {
>        cout << left << setw(10) << "Hello" << endl;  // 输出 "Hello     "
>        cout << right << setw(10) << "Hello" << endl; // 输出 "     Hello"
>        return 0;
>    }
>    ```
>
> 5. **填充字符（`setfill`）**：
>    `setfill` 用于设置输出时填充字符。如果字段宽度不足，输出会使用该字符来填充。
>
>    ```cpp
>    #include <iostream>
>    #include <iomanip>
>    using namespace std;
>                                                                                                 
>    int main() {
>        cout << setfill('*') << setw(10) << 42 << endl;  // 输出 "******42"
>        return 0;
>    }
>    ```
>
> **常见的 `iomanip` 常量：**
>
> - **`fixed`**：强制以小数点形式输出浮点数。
> - **`scientific`**：强制以科学计数法输出浮点数。
> - **`setprecision(n)`**：设置浮点数输出的精度，保留 n 位小数。
> - **`setw(n)`**：设置输出的宽度，输出内容小于 n 时会自动填充空格。
> - **`setfill(ch)`**：设置填充字符，输出内容小于指定宽度时会用该字符填充。
>
> **示例代码：**
>
> ```cpp
> #include <iostream>
> #include <iomanip>
> using namespace std;
> 
> int main() {
>     double pi = 3.14159265358979;
>     int number = 42;
> 
>     // 设置精度为 3 位小数
>     cout << fixed << setprecision(3) << pi << endl;  // 输出 3.142
>     
>     // 设置输出宽度为 10，使用填充字符 '*'
>     cout << setfill('*') << setw(10) << number << endl;  // 输出 "******42"
>     
>     // 设置对齐方式为右对齐
>     cout << right << setw(10) << number << endl;  // 输出 "       42"
> 
>     return 0;
> }
> ```
>
> **总结：**
>
> `<iomanip>` 使得你可以灵活地控制 C++ 输出格式，常用的有设置浮点数精度、输出宽度、对齐方式、填充字符等功能。



## E02676: 整数的个数

math, http://cs101.openjudge.cn/pctbook/E02676/

给定k（1< k < 100）个正整数，其中每个数都是大于等于1，小于等于10的数。写程序计算给定的k个正整数中，1，5和10出现的次数。

**输入**

输入有两行：第一行包含一个正整数k，第二行包含k个正整数，每两个正整数用一个空格分开。

**输出**

输出有三行，第一行为1出现的次数，，第二行为5出现的次数，第三行为10出现的次数。

样例输入

```
5
1 5 8 10 5 
```

样例输出

```
1
2
1
```

来源

计算概论05－模拟考试1



```c++
#include <iostream>
using namespace std;

int main() {
    int k;
    cin >> k;
    int cnt1 = 0, cnt5 = 0, cnt10 = 0;
    for (int i = 0; i < k; i++) {
        int x;
        cin >> x;
        if (x == 1) cnt1++;
        else if (x == 5) cnt5++;
        else if (x == 10) cnt10++;
    }
    cout << cnt1 << endl;
    cout << cnt5 << endl;
    cout << cnt10 << endl;
    return 0;
}

```



```c++
#include <iostream>
#include <sstream>
using namespace std;

int main() {
    int k;
    cin >> k;
    cin.ignore();   // 忽略掉换行符

    string line;
    getline(cin, line);   // 读入整行数字

    stringstream ss(line);
    int x, cnt1 = 0, cnt5 = 0, cnt10 = 0;

    while (ss >> x) {   // 按空格自动分割。>> 操作符自动忽略多余的空格、换行符
        if (x == 1) cnt1++;
        else if (x == 5) cnt5++;
        else if (x == 10) cnt10++;
    }

    cout << cnt1 << "\n" << cnt5 << "\n" << cnt10 << endl;
    return 0;
}

```



【鲍雷栋，2021年秋，物理学院】

由于 Python 对整型高精度的支持，对 C++ 及其他语言使用者来说学习 Python 基础语法是有必要的。应当说，学习 Python 中的一道坎是接受它的输入和输出方式，在习惯了其他语言输入输出方式后再学 Python 的直接一行输入一行输出的方式有种“难以理解”的感觉，仿佛无形之中增添了麻烦。

但在一些输入形式上，Python 自带的函数却提供了便捷，例如split。为了让 C++ 选手们减少不必要的痛苦，将 C++ 中实现 split 的代码放在下面，实现利用了 stringstream 和 vector，如果需要读取 int 或 double，利用自带的 stoi 或 stod 转换即可。

```c++
#include <iostream>
#include <vector>
#include <sstream>
using namespace std;

// 模拟 Python 的 split 函数
vector<string> split(string str, char sp) {
    istringstream iss(str);
    vector<string> res;
    string subs;
    while (getline(iss, subs, sp)) {
        if (!subs.empty()) res.push_back(subs);
    }
    return res;
}

int main() {
    int k;
    cin >> k;          // 读入 k
    cin.ignore();      // 忽略掉换行符，不然 getline 会读到空行

    string line;
    getline(cin, line);   // 一次性读入整行数字

    vector<string> nums = split(line, ' ');  // 按空格分割
    int cnt1 = 0, cnt5 = 0, cnt10 = 0;

    for (string s : nums) {
        int x = stoi(s);   // 转换为整数
        if (x == 1) cnt1++;
        else if (x == 5) cnt5++;
        else if (x == 10) cnt10++;
    }

    cout << cnt1 << "\n" << cnt5 << "\n" << cnt10 << endl;
    return 0;
}

```



## E02733: 判断闰年

math, http://cs101.openjudge.cn/pctbook/E02733

判断某年是否是闰年。

**输入**

输入只有一行，包含一个整数a(0 < a < 3000)

**输出**

一行，如果公元a年是闰年输出Y，否则输出N

样例输入

```
2006
```

样例输出

```
N
```

提示

公历纪年法中，能被4整除的大多是闰年，但能被100整除而不能被400整除的年份不是闰年， 能被3200整除的也不是闰年，如1900年是平年，2000年是闰年，3200年不是闰年。



C语言在语法层面上基本是C++的子集，因此许多用C语言编写的程序也能直接使用C++编译器进行编译。例如，下面这段代码虽然是典型的C风格写法，但同样可以用C++编译器成功编译并运行

```c++
#include <cstdlib>
#include <cstdio>

int main()
{
    int a;
    scanf("%d", &a);

    if (a % 4 == 0)
    {
        if (a % 100 == 0 && a % 400 != 0)
            printf("N");
        else
            printf("Y");
    }
    else
        printf("N");
}
```



## E02750: 鸡兔同笼

math, http://cs101.openjudge.cn/pctbook/E02750/

一个笼子里面关了鸡和兔子（鸡有2只脚，兔子有4只脚，没有例外）。已经知道了笼子里面脚的总数a，问笼子里面至少有多少只动物，至多有多少只动物。

**输入**

一行，一个正整数a (a < 32768)。

**输出**

一行，包含两个正整数，第一个是最少的动物数，第二个是最多的动物数，两个正整数用一个空格分开。
如果没有满足要求的答案，则输出两个0，中间用一个空格分开。

样例输入

```
20
```

样例输出

```
5 10
```



```c++
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;
    
    int b = n / 2; // 最多动物数
    if (n % 4 == 2) {
        int a = (n + 2) / 4; // 最少动物数
        cout << a << " " << b << endl;
    } else if (n % 4 == 0) {
        int a = n / 4; // 最少动物数
        cout << a << " " << b << endl;
    } else {
        cout << "0 0" << endl; // 无解
    }

    return 0;
}

```





## E04067: 回文数字（Palindrome Number）

two pointers, queue, http://cs101.openjudge.cn/pctbook/E04067/

给出一系列非负整数，判断是否是一个回文数。回文数指的是正着写和倒着写相等的数。

**输入**

若干行，每行是一个非负整数（不超过99999999）

**输出**

对每行输入，如果其是一个回文数，输出YES。否则输出NO。

样例输入

```
11
123
0
14277241
67945497
```

样例输出

```
YES
NO
YES
YES
NO
```



这是经典的**回文串判定**问题。常见思路有：

1. **双指针法**
   从字符串首尾同时向中间比较。
2. **队列（deque）法**
   使用双端队列，从两端依次弹出比较。
3. **直接翻转字符串**
   判断 `s == reversed(s)`。

同时，本题需要处理**不定行输入**，在 C++ 中常用 `while (cin >> s)` 来逐行读取。



双指针法

```c++
#include <iostream>
#include <string>
using namespace std;

bool isPalindrome(const string &s) {
    int front = 0, back = s.size() - 1;
    while (front < back) {
        if (s[front] != s[back]) return false;
        front++;
        back--;
    }
    return true;
}

int main() {
    string s;
    while (cin >> s) {  // 处理不定行输入
        cout << (isPalindrome(s) ? "YES" : "NO") << endl;
    }
    return 0;
}

```



使用 deque 模拟双端队列

```c++
#include <iostream>
#include <string>
#include <deque>
using namespace std;

string isPalindrome(const string &s) {
    deque<char> dq(s.begin(), s.end());
    while (dq.size() > 1) {
        if (dq.front() != dq.back()) return "NO";
        dq.pop_front();
        dq.pop_back();
    }
    return "YES";
}

int main() {
    string s;
    while (cin >> s) {
        cout << isPalindrome(s) << endl;
    }
    return 0;
}

```



直接反转字符串

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    string s;
    while (cin >> s) {
        string rev = s;
        reverse(rev.begin(), rev.end());
        cout << (s == rev ? "YES" : "NO") << endl;
    }
    return 0;
}

```



## E07618: 病人排队

sorting, http://cs101.openjudge.cn/pctbook/E07618/

病人登记看病，编写一个程序，将登记的病人按照以下原则排出看病的先后顺序：

1. 老年人（年龄 >= 60岁）比非老年人优先看病。
2. 老年人按年龄从大到小的顺序看病，年龄相同的按登记的先后顺序排序。
3. 非老年人按登记的先后顺序看病。



**输入**

第1行，输入一个小于100的正整数，表示病人的个数；
后面按照病人登记的先后顺序，每行输入一个病人的信息，包括：一个长度小于10的字符串表示病人的ID（每个病人的ID各不相同且只含数字和字母），一个整数表示病人的年龄，中间用单个空格隔开。

**输出**

按排好的看病顺序输出病人的ID，每行一个。

样例输入

```
5
021075 40
004003 15
010158 67
021033 75
102012 30
```

样例输出

```
021033
010158
021075
004003
102012
```

来源

习题(14-6)



**使用`stable_sort`**：为了确保老年人按登记顺序排，如果年龄相同，`stable_sort` 可以保证相同年龄的老年人保持输入时的顺序。sort不稳定，会WA。

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

struct ren {
    string id;
    int a;
    ren(string i, int A) : id(i), a(A){}
    ren() : id(""), a(0){}
};

ren l[105];
ren r[105];

bool cmp(ren a, ren b) {
    return a.a > b.a;
}

int main() {
    int n;
    cin >> n;
    int cnt = 0;
    for (int i = 1; i <= n; i++) {
        string s;
        int a;
        cin >> s >> a;
        if (a >= 60) {
            cnt++;
            l[cnt] = ren(s, a);
        } else {
            r[i - cnt] = ren(s, a);
        }
    }
    stable_sort(l + 1, l + cnt + 1, cmp);
    for (int i = 1; i <= cnt; i++) {
        cout << l[i].id << endl;
    }
    for (int i = 1; i <= n - cnt; i++) {
        cout << r[i].id << endl;
    }
    return 0;
}

```



## E18161: 矩阵运算

matrices, http://cs101.openjudge.cn/pctbook/E18161/

请使用`@`矩阵相乘运算符。

思路：按定义写即可。

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <sstream>
using namespace std;


class marix
{
    private:
        int index = 0;//用来表征能否进行运算

    public:
        int row, col;
        vector<vector<int>> mar;

        void getMarix()
        {
            cin>> row >> col;
            mar.resize(row, vector<int>(col, 0));
            for(int i = 0; i < row; i++)
            {
                for(int j = 0; j < col; j++)
                {
                    cin >> mar[i][j];
                }
            }
            index = 0;
        }

        marix operator+(const marix m)
        {
            if(row != m.row || col != m.col|| index == 1)
            {   
                index = 1;
                return *this;
            }
            marix res;
            res.row = row;
            res.col = col;
            res.mar.resize(row, vector<int>(col, 0));
            for(int i = 0; i < row; i++)
            {
                for(int j = 0; j < col; j++)
                {
                    res.mar[i][j] = mar[i][j] + m.mar[i][j];
                }
            }
            return res;
        }

        marix operator*(const marix m)
        {
            if(col != m.row || index == 1)
            {
                index = 1;
                return *this;
            }
            marix res;
            res.row = row;
            res.col = m.col;
            res.mar.resize(row, vector<int>(m.col, 0));
            for(int i = 0; i < row; i++)
            {
                for(int j = 0; j < m.col; j++)
                {
                    for (int k = 0; k < col; k++)
                    {
                        res.mar[i][j] += mar[i][k] * m.mar[k][j];
                    }
                }
            }
            return res;
        }

        void printMarix()
        {
            if(index == 1)
                cout << "Error!" ;
            else
            {
                for(int i = 0; i < row; i++)
                {
                    if (i) cout << endl;
                    for(int j = 0; j < col; j++)
                    {
                        if (j) cout << " ";
                        cout << mar[i][j] ;
                    } 
                }
            }
        }

};


int main() 
{
    marix A, B, C, D;
    A.getMarix();
    B.getMarix();
    C.getMarix();
    D= A * B + C;
    D.printMarix();
}
```



## E19942: 二维矩阵上的卷积运算

matrices, http://cs101.openjudge.cn/pctbook/E19942/


思路：定义一个卷积函数即可，一遍ac，用时约15min

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <sstream>
using namespace std;


class marix
{
    private:
        int index = 0;//用来表征能否进行运算

    public:
        int row, col;
        vector<vector<int>> mar;

        void setSize()
        {
            cin >> row >> col;
            mar.resize(row, vector<int>(col, 0));
        }

        void getMarix()
        {
            for(int i = 0; i < row; i++)
            {
                for(int j = 0; j < col; j++)
                {
                    cin >> mar[i][j];
                }
            }
            index = 0;
        }

        void printMarix()
        {
            if(index == 1)
                cout << "Error!" ;
            else
            {
                for(int i = 0; i < row; i++)
                {
                    if (i) cout << endl;
                    for(int j = 0; j < col; j++)
                    {
                        if (j) cout << " ";
                        cout << mar[i][j] ;
                    } 
                }
            }
        }

};

marix convolution(marix A, marix B)
{
    marix C;
    C.row = A.row - B.row + 1;
    C.col = A.col - B.col + 1;
    C.mar.resize(C.row, vector<int>(C.col, 0));
    for(int i = 0; i < C.row; i++)
    {
        for(int j = 0; j < C.col; j++)
        {
            for(int k = 0; k < B.row; k++)
            {
                for(int l = 0; l < B.col; l++)
                {
                    C.mar[i][j] += A.mar[i + k][j + l] * B.mar[k][l];
                }
            }
        }
    }
    return C;
}

int main() 
{
    marix A, B, C;
    A.setSize();
    B.setSize();
    A.getMarix();
    B.getMarix();
    C = convolution(A, B);
    C.printMarix();
}
```





## 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/

思路：当 n = 0、1、2 时，直接返回对应的初始值。
从 T3 开始，每一项等于前三项之和。可以用三个变量循环更新，节省空间。

```c++
#include <iostream>
using namespace std;

int tribonacci(int n) {
    if (n == 0) return 0;
    if (n == 1 || n == 2) return 1;
    int t0 = 0, t1 = 1, t2 = 1, t3;
    for (int i = 3; i <= n; ++i) {
        t3 = t0 + t1 + t2;
        t0 = t1;
        t1 = t2;
        t2 = t3;
    }
    return t2;
}

int main() {
    int n;
    cin >> n;
    cout << tribonacci(n) << endl;
    return 0;
}
```



## E02753:菲波那契数列

http://cs101.openjudge.cn/pctbook/E02753

```cpp
//dp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        int input;
        cin >> input;
        if (input == 1 || input == 2)
        {
            cout << 1 << endl;
            continue;
        }
        int a = 1, b = 1;
        int tmp;
        for (int i = 0; i < input - 2; i++)
        {
            tmp = a + b;
            a = b;
            b = tmp;
        }
        cout << b << endl;
    }
    return 0;
}

//math
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int n;
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        int input;
        cin >> input;
        cout << (1 / sqrt(5)) * (pow((1 + sqrt(5)) / 2, input) - pow((1 - sqrt(5)) / 2, input)) << endl;
    }
    return 0;
}
```





## 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/

思路：枚举从 2 到 n/2 的所有数 A，若 A 和 n-A 都是素数，则输出这两个数并结束。

```c++
#include <iostream>

using namespace std;

bool isPrime(int num)
{
    for (int i = 2; i * i <= num; i++)
    {
        if (num % i == 0)
            return false;
    }
    return true;
}

int main()
{
    int n;
    cin >> n;
    for (int i = 2; i <= n / 2; i++)
    {
        if (isPrime(i) && isPrime(n - i))
        {
            cout << i << " " << n - i;
            return 0;
        }
    }
}

```



## E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/pctbook/E23555

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int n;
    scanf("%d", &n);
    vector<vector<int>> x(n, vector<int>(n, 0));
    vector<vector<int>> y(n, vector<int>(n, 0));

    int m1, m2;
    scanf("%d%d", &m1, &m2);
    for (int i = 0; i < m1; i++)
    {
        int a, b, v;
        scanf("%d%d%d", &a, &b, &v);
        x[a][b] = v;
    }
    for (int i = 0; i < m2; i++)
    {
        int a, b, v;
        scanf("%d%d%d", &a, &b, &v);
        y[a][b] = v;
    }
    
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
        {
            int ans = 0;
            for (int k = 0; k < n; k++)
                ans += x[i][k] * y[k][j];
            if (ans != 0)
                printf("%d %d %d\n", i, j, ans);
        }
    return 0;
}
```

>



## E23563: 多项式时间复杂度

http://cs101.openjudge.cn/pctbook/E23563/



解题步骤

1. **分割字符串**
    按照 `'+'` 拆分每一项。
2. **解析每一项**
   - 可能形式：
     - `ax^b` （如 `6n^2`）
     - `n^b`   （相当于系数 1）
     - `an^b`  （如 `99n^10`）
     - `0n^b`  （等价于 0）
     - 纯常数 `5` （等价于 `5n^0`）
   - 提取指数 b，如果该项系数为 0，则忽略。
3. **找最大指数**
    遍历所有项，记录最大 `b`。
4. **输出**
    输出 `n^最大指数`。

```c++
//#include <bits/stdc++.h>
#include <iostream>
#include <string>
#include <sstream>
#include <algorithm>
using namespace std;

int main() {
    string s;
    cin >> s;

    int maxExp = 0;  // 记录最大指数
    stringstream ss(s);
    string term;

    while (getline(ss, term, '+')) {
        int coef = 1;  // 默认系数
        int exp = 0;   // 默认指数

        size_t nPos = term.find('n');
        if (nPos == string::npos) {
            // 没有 n，纯常数项
            coef = stoi(term);
            exp = 0;
        } else {
            // 处理系数
            if (nPos == 0) {
                coef = 1; // "n^b"
            } else {
                coef = stoi(term.substr(0, nPos));
            }

            // 处理指数
            size_t powPos = term.find('^');
            if (powPos == string::npos) {
                exp = 1; // 只有 "n"，即 n^1
            } else {
                exp = stoi(term.substr(powPos + 1));
            }
        }

        if (coef != 0) {
            maxExp = max(maxExp, exp);
        }
    }

    cout << "n^" << maxExp << endl;
    return 0;
}
```



## E24588: 后序表达式求值

Stack, http://cs101.openjudge.cn/practice/24588/

思路：按照课上讲的用栈解决即可，忘记处理单走一个数字的情形了，花了点时间找bug，用时约20min，由于代码全部手敲，因此运行时间很短，仅1ms

```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <iomanip>
using namespace std;

vector<double> st;

bool isNumber(char s) 
{
    return (s >= '0' && s <= '9');
}

void calc(char c) 
{
    double a = st.back(); st.pop_back();
    double b = st.back(); st.pop_back();
    switch (c) 
    {
    case '+': st.push_back(b + a); break;
    case '-': st.push_back(b - a); break;
    case '*': st.push_back(b * a); break;
    case '/': st.push_back(b / a); break;
    }
}

double calculate() 
{
    st.clear();
    char c;
    double tmp = 0;
    bool isNum = false;
    double frac = 0;
    while ((c = getchar())) 
    {
        if (c == '\n' || c == EOF) 
        {
            if (isNum) st.push_back(tmp);
            break;
        }
        if (isNumber(c)) 
        {
            isNum = true;
            if (frac == 0) tmp = tmp * 10 + (c - '0');
            else 
            {
                tmp += (c - '0') * frac;
                frac *= 0.1;
            }
        }
        else if (c == '.') 
        {
            frac = 0.1;
        }
        else if (c == ' ') 
        {
            if (isNum) 
            {
                st.push_back(tmp);
                tmp = 0; frac = 0; isNum = false;
            }
        }
        else if (c == '+' || c == '-' || c == '*' || c == '/') 
        {
            if (isNum) 
            {
                st.push_back(tmp);
                tmp = 0; frac = 0; isNum = false;
            }
            calc(c);
        }
    }
    return st.back();
}

int main() 
{
    int N;
    cin >> N;
    cin.ignore();
    while (N--) 
    {
        double ans = calculate();
        cout << fixed << setprecision(2) << ans << endl;
    }
}

```



## E27653: Fraction类

http://cs101.openjudge.cn/pctbook/E27653/

请练习用OOP方式实现。



思路：建立一个分数类，定义分数的定义，化简，运算和输出，用时约30分钟（主要用来学习什么是类）

```c++
//该题练习使用了一下类
#include <iostream>
using namespace std;
//最大公约数
int gcd(int a, int b)
{
    if (b == 0)
    {
        return a;
    }
    return gcd(b, a % b);
    }

//实现分数相加，化简的类
class Fraction
{
    private:
        int numerator; //分子
        int denominator; //分母
    public:
        Fraction(int numerator, int denominator)
        {
            this->numerator = numerator;
            this->denominator = denominator;
            simplify();
        }
        //化简
        void simplify()
        {
            int g = gcd(this->numerator, this->denominator);
            this->numerator /= g;
            this->denominator /= g;
        }
        //定义分数相加
        Fraction operator+(Fraction& f)
        {
            int numerator = this->numerator * f.denominator + f.numerator * this->denominator;
            int denominator = this->denominator * f.denominator;
            simplify();
            return Fraction(numerator, denominator);
        }
        //输出
        void show()
        {
            cout << this->numerator << "/" << this->denominator << endl;
        }
};

int main()
{
    int numerator_1, denominator_1, numerator_2, denominator_2;
    cin >> numerator_1 >> denominator_1 >> numerator_2 >> denominator_2;
    //两个分数相加及化简
    Fraction f1(numerator_1, denominator_1);
    Fraction f2(numerator_2, denominator_2);
    Fraction f3 = f1 + f2;
    f3.show();
}

```





## E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/pctbook/E28674/



```cpp
#include <iostream>
using namespace std;

int main()
{
    int k;
    string password;
    cin >> k >> password;
    k = k % 26; 
    for (int i = 0; i < password.length(); i++)
    {
        if (password[i] >= 'A' && password[i] <= 'Z')
        {
            password[i] = (password[i] - 'A' - k + 26) % 26 + 'A';
        }
        else if (password[i] >= 'a' && password[i] <= 'z')
        {
            password[i] = (password[i] - 'a' - k + 26) % 26 + 'a';
        }
    }
    cout << password << endl;
    return 0;
}
```



## M28678: 角谷猜想

http://cs101.openjudge.cn/practice/28678/



```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;
    while (true)
    {
        if (n == 1)
            break;
        if (n % 2 == 0)
        {
            printf("%d/2=%d\n", n, n / 2);
            n /= 2;
        }
        else
        {
            printf("%d*3+1=%d\n", n, n * 3 + 1);
            n = n * 3 + 1;
        }
        if (n == 1)
            break;
    }
    cout << "End\n";
    return 0;
}
```



## E28691: 字符串中的整数求和

http://cs101.openjudge.cn/pctbook/E28691/



```cpp
#include <iostream>
using namespace std;

int main()
{
    string a, b;
    cin >> a >> b;
    cout << stoi(a) + stoi(b) << endl;
    return 0;
}
```



## E29895: 分解因数

implementation, http://cs101.openjudge.cn/practice/29895/

```cpp
#include<bits/stdc++.h>
using namespace std;
long long n;
int main(){
    scanf("%lld",&n);
    for(long long i=2;i<=n/i;i++){
        if(n%i==0){
            printf("%lld",n/i);
            return 0;
        }
    }
    return 0;
}
```



## E29940: 机器猫斗恶龙

greedy, http://cs101.openjudge.cn/practice/29940/

```cpp
#include<bits/stdc++.h>
using namespace std;
int n,ans,a,sum=-1;
int main(){
    scanf("%d",&n);
    for(int i=1;i<=n;i++){
        scanf("%d",&a);
        sum+=a;
        ans=min(ans,sum);
    }
    printf("%d",-ans);
    return 0;
}
```



## E29952 咒语序列

思路：

- 考虑对每个位置 $i$，**可能**存在一个**最大的** $j \leq i$，使得 $[j, i]$ 为一个合法括号序列，如 `()(())` 中 $i = 6$ 对应的最大的 $j$ 为 $3$，$i = 4$ 时不存在这样的 $j$。
- 考虑 dp：设 $dp_i$ 表示 $s[1, i]$ 的最长合法**后缀**括号序列。
- 从前到后扫一遍，维护一个栈，当 $s_i$ 为 `(` 时将 $i$ 压入，当 $s_i$  为 `)` 时，若栈非空则 $j$ 为栈顶下标，然后弹栈，此时更新 $dp_i = dp_{j - 1} + (i - j + 1)$。
- 答案即为 $\max(dp_i)$。时间复杂度为 $O(n)$。
- 如上面的例子中，$dp_2 = dp_0 + 2 = 2, dp_5 = dp_3 + 2 = 2, dp_6 = dp_2 + 4 = 6$，答案为 $\max(dp_2, dp_5, dp_6) = 6$。

代码：

```cpp
#include <iostream>
#include <stack>

using namespace std;

int dp[30001];
stack<int> stk;

int main(){
	int len, ans = 0;
	string s;
	cin >> s;
	len = s.size();
	s = " " + s;
	for (int i = 1; i <= len; i++){
		if (s[i] == '('){
			stk.push(i);
		} else {
			if (!stk.empty()){
				int cur = stk.top();
				stk.pop();
				dp[i] = dp[cur - 1] + (i - cur + 1);
				ans = max(ans, dp[i]);
			}
		}
	}
	cout << ans;
	return 0;
}
```





# Medium



## M06: 空格分隔输出

http://noi.openjudge.cn/ch0101/06/

读入一个字符，一个整数，一个单精度浮点数，一个双精度浮点数，然后按顺序输出它们，并且要求在他们之间用一个空格分隔。输出浮点数时保留6位小数。

**输入**

共有四行：
第一行是一个字符；
第二行是一个整数；
第三行是一个单精度浮点数；
第四行是一个双精度浮点数。

**输出**

输出字符、整数、单精度浮点数和双精度浮点数，之间用空格分隔。

样例输入

```
a
12
2.3
3.2
```

样例输出

```
a 12 2.300000 3.200000
```

来源

习题(2-4)



这题目初衷是面向C++语言的。

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    char c;
    int n;
    float f1;
    double f2;

    if (!(cin >> c >> n >> f1 >> f2)) return 0;

    cout << c << ' ' << n << ' ' << fixed << setprecision(6) << f1 << ' ' << f2 << '\n';
    return 0;
}
```



Python 中没有严格的 单精度 / 双精度 区分，float 默认就是双精度浮点数。所以 Python 想 AC，必须在读到“单精度”的时候，**先按 C++ float 精度截断一次**，再输出。注意到 C++ 的 `float`/`double` 丢精度是二进制截断，在Python中**用 `struct` 做二进制精度截断**模拟。

> 用 `struct.pack/unpack`，它直接用二进制截断，和 C++ 的行为完全一致。

```python
import struct

def to_c_float(x: float) -> float:
    # 先把 Python 的 float (C double) 按照 C float (4字节) 打包
    b = struct.pack('f', x)
    # 再解包回来变成 Python float，这时候数值精度已经被截断到 float 精度
    return struct.unpack('f', b)[0]


def main():
    c = input().strip()
    i = int(input().strip())
    f1 = float(input().strip())   # 读单精度
    f2 = float(input().strip())   # 读双精度

    f1 = to_c_float(f1)  # 模拟 C++ float 精度

    print(f"{c} {i} {f1:.6f} {f2:.6f}")

if __name__ == "__main__":
    main()
```

> - `struct.pack('f', x)`
>   把 `x` 按 **单精度浮点数 (4字节, IEEE 754)** 存储。
> - `struct.unpack('f', …)[0]`
>   再把 4 字节解析出来，转成 Python 的 `float`（C double），但精度已经丢失，只保留了单精度的部分。`'f'` 表示解析一个单精度浮点，所以返回的 tuple 里有 **1 个元素**；这里取 `[0]`，拿到里面唯一的那个值。
>
> 这样就可以 **模拟 C++ 里的 float 精度**。



## M01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

思路：日期计算很简单，但是有个tricky的地方就是如果days中日期+1那么对于被260整除的数会计算成下一年。

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main()
{
    int n;
    cin >> n;
    vector<string> Habb = {"pop", "no", "zip", "zotz", "tzec", "xul", "yoxkin", "mol", "chen", "yax", "zac", "ceh", "mac", "kankin", "muan", "pax", "koyab", "cumhu", "uayet"};
    string Tzolkin[] = {"ahau", "imix", "ik", "akbal", "kan", "chicchan", "cimi", "manik", "lamat", "muluk", "ok", "chuen", "eb", "ben", "ix", "mem", "cib", "caban", "eznab", "canac"};
    cout << n << endl;
    for (int i = 0; i < n; i++)
    {
        int H_Year, H_Date;
        string H_Month;
        cin >> H_Date;
        cin.ignore();
        cin >> H_Month >> H_Year;
        int days;
        for (int i = 0; i < Habb.size(); i++)
            if (Habb[i] == H_Month)
            {
                days = i * 20;
                break;
            }
        days += H_Date + H_Year * 365;
        int T_Year = days / 260;
        string T_Month = Tzolkin[(days + 1) % 260 % 20];
        int T_Date = days % 260 % 13 + 1;
        cout << T_Date << ' ' << T_Month << ' ' << T_Year << endl;
    }
    return 0;
}
```





## M01017: 装箱问题

greedy, http://cs101.openjudge.cn/pctbook/M01017/



```c++
#include<bits/stdc++.h>
using namespace std;
int a[10], sum, a2, a1;
bool flag;
int main(){
    while(1){
        flag = 0;
        for(int i = 1; i <= 6; i++){
            scanf("%d", &a[i]);
            if(a[i])
                flag = 1;
        }
        if(!flag)
            break;

        sum = a[6] + a[5] + a[4] + a[3]/4 + (a[3]%4 ? 1 : 0);
        a2 = a[4] * 5;
        a1 = a[5]*11 + a[4]*20 + (a[3]%4 ? ((4 - a[3]%4)*9) : 0);
        if(a[3]%4 == 3) a2 += 1;
        else if(a[3]%4 == 2) a2 += 3;
        else if(a[3]%4 == 1) a2 += 5;
        a1 -= 4 * min(a[2], a2);
        a[2] -= a2;
        if(a[2] > 0){
            sum += a[2]/9;
            if(a[2]%9){
                sum++;
                a1 += 36 - a[2]%9 * 4;
            }
        }
        a[1] -= a1;
        if(a[1] > 0)
            sum += a[1]/36 + (a[1]%36 ? 1 : 0);
        printf("%d\n", sum);
    }
    return 0;
}
```



```python
# 
#include <iostream>
using namespace std;

int main() {
    int remain[4] = {0, 5, 3, 1};
    while(true) {
        int arr[6], count=0;
        bool status=false;
        for(int i=0; i<6; i++)  {
            cin>>arr[i];
            if(arr[i]!=0) status=true;
        }
        if(status == false){break;}
        count += arr[5]+arr[4]+arr[3]+(arr[2]+3)/4;
        int num1 = arr[3]*5+remain[arr[2]%4];
        if(arr[1]>num1) {
            count += ((arr[1]-num1)+8)/9;
        }
        int num2=count*36-25*arr[4]-36*arr[5]-16*arr[3]-9*arr[2]-4*arr[1];
        if(arr[0]>num2) {
            count += ((arr[0]-num2)+35)/36;
        }
        cout<<count<<'\n';
    }
    return 0;
}
```





## M01321: 棋盘问题

backtracking, http://cs101.openjudge.cn/pctbook/M01321

在一个给定形状的棋盘（形状可能是不规则的）上面摆放棋子，棋子没有区别。要求摆放时任意的两个棋子不能放在棋盘中的同一行或者同一列，请编程求解对于给定形状和大小的棋盘，摆放k个棋子的所有可行的摆放方案C。

**输入**

输入含有多组测试数据。
每组数据的第一行是两个正整数，n k，用一个空格隔开，表示了将在一个n*n的矩阵内描述棋盘，以及摆放棋子的数目。 n <= 8 , k <= n
当为-1 -1时表示输入结束。
随后的n行描述了棋盘的形状：每行有n个字符，其中 # 表示棋盘区域， . 表示空白区域（数据保证不出现多余的空白行或者空白列）。

**输出**

对于每一组数据，给出一行输出，输出摆放的方案数目C （数据保证C<2^31）。

样例输入

```
2 1
#.
.#
4 4
...#
..#.
.#..
#...
-1 -1
```

样例输出

```
2
1
```

来源

蔡错@pku



这个问题要求我们在一个不规则的棋盘上摆放棋子，且任何两个棋子都不能放在同一行或同一列。我们需要找出所有符合条件的摆放方案数。

**思路分析：**

1. **棋盘的表示：**
   棋盘是一个`n*n`的矩阵，每个位置上可能是`#`（可以放棋子）或者`.`（不能放棋子）。
2. **摆放棋子的要求：**
   - 不同的棋子不能在同一行或同一列。
   - `k`个棋子必须放置在`#`的位置上。
3. **求解方法：**
   这类似于**n皇后问题**的变种，可以使用**回溯法**来搜索所有可行的摆放方案。
4. **回溯法：**
   - 通过回溯的方法尝试在棋盘上放置`k`个棋子。
   - 需要记录已被放置棋子的行和列，避免放在同一行或同一列。
   - 只考虑可以放棋子的格子，即`#`的位置。
5. **输入与输出：**
   - 输入中有多组测试数据，直到输入为`-1 -1`时结束。
   - 对每组数据输出可行的摆放方案数。



```cpp
#include <iostream>
#include <vector>

using namespace std;

// 回溯函数
void placePieces(int n, int k, int row, vector<string>& board, vector<int>& cols, int& count) {
    // 如果已经放置了k个棋子，计数加一
    if (k == 0) {
        count++;
        return;
    }
    
    // 从当前行row开始尝试
    for (int i = row; i < n; i++) {
        // 遍历该行所有列
        for (int j = 0; j < n; j++) {
            // 如果当前位置是可放棋子的地方，并且没有放置在该列，且该行还没被用过
            if (board[i][j] == '#' && !cols[j]) {
                // 放置棋子，标记该行和该列
                cols[j] = 1;
                placePieces(n, k - 1, i + 1, board, cols, count);
                // 回溯，撤销棋子的放置
                cols[j] = 0;
            }
        }
    }
}

int main() {
    int n, k;
    
    while (cin >> n >> k, n != -1 && k != -1) {
        vector<string> board(n);
        for (int i = 0; i < n; i++) {
            cin >> board[i];
        }
        
        vector<int> cols(n, 0);  // 用来记录列的状态，0表示该列没有放棋子，1表示放了
        int count = 0;
        
        placePieces(n, k, 0, board, cols, count);
        
        cout << count << endl;
    }
    
    return 0;
}
```

代码解释：

1. **`placePieces`函数**：
   - 这是一个回溯函数，用来递归地在棋盘上放置`k`个棋子。
   - 参数：
     - `n`：棋盘的大小。
     - `k`：当前需要放置的棋子数目。
     - `row`：当前正在处理的行。
     - `board`：棋盘的形状，记录每个位置是否可放棋子。
     - `cols`：一个数组，用来标记哪些列已经被占用。
     - `count`：用来记录当前的方案数。
   - 回溯的核心是：在一个行内，尝试将棋子放在每个`#`的位置上，放置棋子后递归处理下一个棋子，放置后回溯撤销该放置，继续寻找下一个位置。
2. **`main`函数**：
   - 读取输入，处理每一组测试数据。
   - 对于每组数据，调用`placePieces`函数来计算所有可能的摆放方案数。

**时间复杂度：**

- 由于最多有`n`行，每行最多有`n`个格子需要判断，递归过程中最多会遍历所有可能的放置方式。
- 回溯的时间复杂度大致为`O(n^k)`，其中`k`是要摆放的棋子数。



## M01328 Radar Installation

思路：

- 若 $\exists 1 \leq i \leq n, \text{s.t. } y_i > d$，显然无解；否则，$\forall 1 \leq i \leq n$，令 $r_i = \sqrt{d^2 - y_i^2}$，我们要求 $[x_i - r_i, x_i + r_i]$ 中至少存在一个雷达。
- 因此问题抽象为：给定数轴上若干线段 $[L_i, R_i]$，要求在数轴上选出尽可能少的点，使得每一条线段中都至少含有一个点。
- 考虑按 $R_i$ 将线段升序排序，记录当前选的最靠右的点的位置 $t$，若 $t < L_i$ 则在 $R_i$ 处新选一个点。
- 时间复杂度为 $O(\sum n \log n)$。

代码：

```cpp
#include <iostream>
#include <algorithm>
#include <cmath>

using namespace std;

typedef long long ll;

struct Requirement {
	double l;
	double r;
};

const double eps = 1e-9;
int x[1001], y[1001];
Requirement req[1001];

bool operator <(const Requirement a, const Requirement b){
	return a.r < b.r;
}

bool myless(double a, double b){
	return fabs(a - b) > eps && a < b;
}

bool solve(int cas){
	int n, d;
	cin >> n >> d;
	if (n == 0 && d == 0) return false;
	bool flag = true;
	for (int i = 1; i <= n; i++){
		cin >> x[i] >> y[i];
		if (y[i] > d) flag = false;
	}
	if (!flag){
		cout << "Case " << cas << ": " << -1 << endl;
		return true;
	}
	int ans = 0;
	double lst = -1e10;
	for (int i = 1; i <= n; i++){
		double r = sqrt((ll)d * d - (ll)y[i] * y[i]);
		req[i].l = x[i] - r;
		req[i].r = x[i] + r;
	}
	sort(req + 1, req + n + 1);
	for (int i = 1; i <= n; i++){
		if (myless(lst, req[i].l)){
			lst = req[i].r;
			ans++;
		}
	}
	cout << "Case " << cas << ": " << ans << endl;
	return true;
}

int main(){
	for (int i = 1; solve(i); i++) ;
	return 0;
}
```



```c++
#include <iostream>
#include <vector>
#include <cmath>
#include <algorithm>
using namespace std;

struct loc{
 int x;
 int y;
};
struct range{
 float l;
 float r;
};
range f(loc a,int d){
 float w=sqrt(d*d-a.y*a.y);
 return {a.x-w, a.x+w};
}
bool cmp(range a,range b){
 return a.r<b.r;
}
int main(){
 int count=0;
 bool noans=0;
 while(true){
     count++;
     int n,d;
     cin>>n>>d;
     if(n==0&&d==0) {break;}
     vector<loc> locs(n);
     vector<range> ranges(n);
     for(int i=0;i<n;i++){
         cin>>locs[i].x>>locs[i].y;
     }
     for(int i=0;i<n;i++){
         if(locs[i].y>d){
             cout<<"Case "<<count<<": "<<-1<<'\n';
             noans=1;
             break;
         }
     }
     //就只是因为这两行代码交换了位置，改了半天的错。。。

     if(noans==1){noans=0;continue;}
     if(n==1) {cout<<"Case "<<count<<": "<<1<<'\n';continue;}

     //就只是因为这两行代码交换了位置，改了半天的错。。。
     for(int i=0;i<n;i++){
         ranges[i]=f(locs[i], d);
     }
     sort(ranges.begin(),ranges.end(),cmp);
     int ans=1;
     float rad=ranges[0].r;
     for(int i=1;i<n;i++){
         if(rad<ranges[i].l){
             rad=ranges[i].r;
             ans++;
         }
     }
     cout<<"Case "<<count<<": "<<ans<<'\n';
 }
 return 0;
}
```





## M1760.袋子里最少数目的球

binary search, https://leetcode.cn/problems/minimum-limit-of-balls-in-a-bag/


二分答案

```c++
class Solution {
public:
    int minimumSize(vector<int>& nums, int maxOperations) {
        int l = 1, r = *max_element(nums.begin(), nums.end());
        int n = nums.size();
        while (l <= r) {
            int mid = l + (r - l) / 2;
            long long tmp = 0;
            for (int i = 0; i < n; i++) {
                tmp += (nums[i] / mid - 1);
                if (nums[i] % mid) tmp ++;
            }
            if (tmp <= maxOperations) r = mid - 1;
            else l = mid + 1;
        }
        return l;
    }
};
```



## M02299:Ultra-QuickSort

merge sort, http://cs101.openjudge.cn/practice/02299/

思路：问题等价于求逆序数，写一个递归函数即可，用时约25min（又去写bug去了）

```cpp
#include <iostream>
#include <vector>
using namespace std;

long long merge_count(vector<long long>& a, int left, int right) 
{
    if (left >= right) return 0;
    int mid = (left + right) / 2;
    long long count = 0;
    count += merge_count(a, left, mid);
    count += merge_count(a, mid + 1, right);

    vector<long long> temp;
    int i = left, j = mid + 1;
    while (i <= mid && j <= right) 
    {
        if (a[i] <= a[j]) temp.push_back(a[i++]);
        else 
        {
            temp.push_back(a[j++]);
            count += (mid - i + 1); // 左边剩下的都比a[j]大
        }
    }
    while (i <= mid) temp.push_back(a[i++]);
    while (j <= right) temp.push_back(a[j++]);
    for (int k = 0; k < temp.size(); k++) 
        a[left + k] = temp[k];
    return count;
}

int main() 
{
    int n;
    while (cin >> n && n != 0) 
    {
        vector<long long> a(n);
        for (int i = 0; i < n; i++) cin >> a[i];
        long long ans = merge_count(a, 0, n - 1);
        cout << ans << "\n";
    }
    return 0;
}


```





## M02749:分解因数

recursion, http://cs101.openjudge.cn/pctbook/M02749/

给出一个正整数a，要求分解成若干个正整数的乘积，即a = a1 * a2 * a3 * ... * an，并且1 < a1 <= a2 <= a3 <= ... <= an，问这样的分解的种数有多少。注意到a = a也是一种分解。

**输入**

第1行是测试数据的组数n，后面跟着n行输入。每组测试数据占1行，包括一个正整数a (1 < a < 32768)

**输出**

n行，每行输出对应一个输入。输出应是一个正整数，指明满足要求的分解的种数

样例输入

```
2
2
20
```

样例输出

```
1
4
```



代码解读和优化

```c++
# include <iostream>
using namespace std;

int count(short num, short mininum) {
    int cnt = 1;
    for (short i = mininum; i*i <= num; i++) {
        if (num % i) {continue;}
        // printf("i=%d", i);
        cnt += count(num / i, i);
        
    }
    return cnt;
}

int main() {
    int n, ans;
    short a;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> a;
        ans = 0;
        // cout << "check point 1" << endl;
        ans = count(a, 2);
        // cout << "check point 2" << endl;
        cout << ans << endl;
    }

    return 0;
}

```



## M02754 八皇后

思路：

- 枚举全排列 $p$，表示第 $i$ 行的皇后在第 $p_i$ 列。
- 我们可以用 $i + p_i, i - p_i$ 分别代表某一个皇后所在的左上-右下、左下-右上两条对角线。
- 分别判断有无重复的 $i + p_i, i - p_i$ 即可，笔者通过压位实现。
- 时间复杂度为 $O(N! \cdot N + nN)$，其中 $N = 8$。

代码：

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

int p[9], ans[93][9];

int main(){
	int cnt = 0;
	for (int i = 1; i <= 8; i++){
		p[i] = i;
	}
	do {
		int st1 = 0, st2 = 0;
		bool flag = true;
		for (int i = 1; i <= 8; i++){
			int x = i + p[i], y = i - p[i] + 8;
			if ((st1 >> x & 1) || (st2 >> y & 1)){
				flag = false;
				break;
			}
			st1 |= 1 << x;
			st2 |= 1 << y;
		}
		if (flag){
			cnt++;
			for (int i = 1; i <= 8; i++){
				ans[cnt][i] = p[i];
			}
		}
	} while (next_permutation(p + 1, p + 9));
	int n;
	cin >> n;
	for (int i = 1; i <= n; i++){
		int b;
		cin >> b;
		for (int j = 1; j <= 8; j++){
			cout << ans[b][j];
		}
		cout << endl;
	}
	return 0;
}
```



## M02783: Holiday Hotel

greedy, http://cs101.openjudge.cn/practice/02783/

### 

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

struct Node
{
    int d, c;
};

bool cmp(Node a, Node b)
{
    if (a.c != b.c)
        return a.c < b.c;
    return a.d < b.d;
}

int main()
{
    int n;
    while (scanf("%d", &n) && n)
    {
        Node hotel[10001];
        for (int i = 0; i < n; i++)
            scanf("%d%d", &hotel[i].d, &hotel[i].c);
        sort(hotel, hotel + n, cmp);

        int ans = 0;
        int min_d = 1e9 + 1;
        for (int i = 0; i < n; i++)
            if (hotel[i].d < min_d)
            {
                ans++;
                min_d = hotel[i].d;
            }
        printf("%d\n", ans);
    }
    return 0;
}
```





## M02786: Pell数列

dp, http://cs101.openjudge.cn/pctbook/M02786/

Pell数列a1, a2, a3, ...的定义是这样的，a1 = 1, a2 = 2, ... , an = 2 * an − 1 + an - 2 (n > 2)。
给出一个正整数k，要求Pell数列的第k项模上32767是多少。

**输入**

第1行是测试数据的组数n，后面跟着n行输入。每组测试数据占1行，包括一个正整数k (1 ≤ k < 1000000)。

**输出**

n行，每行输出对应一个输入。输出应是一个非负整数。

样例输入

```
2
1
8
```

样例输出

```
1
408
```





可以用**尾递归**优化。

将递归函数改写成尾递归形式的关键在于确保递归调用是函数的最后一个动作，并且所有必要的状态信息都通过参数传递。对于 `pell` 函数，可以使用两个辅助参数来保存前两个佩尔数的值，从而实现尾递归。

尾递归优化：C++ 编译器通常会优化尾递归，因此这种实现方式在处理大范围的 n 时通常不会遇到栈溢出的问题。Python 的官方解释器 CPython 并不支持尾递归优化。

```c++
#include <iostream>
#include <vector>

const int MOD = 32767;

// 尾递归函数
int pell_tail(int n, int a = 1, int b = 2) {
    if (n == 1) {
        return a;
    }
    if (n == 2) {
        return b;
    }
    return pell_tail(n - 1, b, (2 * b + a) % MOD);
}

int main() {
    const int MAX_N = 1000000;
    std::vector<int> dp(MAX_N, 0);

    int n;
    std::cin >> n;

    for (int i = 0; i < n; ++i) {
        int k;
        std::cin >> k;

        if (dp[k] != 0) {
            std::cout << dp[k] << std::endl;
        } else {
            dp[k] = pell_tail(k) % MOD;
            std::cout << dp[k] << std::endl;
        }
    }

    return 0;
}
```



## M03704: 扩号匹配问题

Stack, http://cs101.openjudge.cn/pctbook/M03704/

在某个字符串（长度不超过100）中有左括号、右括号和大小写字母；规定（与常见的算数式子一样）任何一个左括号都从内到外与在它右边且距离最近的右括号匹配。写一个程序，找到无法匹配的左括号和右括号，输出原来字符串，并在下一行标出不能匹配的括号。不能匹配的左括号用"$"标注,不能匹配的右括号用"?"标注.

**输入**

输入包括多组数据，每组数据一行，包含一个字符串，只包含左右括号和大小写字母，**字符串长度不超过100**
**注意：cin.getline(str,100)最多只能输入99个字符！**

**输出**

对每组输出数据，输出两行，第一行包含原始输入字符，第二行由"$","?"和空格组成，"$"和"?"表示与之对应的左括号和右括号不能匹配。

样例输入

```
((ABCD(x)
)(rttyy())sss)(
```

样例输出

```
((ABCD(x)
$$
)(rttyy())sss)(
?            ?$
```



题目里说“字符串长度不超过 100”，但 `cin.getline(str, 100)` 最多只能读 **99 个字符**，再加上 `'\0'`。

1. **数组开大一位**：用 `char str[101];` 和 `char accord[101];`，避免越界。
2. **getline 读 101**：`cin.getline(str, 101)`，这样能读入 100 个字符 + 末尾 `\0`。
3. **accord 初始化**：初始化时一定要覆盖到 `[0..length-1]`，不然可能带有上一次循环的数据。

```c++
#include <iostream>
#include <string>
#include <stack>
#include <cstring>
using namespace std;

int main() {
    char str[101]; // 开大一位，避免越界
    while (cin.getline(str, 101)) { // 改为 101
        int length = strlen(str);
        stack<int> err;
        char accord[101]; // 同样开大一位

        // 初始化 accord 数组
        for (int i = 0; i < length; i++) {
            accord[i] = ' ';
        }

        for (int i = 0; i < length; i++) {
            if (str[i] == '(') {
                err.push(i);
            }
            else if (str[i] == ')') {
                if (!err.empty()) {
                    err.pop();
                }
                else {
                    accord[i] = '?';
                }
            }
        }

        while (!err.empty()) {
            int position = err.top();
            err.pop();
            accord[position] = '$';
        }

        cout << str << endl;
        for (int i = 0; i < length; i++) {
            cout << accord[i];
        }
        cout << endl;
    }
    return 0;
}

```





## M04123: 马走日

backtracking, http://cs101.openjudge.cn/pctbook/M04123

马在中国象棋以日字形规则移动。

请编写一段程序，给定n*m大小的棋盘，以及马的初始位置(x，y)，要求不能重复经过棋盘上的同一个点，计算马可以有多少途径遍历棋盘上的所有点。

输入

第一行为整数T(T < 10)，表示测试数据组数。
每一组测试数据包含一行，为四个整数，分别为棋盘的大小以及初始位置坐标n,m,x,y。(0<=x<=n-1,0<=y<=m-1, m < 10, n < 10)

输出

每组测试数据包含一行，为一个整数，表示马能遍历棋盘的途径总数，0为无法遍历一次。

样例输入

```
1
5 4 0 0
```

样例输出

```
32
```



这个问题可以使用回溯算法来解决。需要模拟马的移动路径，并在每一步检查是否能访问到棋盘上的所有点。

**思路**：

1. 马的移动遵循“日”字形规则，可以向8个方向移动：上下左右及斜对角。
2. 使用回溯法遍历棋盘上的每一个点。每当访问一个新的点，就将其标记为已访问，且递归尝试访问下一个点。
3. 如果能够成功访问所有棋盘点（即移动的步数等于棋盘的大小），则记录为一个有效路径。
4. 避免重复访问，使用一个二维数组来标记每个点是否已访问过。

**步骤**：

1. 先初始化棋盘的大小和起始位置。
2. 使用回溯递归进行搜索。
3. 检查每一个方向的移动是否合法，并在合法时进行递归调用。
4. 当递归到达棋盘的所有点时，计数有效路径。



```cpp
#include <iostream>
#include <vector>

using namespace std;

const int dx[] = {-2, -1, 1, 2, 2, 1, -1, -2};  // 马的横向移动
const int dy[] = {1, 2, 2, 1, -1, -2, -2, -1};  // 马的纵向移动

// 回溯法计算遍历路径的数量
void dfs(int x, int y, int n, int m, int visited_count, vector<vector<bool>>& visited, int& result) {
    // 如果已经遍历了所有格子
    if (visited_count == n * m) {
        result++;
        return;
    }

    // 尝试所有8个方向
    for (int i = 0; i < 8; ++i) {
        int nx = x + dx[i];
        int ny = y + dy[i];
        
        // 如果新位置合法并且没有被访问过
        if (nx >= 0 && ny >= 0 && nx < n && ny < m && !visited[nx][ny]) {
            visited[nx][ny] = true;
            dfs(nx, ny, n, m, visited_count + 1, visited, result);
            visited[nx][ny] = false;  // 回溯
        }
    }
}

int main() {
    int T;
    cin >> T;  // 输入测试数据组数
    
    while (T--) {
        int n, m, x, y;
        cin >> n >> m >> x >> y;  // 输入棋盘大小和起始位置

        // 访问标记数组，初始化为false
        vector<vector<bool>> visited(n, vector<bool>(m, false));
        int result = 0;

        // 从起始位置(x, y)开始，标记为已访问
        visited[x][y] = true;
        dfs(x, y, n, m, 1, visited, result);

        // 输出结果
        cout << result << endl;
    }
    
    return 0;
}
```

代码解释：

1. **dx 和 dy 数组**：定义了马可以向8个方向移动的偏移量。
2. **dfs 函数**：使用递归进行回溯。参数包括当前坐标 `(x, y)`，棋盘大小 `n, m`，已访问的点数 `visited_count`，标记访问状态的 `visited` 数组，以及存储结果的 `result`。
3. **回溯过程**：每次尝试马的8个可能的移动，若合法且未访问过，就递归调用。
4. **主函数**：首先读取测试数据组数 `T`，然后每组数据执行一次 `dfs`，最终输出结果。

复杂度：

- 在最坏的情况下，每个位置都要遍历一次，且对于每个位置尝试8个方向的移动。最坏时间复杂度为 O(8^N)（其中 N 为棋盘的格数）。但由于棋盘大小限制，最大为 9x9，实际运行时会比这个上限快得多。



## M04135: 月度开销

binary search, http://cs101.openjudge.cn/pctbook/M04135/



思路：该题与上题本质上完全一致，均为假设答案然后二分查找，用时约10分钟（一遍ac)

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Solution 
{
    private:
        int N, M;
        vector<int> cost = {};
        int right = 0;
        int left = -1;
    public:
        void get()//输入数据，并设置二分查找的初始条件
        {
            cin >> N >> M;
            int x;
            for (int i = 0; i < N; i++)
            {
                cin >> x;
                right += x;
                if(i==0)
                {
                    left = x;
                }
                else
                {
                    if(x > left)
                    {
                        left = x;
                    }
                }
                cost.push_back(x);
            }
        }
        void solve()
        {
            int ans = 0;
           
            while (left <= right)
            {
                int mid = (right + left) / 2;
                int sum = 0;
                int num = 0;
                for (int x : cost)
                {
                    sum += x;
                    if (sum > mid)
                    {
                        num++;
                        sum = x;
                    }
                }
                num++;
                if (num > M)
                {
                    left = mid + 1;
                }
                else
                {
                    ans = mid;
                    right = mid - 1;
                }
            }
            cout << ans << endl;
        }
};


int main()
{
    Solution s;
    s.get();
    s.solve();
    return 0;
}

```



思路：二分答案

```c++
#include<iostream>
#include<algorithm>
using namespace std;
int n, m;
int a[100002];
int main() {
    cin >> n >> m;
    int l = 1, r = 0;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
        r += a[i];
        l = max(l, a[i]);
    }
    while (l <= r) {
        int mid = l + (r - l) / 2;
        int fajo = 0, tmp = 1;
        for (int i = 0; i < n; i ++) {
            if (fajo + a[i] > mid) {
                fajo = a[i];
                tmp ++;
            } else fajo += a[i];
        }
        if (tmp <= m) r = mid - 1;
        else l = mid + 1;
    }
    cout << l << endl;
    return 0;
}
```



## M06640: 倒排索引

data structures, http://cs101.openjudge.cn/pctbook/M06640/

思路：用 map<string, set<int>> 建立倒排索引：key 为单词，value 为出现该单词的文档编号集合。

```c++
#include <iostream>
#include <map>
#include <set>
#include <string>
using namespace std;

int main() {
    int N;
    cin >> N;

    map<string, set<int>> invertedIndex;

    for (int i = 1; i <= N; i++) {
        int c;
        cin >> c;
        for (int j = 0; j < c; j++) {
            string word;
            cin >> word;
            invertedIndex[word].insert(i);
        }
    }

    int M;
    cin >> M;
    while (M--) {
        string query;
        cin >> query;
        if (invertedIndex.count(query) == 0)
            cout << "NOT FOUND\n";
        else {
            bool first = true;
            for (int id : invertedIndex[query]) {
                if (!first) cout << " ";
                cout << id;
                first = false;
            }
            cout << "\n";
        }
    }
    return 0;
}
```



## M08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/pctbook/M08210

每年奶牛们都要举办各种特殊版本的跳房子比赛，包括在河里从一个岩石跳到另一个岩石。这项激动人心的活动在一条长长的笔直河道中进行，在起点和离起点L远 (1 ≤ *L*≤ 1,000,000,000) 的终点处均有一个岩石。在起点和终点之间，有*N* (0 ≤ *N* ≤ 50,000) 个岩石，每个岩石与起点的距离分别为*Di (0 < \*Di\* < \*L*)。*

在比赛过程中，奶牛轮流从起点出发，尝试到达终点，每一步只能从一个岩石跳到另一个岩石。当然，实力不济的奶牛是没有办法完成目标的。

农夫约翰为他的奶牛们感到自豪并且年年都观看了这项比赛。但随着时间的推移，看着其他农夫的胆小奶牛们在相距很近的岩石之间缓慢前行，他感到非常厌烦。他计划移走一些岩石，使得从起点到终点的过程中，最短的跳跃距离最长。他可以移走除起点和终点外的至多*M* (0 ≤ *M* ≤ *N*) 个岩石。

请帮助约翰确定移走这些岩石后，最长可能的最短跳跃距离是多少？



**输入**

第一行包含三个整数L, N, M，相邻两个整数之间用单个空格隔开。
接下来N行，每行一个整数，表示每个岩石与起点的距离。岩石按与起点距离从近到远给出，且不会有两个岩石出现在同一个位置。

**输出**

一个整数，最长可能的最短跳跃距离。

样例输入

```
25 5 2
2
11
14
17
21
```

样例输出

```
4
```

提示

在移除位于2和14的两个岩石之后，最短跳跃距离为4（从17到21或从21到25）。





```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

bool canAchieve(const vector<int>& rocks, int L, int M, int minDist) {
    int removed = 0;  // 记录移除的岩石数量
    int prev = 0;     // 记录上一个岩石的位置（起点）

    for (int i = 1; i < rocks.size(); i++) {
        if (rocks[i] - rocks[prev] < minDist) {
            removed++;  // 如果当前岩石与上一个岩石的距离小于 minDist，则移除当前岩石
            if (removed > M) {
                return false;  // 超过可移除的岩石数量，返回 false
            }
        } else {
            prev = i;  // 更新上一个岩石的位置
        }
    }
    return true;  // 可以满足要求
}

int maxMinJump(int L, int N, int M, const vector<int>& rocks) {
    // 先将岩石位置排序，并加入起点和终点
    vector<int> allRocks = {0};
    allRocks.insert(allRocks.end(), rocks.begin(), rocks.end());
    allRocks.push_back(L);

    int left = 0, right = L + 1;  // 二分查找的范围是 [0, L+1)

    int ans = -1;
    while (left < right) {
        int mid = (left + right) / 2;  // 取中间偏右的值
        if (canAchieve(allRocks, L, M, mid)) {
            ans = mid;    // 如果 mid 可行，记录答案并尝试更大的值
            left = mid + 1;
        } else {
            right = mid;  // 否则尝试更小的值
        }
    }
    return ans;
}

int main() {
    int L, N, M;
    cin >> L >> N >> M;

    vector<int> rocks(N);
    for (int i = 0; i < N; i++) {
        cin >> rocks[i];
    }

    // 计算并输出答案
    cout << maxMinJump(L, N, M, rocks) << endl;

    return 0;
}
```



> **`canAchieve` 函数**：
>
> - 这个函数的作用是判断是否可以通过移除至多 `M` 个岩石，确保最短跳跃距离不小于 `minDist`。
> - 从起点开始，依次检查岩石的位置。如果当前岩石与上一个岩石之间的距离小于 `minDist`，则认为这个岩石需要被移除。如果移除的岩石数超过了 `M`，则返回 `false`。否则，更新上一个岩石的位置。
>
> **`maxMinJump` 函数**：
>
> - 该函数使用二分查找来查找最大可能的最小跳跃距离。二分查找的范围是 `[0, L+1)`，每次计算中值 `mid`，并使用 `canAchieve` 判断是否可以通过移除岩石来实现该最小跳跃距离。如果可以，则更新答案，并尝试更大的 `mid` 值；否则，尝试更小的 `mid` 值。
>
> **`main` 函数**：
>
> - 从输入中读取参数 `L`（终点距离）、`N`（岩石数目）、`M`（最多可以移除的岩石数）以及岩石位置，最后调用 `maxMinJump` 函数计算并输出结果。
>
> 在 C++ 中，常常推荐使用常量引用（`const T&`）来传递对象，特别是当传递的是较大的数据结构（如 `vector`、`string`、`map` 等）时。这样既能提高性能，又能保证代码的清晰和安全。
>
> 
>
> **复杂度分析**：
>
> - **时间复杂度**：
>   - 二分查找的次数为 O(log L)。
>   - 每次检查是否可行的时间为 O(N)，因为我们要遍历岩石数组。
>   - 总的时间复杂度为 O(N * log L)。
> - **空间复杂度**：
>   - 主要使用一个数组 `allRocks` 来存储岩石位置和起点终点，空间复杂度为 O(N)。



## M12558: 岛屿周⻓

matrices, http://cs101.openjudge.cn/pctbook/M12558

```python
# 
#include <iostream>
#include <vector>

using namespace std;
int countp(vector<vector<int>> vec,int i, int j,int n,int m){
    int ret=0;
    if(j==0||vec[i][j-1]==0){
        ret++;
    }
    if(j==m-1||vec[i][j+1]==0){
        ret++;
    }
    if(i==0||vec[i-1][j]==0){
        ret++;
    }
    if(i==n-1||vec[i+1][j]==0){
        ret++;
    }
    return ret;
}

int main(){
    int n,m;
    cin>>n>>m;
    vector<vector<int>> vec(n, vector<int>(m,0));
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            cin>>vec[i][j];
        }
    }
    int ans=0;
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if(vec[i][j]==1){
                ans+=countp(vec,i,j,n,m);
            }
        }
    }
    cout<<ans<<'\n';
    return 0;
}
```



## M18164: 剪绳子

Heap, http://cs101.openjudge.cn/pctbook/M18164/

小张要将一根长度为L的绳子剪成N段。准备剪的绳子的长度为L1,L2,L3...,LN，未剪的绳子长度恰好为剪后所有绳子长度的和。 

每次剪断绳子时，需要的开销是此段绳子的长度。

比如，长度为10的绳子要剪成长度为2,3,5的三段绳子。长度为10的绳子切成5和5的两段绳子时，开销为10。再将5切成长度为2和3的绳子，开销为5。因此总开销为15。


请按照目标要求将绳子剪完最小的开销时多少。

已知，1<=N <= 20000，0<=Li<= 50000

**输入**

第一行：N，将绳子剪成的段数。
第二行：准备剪成的各段绳子的长度。

**输出**

最小开销

样例输入

```
3
2 3 5
```

样例输出

```
15
```

提示

tags: greedy, huffman

来源

cs101-2017 期末机考备选



```c++
#include <iostream>
#include <queue>
#include <functional>
#include <vector>
using namespace std;

long min_Heap(long arr[], long n)
{
    priority_queue<long, vector<long>, greater<long> > minHeap;
    for (int i = 0; i < n; i++)
    {
        // if (arr[i] != 0)
            // minHeap.push(arr[i]);
        minHeap.push(arr[i]);
    }
    long totalCost = 0;
    while (minHeap.size() > 1)
    {
        long first = minHeap.top();
        minHeap.pop();
        long second = minHeap.top();
        minHeap.pop();
        totalCost += first + second;
        minHeap.push(first + second);
    }
    return totalCost;
}

int main()
{
    int n;
    long arr[20001];
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        scanf("%ld", &arr[i]);
    }
    printf("%ld\n", min_Heap(arr, n));
    return 0;
}
```



## M18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/pctbook/M18211

思路：需要注意到可以存在没有被制造也没有被卖掉的图纸

```python
# 
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main(){
    int n,a;
    cin>>n;
    vector<int> vec;
    while(cin>>a){
        vec.push_back(a);
    }
    int m=vec.size()-1;
    vector<int> sum(m+1);
    sort(vec.begin(),vec.end());
    if(n<vec[0]){
        cout<<0;
        return 0;
    }
    sum[0]=vec[0];
    for(int i=1;i<=m;i++){
        sum[i]=sum[i-1]+vec[i];
    }
    int id=0;
    for(int j=0;j<m;j++){
        for(int i=0;i<=m;i++){
            if(sum[i]>n+sum[m]-sum[m-j]){
                id=max(id,i-j);
                break;
            }
        }
    }
    cout<<id<<'\n';
    return 0;
}
```



## M21554: 排队做实验

greedy, http://cs101.openjudge.cn/pctbook/M21554/

思路：cpp对pair的sort完美适配此题，不用重写cmp函数

```python
#include <iostream>
#include <vector>
#include <algorithm>
#include <iomanip>
using namespace std;

int main(){
    int n;
    cin>>n;
    vector<pair<int,int>> vec;
    for(int i=0;i<n;i++){
        int x;
        cin>>x;
        vec.push_back({x,i});
    }
    sort(vec.begin(),vec.end());
    float time=0;
    for(int i=0;i<n;i++){
        cout<<vec[i].second+1<<' ';
        time+=vec[i].first*(n-i-1);
    }
    cout<<'\n'<<fixed<<setprecision(2)<<time/n<<'\n';
    return 0;
}
```



## M23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555

要求用节省内存的方式实现，不能还原矩阵的方式实现。

思路：利用STL容器思路，对矩阵Y采用行优先的存储方式，实现稀疏矩阵的存储与计算，本题难度可以接受，算上思考时间使用20分钟左右。

```c++
#include <iostream>
#include <vector>
#include <map>
#include <tuple>

using namespace std;

int main() {
    int n, m1, m2;
    cin >> n >> m1 >> m2;

    vector<tuple<int, int, int>> X;
    for (int i = 0; i < m1; ++i) {
        int row, col, val;
        cin >> row >> col >> val;
        X.emplace_back(row, col, val);
    }

    vector<vector<pair<int, int>>> Y_rows(n);
    for (int i = 0; i < m2; ++i) {
        int row, col, val;
        cin >> row >> col >> val;
        Y_rows[row].emplace_back(col, val);
    }
    map<pair<int, int>, int> Z;
    for (const auto& x : X) {
        int i = get<0>(x);    
        int k = get<1>(x);    
        int a = get<2>(x);    
        for (const auto& y : Y_rows[k]) {
            int j = y.first;  
            int b = y.second; 
            Z[{i, j}] += a * b;
        }
    }
    for (const auto& entry : Z) {
        if (entry.second != 0) {
            cout << entry.first.first << " " << entry.first.second << " " << entry.second << endl;
        }
    }
    return 0;
}
```





## M24591:中序表达式转后序表达式

http://cs101.openjudge.cn/practice/24591/

思路：按照课上讲解，给符号设置等级即可，用时约20min，但是值得高兴的是一遍ac，我终于没在写bug了，代码也是十分高效，2ms

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Solution
{
    public:
        string s;
        vector<string> res;//以后缀表达式存储
        //给运算符设置等级
        bool isSymbal(char c)
        {
            return (c == '+' || c == '-' || c == '*' || c == '/' || c == '(' || c == ')');
        }
        int level(char c)
        {
            if (c == '*' || c == '/')
                return 2;
            if (c == '+' || c == '-')
                return 1;
            if (c == '(')
                return -1;
            return 0;
        }
        void get()
        {
            getline(cin, s);
        }
        void translate()
        {
            string temp="";
            vector<char> symbalStack;
            for (int i = 0; i < s.size(); i++)
            {
                if (isSymbal(s[i]))
                {
                    temp = "";
                    if (s[i] == '(')
                        symbalStack.push_back(s[i]);
                    else if (s[i] == ')')
                    {
                        while (!symbalStack.empty() && symbalStack.back() != '(')
                        {
                            temp = "";
                            temp += symbalStack.back();
                            symbalStack.pop_back();
                            res.push_back(temp);
                        }
                        symbalStack.pop_back();//去掉'('
                    }
                    else
                    {
                        while (!symbalStack.empty() && level(s[i]) <= level(symbalStack.back()))
                        {
                            temp = "";
                            temp += symbalStack.back();
                            symbalStack.pop_back();
                            res.push_back(temp);
                        }
                        symbalStack.push_back(s[i]);//将当前运算符入栈
                    }
                    temp = "";
                }
                else
                {
                    temp = "";
                    while (i < s.size() && !isSymbal(s[i]))
                    {
                        temp += s[i];
                        i++;
                    }
                    i--;//回退一步
                    res.push_back(temp);
                }
            }
            while (!symbalStack.empty())
            {
                temp = "";
                temp += symbalStack.back();
                symbalStack.pop_back();
                res.push_back(temp);
            }
        }
        void print()
        {
            for (int i = 0; i < res.size(); i++)
            {
                if (res[i]=="") continue;
                if(i) cout << " ";
                cout << res[i];
            }
            cout << endl;
        }
};


int main() 
{
    int N;
    cin >> N;
    cin.ignore();
    while (N--)
    {
        Solution s;
        s.get();
        s.translate();
        s.print();
    }
    return 0;
}

```



思路：我上网查了中序表达式转后序表达式的理论方法，自己编了程序。将数字直接加入结果，遇到运算符则将前面入栈的优先级不低于它的运算符全部弹出，随后将它入栈，最后把栈清空。每次调用.top()函数几乎都必须查找.empty()，不然就会RTE，需要注意。

```c++
#include<iostream>
#include<string>
#include<stack>
using namespace std;
int n;
string conv(string s) {
    stack<char> ss;
    string ans = "";
    for(int i = 0; i < s.size(); i ++) {
        if(s[i] == '(') ss.push('(');
        else if(s[i] == ')') {
            while(!ss.empty() && ss.top() != '(') {
                ans += ss.top();
                ans += ' ';
                ss.pop();
            }
            if(!ss.empty()) ss.pop();
        } else if(s[i] == '+' || s[i] == '-') {
            while(!ss.empty() && ss.top() != '(') {
                ans += ss.top();
                ans += ' ';
                ss.pop();
            }
            ss.push(s[i]);
        } else if(s[i] == '*' || s[i] == '/') {
            if(!ss.empty()) {
                while(ss.top() == '*' || ss.top() == '/') {
                    ans += ss.top();
                    ans += ' ';
                    ss.pop();
                    if(ss.empty()) break;
                }
            }
            ss.push(s[i]);
        }
        else {
            while((s[i] >= '0' && s[i] <= '9') || s[i] == '.') {
                ans += s[i];
                i ++;
            }
            i --;
            ans += ' ';
        }
    }
    while(!ss.empty()) {
        ans += ss.top();
        ans += ' ';
        ss.pop();
    }
    if(!ans.empty() && ans.back() == ' ')
        ans = ans.substr(0, ans.size() - 1);
    return ans;
}
string s;
int main() {
    cin >> n;
    for(int i = 0; i < n; i ++) {
        cin >> s;
        cout << conv(s) << endl;
    }
    return 0;
}
```





## 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/

思路：用字典的方式记录选票，在查询最大票数的同时记录答案数组

```c++
#include <iostream>
#include <map>
#include <vector>
using namespace std;

int main() {
    map<int, int> count;  // 选项编号 -> 票数
    int x;
    
    while (cin >> x) 
    {
        count[x]++;
    }
    
    int max_votes = 0;
    vector<int> ans_vec;
    for (auto& p : count) 
    {
        if (p.second > max_votes) 
        {
            max_votes = p.second;
            ans_vec.clear();
            ans_vec.push_back(p.first);
        }
        else if (p.second == max_votes)
        {
            ans_vec.push_back(p.first);
        }
    }
    
    bool isFirst = true;
    for (auto& ans : ans_vec)
    {
        if (!isFirst)
        {
            cout << " ";
        }
        cout << ans;
        isFirst = false;
    }

    return 0;
}

```



## M25570 洋葱

思路：

- 枚举 $1 \leq i \leq \lceil \frac{n}{2} \rceil$，令 $j = n - i + 1$，则第 $i$ 层包含以 $(i, i)$ 为左上角、以 $(j, j)$ 为右下角的正方形边框上的数。
- 对每一层，把这些数加起来，再取所有层中的最大值即可。
- 时间复杂度为 $O(n^2)$。

代码：

```cpp
#include <stdio.h>

int a[101][101];

int main(){
	int n, mid, ans = 0;
	scanf("%d", &n);
	mid = (n + 1) / 2;
	for (int i = 1; i <= n; i++){
		for (int j = 1; j <= n; j++){
			scanf("%d", &a[i][j]);
		}
	}
	for (int i = 1, j = n; i <= mid; i++, j--){
		int cur_ans = 0;
		for (int k = i; k <= j; k++){
			cur_ans += a[i][k];
		}
		for (int k = i + 1; k <= j; k++){
			cur_ans += a[k][i];
		}
		if (i < j){
			for (int k = i + 1; k <= j; k++){
				cur_ans += a[j][k];
			}
			for (int k = i + 1; k < j; k++){
				cur_ans += a[k][j];
			}
		}
		if (ans < cur_ans) ans = cur_ans;
	}
	printf("%d", ans);
	return 0;
}
```



## M27217: 有多少种合法的出栈顺序

http://cs101.openjudge.cn/practice/27217/



```c++
#include <bits/stdc++.h>
using namespace std;

vector<int> ans = {1};
vector<int> prime;
int n, m, expo[1000], num;
bool b[2001];

vector<int> multiply(const vector<int>& ans, int x) {
    vector<int> c;
    int carry = 0;
    for (int i = 0; i < ans.size() || carry; i++) {
        if (i < ans.size()) carry += ans[i] * x;
        c.push_back(carry % 10);
        carry /= 10;
    }
    return c;
}

// 计算 n! 中质数 p 的指数（勒让德公式）
int getExponent(int n, int p) {
    int count = 0;
    while (n > 0) {
        n /= p;
        count += n;
    }
    return count;
}

int main() {
    scanf("%d", &n);
    
    // 筛法求素数
    memset(b, true, sizeof(b));
    for (int i = 2; i <= n * 2; i++) {
        if (b[i]) {
            prime.push_back(i);
            for (int j = i * i; j <= n * 2; j += i) {
                b[j] = false;
            }
        }
    }
    m = prime.size();
    
    // 计算卡特兰数的质因数分解
    // C_n = (2n)! / (n! * (n+1)!)
    for (int i = 0; i < m; i++) {
        int p = prime[i];
        // 分子：(2n)!
        expo[i] += getExponent(2 * n, p);
        // 分母：n! 和 (n+1)!
        expo[i] -= getExponent(n, p);
        expo[i] -= getExponent(n + 1, p);
    }
    
    // 根据质因数分解计算结果
    for (int i = 0; i < m; i++) {
        for (int j = 1; j <= expo[i]; j++) {
            ans = multiply(ans, prime[i]);
        }
    }
    
    // 输出结果
    for (int i = ans.size() - 1; i >= 0; i--) {
        printf("%d", ans[i]);
    }
    return 0;
}
```



## M27300: 模型整理

sortings, AI, http://cs101.openjudge.cn/pctbook/M27300/

深度学习模型（尤其是大模型）是近两年计算机学术和业界热门的研究方向。每个模型可以用 “模型名称-参数量” 命名，其中参数量的单位会使用两种：M，即百万；B，即十亿。同一个模型通常有多个不同参数的版本。

例如，Bert-110M，Bert-340M 分别代表参数量为 1.1 亿和 3.4 亿的 Bert 模型，GPT3-350M，GPT3-1.3B 和 GPT3-175B 分别代表参数量为 3.5亿，13亿和 1750 亿的 GPT3 模型。

参数量的数字部分取值在 [1, 1000) 区间（一个 8 亿参数的模型表示为 800M 而非 0.8B，10 亿参数的模型表示为 1B 而非 1000M）。

计算机专业的学生小 A 从网上收集了一份模型的列表，他需要将它们按照名称归类排序，并且同一个模型的参数量从小到大排序，生成 “模型名称: 参数量1, 参数量2, ...” 的列表。请你帮他写一个程序实现。

**输入**

第一行为一个正整数 n（n <= 1000），表示有 n 个待整理的模型。

接下来 n 行，每行一个 “模型名称-参数量” 的字符串。模型名称是字母和数字的混合。

**输出**

每行一个 “模型名称: 参数量1, 参数量2, ...” 的字符串，符号均为英文符号，模型名称按字典序排列，参数量按从小到大排序。

样例输入

```
5
GPT-1.3B
Bert-340M
GPT-350M
Bert-110M
GPT-175B
```

样例输出

```
Bert: 110M, 340M
GPT: 350M, 1.3B, 175B
```

提示

tags: string, sort

来源

2023fall zyn



```c++
#include <iostream>
#include <algorithm>
#include <string>
#include <vector>
using namespace std;

class Model {
private:
    string raw;       // 原始参数量字符串，比如 "350M" 或 "1.3B"
    double value;     // 换算成 B 的数值，方便比较

public:
    string name;      // 模型名公开

    // 构造函数：接收 "模型名-参数量" 字符串
    Model(const string& fullname) {
        size_t pos = fullname.find('-');
        name = fullname.substr(0, pos);
        raw = fullname.substr(pos + 1);

        char unit = raw.back();
        double num = stod(raw.substr(0, raw.size() - 1));
        if (unit == 'M') {
            value = num / 1000.0;  // 百万 → 十亿
        } else {
            value = num;           // 已经是 B
        }
    }

    // 提供获取原始参数量字符串的方法
    string getRaw() const {
        return raw;
    }

    // 重载 < 运算符用于排序
    bool operator<(const Model& other) const {
        if (name == other.name) {
            return value < other.value;
        }
        return name < other.name;
    }
};

int main() {
    int n;
    cin >> n;
    vector<Model> models;
    models.reserve(n);

    for (int i = 0; i < n; i++) {
        string s;
        cin >> s;
        models.emplace_back(s);
    }

    sort(models.begin(), models.end());

    cout << models[0].name << ": " << models[0].getRaw();
    for (int i = 1; i < n; i++) {
        if (models[i].name == models[i - 1].name) {
            cout << ", " << models[i].getRaw();
        } else {
            cout << "\n" << models[i].name << ": " << models[i].getRaw();
        }
    }
    cout << "\n";

    return 0;
}
```



> **reserve** → 提前分配内存
>
> **emplace_back** → 直接构造对象，避免不必要拷贝
>
> `struct` = 数据结构（默认 public）
>
> `class` = 面向对象（默认 private）
>
> 功能上完全等价，选择哪种主要看**语义**：
>
> - 你只是存数据 → struct 更清晰
> - 你需要封装/隐藏/继承 → class 更合适
>
> 如果用 `class`：
>
> ```c++
> class Model {
>     string name;
>     double value;
> };
> ```
>
> - 默认是 **private**
> - 你必须提供 getter 或者把成员改成 `public`：
>
> ```c++
> class Model {
> public:
>     string name;
>     double value;
> };
> ```



思路：核心在数据的接收上，排序可以直接sort()，只要数据接收正确就可以，用时约10分钟

```c++
#include <iostream>
#include <sstream>
#include <map>
#include <vector>
#include <algorithm>


using namespace std;

// 把参数量字符串转成数值 (统一为实际参数个数)
long parseParam(const string& s) 
{
    double num = stod(s.substr(0, s.size() - 1));
    char unit = s.back();
    if (unit == 'M') return (long)(num * 1e6 + 0.5);
    if (unit == 'B') return (long)(num * 1e9 + 0.5);
    return 0; 
}

int main() 
{
    int n;
    cin >> n;
    //以模型名称为键，参数量为值
    map<string, vector<pair<long , string>>> models;

    for (int i = 0; i < n; i++) 
    {
        string input;
        cin >> input;

        // 拆分 模型名称 和 参数量
        size_t pos = input.find('-');
        string name = input.substr(0, pos);
        string param = input.substr(pos + 1);

        long value = parseParam(param);
        models[name].push_back({ value, param });
    }

    // 按名称字典序输出
    for (auto& temp : models) 
    {
        string name = temp.first;
        auto& vec = temp.second;

        // 按数值排序
        sort(vec.begin(), vec.end());

        cout << name << ": ";
        for (int i = 0; i < vec.size(); i++) 
        {
            if (i > 0) cout << ", ";
            cout << vec[i].second;
        }
        cout << "\n";
    }

    return 0;
}

```



## M28664: 验证身份证号 

http://cs101.openjudge.cn/pctbook/M28664/



思路：打表，优化时间复杂度

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    int c[17] = {7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2};
    char ref[11] = {'1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2'};
    cin >> n;
    string ID;
    for (int i = 0; i < n; i++)
    {
        cin >> ID;
        int check = 0;
        for (int j = 0; j < ID.length() - 1; j++)
            check += (ID[j] - '0') * c[j];
        int l = check % 11;
        char end = ID.back();
        if (ref[l] == end)
            cout << "YES" << endl;
        else
            cout << "NO" << endl;
    }
    return 0;
}
```





## M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/pctbook/M28700/



思路：模拟+打表，其实也可以纯打表做。一开始没想到映射方法，直接纯模拟，发现很难实现，然后打了个表就豁然开朗了

```cpp
#include <iostream>
using namespace std;

string intToRoman(int input)
{
    string roman[] = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
    int num[] = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
    string res;
    for (int i = 0; i < 13; i++)
        while (input >= num[i])
        {
            input -= num[i];
            res += roman[i];
        }
    return res;
}

int RomanToint(string input)
{
    int num[256];
    num['I'] = 1; num['V'] = 5; num['X'] = 10;
    num['L'] = 50; num['C'] = 100; num['D'] = 500; num['M'] = 1000;
    int res = num[input.back()];
    for (int i = input.length() - 2; i >= 0; i--)
        if (num[input[i]] >= num[input[i + 1]])
            res += num[input[i]];
        else
            res -= num[input[i]];
    return res;
}
int main()
{
    string input;
    cin >> input;
    if (input[0] >= '0' && input[0] <= '9')
        cout << intToRoman(stoi(input)) << endl;
    else
        cout << RomanToint(input) << endl;
    return 0;
}
```



## M29917: 牛顿迭代法

implementation, http://cs101.openjudge.cn/practice/29917/

```cpp
#include<bits/stdc++.h>
using namespace std;
double const c=1e-6;
double a,x1,x2;
int cnt;
int main(){
    while(scanf("%lf",&a)!=EOF){
        cnt=0;
        x1=1;
        while(1){
            cnt++;
            x2=x1-(x1*x1-a)/(2*x1);
            if(abs(x1-x2)<=c)
                break;
            x1=x2;
        }
        printf("%d %.2lf\n",cnt,x2);
    }
    return 0;
}
```



## M29918: 求亲和数

implementation, http://cs101.openjudge.cn/practice/29918/

```cpp
#include<bits/stdc++.h>
using namespace std;
int n,a[100005];
int main(){
    scanf("%d",&n);
    for(int i=1;i<=n;i++){
        for(int j=2;j<=n/i;j++)
            a[i*j]+=i;
    }
    for(int i=1;i<=n;i++){
        if(a[i]<=n && a[a[i]]==i && i<a[i])
            printf("%d %d\n",i,a[i]);
    }
    return 0;
}
```



## M29949: 贪婪的哥布林

greedy, http://cs101.openjudge.cn/practice/29949/

```cpp
#include<bits/stdc++.h>
using namespace std;
int n,m;
double ans;
struct A{
    int v,w;
    double p;
}a[105];
bool cmp(A &x,A &y){
    return x.p>y.p;
}
int main(){
    scanf("%d %d",&n,&m);
    for(int i=1;i<=n;i++){
        scanf("%d %d",&a[i].v,&a[i].w);
        a[i].p=1.0*a[i].v/a[i].w;
    }
    sort(a+1,a+1+n,cmp);
    for(int i=1;i<=n;i++){
        if(a[i].w<=m){
            ans+=a[i].v;
            m-=a[i].w;
        }
        else{
            ans+=m*a[i].p;
            break;
        }
    }
    printf("%.2lf",ans);
    return 0;
}
```



## M29954 逃离紫罗兰监狱

思路：

- 某一时刻的状态可以描述为 $(x, y, cnt)$，表示位于 $(x, y)$ 且现在已经使用了 $cnt$ 次闪现术。
- 则接下来可以消耗一单位时间移动到 $(x, y, cnt) \to (x + dx, y + dy, cnt + [mp_{x + dx, y + dy} = \text{\#}])$，当且仅当：

$$
\begin{cases}
|dx| + |dy| = 1 \\
0 \leq x + dx < r, 0 \leq y + dy < c \\
cnt + [mp_{x + dx, y + dy} = \text{\#}] \leq k
\end{cases}
$$

- 进而不难抽象为一个图论模型：边权均为 $1$ 的分层图单源最短路问题，起点为 $(x_S, y_S, 0)$，所有可能的终点为 $(x_E, y_E, \_)$。
- bfs 即可。时间复杂度为 $O(rck)$。

代码：

```cpp
#include <iostream>
#include <queue>

using namespace std;

struct Node {
	int x;
	int y;
	int cnt;
	int dis;
	
	Node(int _x, int _y, int _cnt, int _dis) : x(_x), y(_y), cnt(_cnt), dis(_dis) {}
};

bool vis[100][100][11];
string mp[100];
queue<Node> q;

void update(int x, int y, int cnt, int dis, int k){
	if (cnt <= k && !vis[x][y][cnt]){
		vis[x][y][cnt] = true;
		q.push(Node(x, y, cnt, dis));
	}
}

int main(){
	int r, c, k, sx = -1, sy;
	cin >> r >> c >> k;
	for (int i = 0; i < r; i++){
		cin >> mp[i];
		if (sx == -1){
			for (int j = 0; j < c; j++){
				if (mp[i][j] == 'S'){
					sx = i;
					sy = j;
					break;
				}
			}
		}
	}
	update(sx, sy, 0, 0, 0);
	while (!q.empty()){
		Node cur = q.front();
		q.pop();
		if (mp[cur.x][cur.y] == 'E'){
			cout << cur.dis;
			return 0;
		}
		for (int i : {-1, 1}){
			int new_x = cur.x + i;
			if (new_x >= 0 && new_x < r) update(new_x, cur.y, cur.cnt + (mp[new_x][cur.y] == '#' ? 1 : 0), cur.dis + 1, k);
		}
		for (int i : {-1, 1}){
			int new_y = cur.y + i;
			if (new_y >= 0 && new_y < c) update(cur.x, new_y, cur.cnt + (mp[cur.x][new_y] == '#' ? 1 : 0), cur.dis + 1, k);
		}
	}
	cout << -1;
	return 0;
}
```





# Tough

## T02488: A Knight's Journey

backtracking, http://cs101.openjudge.cn/practice/02488/

思路：dfs暴力求解，没有一点剪枝，一遍ac，用时约30min

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <sstream>
#include <algorithm>
using namespace std;

const vector<pair<int,int>> directions = {{-2,-1},{-2,1},{-1,-2},{-1,2},{1,-2},{1,2},{2,-1},{2,1}};

class Solution
{
	public:
		int row , col;
		vector<vector<bool>> isVisited;
		bool isFind;
		vector<pair<int,int>> path;
		int step;
		int curX, curY;

		void initialize()
		{
			cin >> col >> row;
			isVisited.resize(row,vector<bool>(col,false));
			isFind = false;
			path.clear();
            step = 0;
			curX = curY = 0;
		}

		bool isInBoard(int x, int y)
		{
			return (x >= 0 && x < row && y >= 0 && y < col);
		}

		void findPath( )
		{
            if(isFind) return;
            if(!isInBoard(curX,curY)) return;
            if(isVisited[curX][curY]) return;
			if (step == row * col - 1)
			{
                isFind = true;
                path.push_back({curX,curY});
                return;
			}
           
			for (auto dir : directions)
			{
				isVisited[curX][curY] = true;
				path.push_back({ curX,curY });
                curX += dir.first;
                curY += dir.second;
                step++;
                findPath();
                if (isFind) return;
				step--;
				curX -= dir.first;
                curY -= dir.second;
				path.pop_back();
				isVisited[curX][curY] = false;
			}
			
		}

		void solve()
		{
			for (int curX = 0; curX < row; curX++)
			{
				for (int curY = 0; curY < col; curY++)
				{
					if(isFind) return;
                    findPath();
				}
			}
		}

		void printAns()
		{
			solve();
			if (isFind)
			{
				for (auto p : path)
					cout << char(p.first + (int)'A') << p.second + 1;
			}
			else
				cout << "impossible" ;
		}
};

int main()
{
	int n;
    cin >> n;
	for (int i = 0; i < n; i++)
	{
		Solution s;
        s.initialize();
		if (i) cout << endl;
		cout <<"Scenario #"<< i + 1 << ":" << endl;
        s.printAns();
        cout << endl;
	}
	return 0;
}

```



## T29947: 校门外的树又来了

http://cs101.openjudge.cn/practice/29947/



```cpp
#include<bits/stdc++.h>
using namespace std;
#define pii pair<int,int>
int L,n,r=-1,sum;
pii d[105];
bool cmp(pii &x,pii &y){
    if(x.first==y.first)
        return x.second>y.second;
    return x.first<y.first;
}
int main(){
    scanf("%d %d",&L,&n);
    for(int i=1;i<=n;i++)
        scanf("%d %d",&d[i].first,&d[i].second);
    sort(d+1,d+1+n,cmp);
    d[0].first=-1;
    for(int i=1;i<=n;i++){
        if(d[i].first==d[i-1].first || d[i].second<=r)
            continue;
        if(r>=d[i].first)
            sum+=d[i].second-r;
        else
            sum+=d[i].second-d[i].first+1;
        r=d[i].second;
    }
    printf("%d",L+1-sum);
    return 0;
}
```



## T27256: 当前队列中位数

思路：

- 题意即维护一个队列，有如下三种操作：(1) 在队尾添加；(2) 弹出队首；(3) 查询队列中的数集的中位数。
- 现在把队列的壳去掉，问题变为对一个**可重集合**的操作：有如下三种操作：(1) 插入一个数；(2) 删除一个数；(3) 查询集合的中位数。
- 思路 A：最好写的做法就是用 vector 维护一个**有序**数列，每次 lower_bound 到插入 / 删除位置并用 vector.insert / vector.erase 执行相应操作。Python 玩家的话可以使用 bisect。但这样做的时间复杂度为 $O(n^2)$，本不应该通过。~~虽然我赛时过了 /youl~~
- 思路 B：考虑“中位数”的性质：注意到我们总是可以将原集合分成两个集合 $\mathbb{P}, \mathbb{Q}$，其中：(1) $\mathbb{P}$ 中的元素都**不大于**中位数，$\mathbb{Q}$ 中的元素都**不小于**中位数；(2) $|\mathbb{P}| - |\mathbb{Q}| \in \{0, 1\}$。分别用大根堆和小根堆维护两个集合。
- 插入时，不难得知插入到哪个集合中可以维持性质 (1)，插入完成后若不再满足 (2)，则将其中一方的堆顶弹出，并放到另一方的堆顶。
- 删除时，打个标记，并维护 $|\mathbb{P}|, |\mathbb{Q}|$ 的实际值即可。
- 查询时，若 $|\mathbb{P}| = |\mathbb{Q}|$ 则答案为两个堆顶的平均数，若 $|\mathbb{P}| - |\mathbb{Q}| = 1$ 则答案为 $\mathbb{P}$ 的堆顶。
- 思路 C：注意到平衡树可以胜任以上三种操作（第三种是求第 k 小的特殊情况）。当然，这题 $n$ 并不太大，写值域线段树也可以通过。

代码（思路 A）：

```cpp
#include <algorithm>
#include <queue>
#include <vector>
#include <cstdio>

using namespace std;

char op[7];
queue<int> q;
vector<int> v;

void insert(int x){
	v.insert(lower_bound(v.begin(), v.end(), x), x);
}

void erase(int x){
	v.erase(lower_bound(v.begin(), v.end(), x));
}

int main(){
	int n, len = 0;
	scanf("%d", &n);
	for (int i = 1; i <= n; i++){
		scanf("%s", op);
		if (op[0] == 'a'){
			int x;
			scanf("%d", &x);
			len++;
			q.push(x);
			insert(x);
		} else if (op[0] == 'd'){
			len--;
			erase(q.front());
			q.pop();
		} else {
			if (len % 2 == 1){
				printf("%d\n", v[len / 2]);
			} else {
				int sum = v[len / 2] + v[len / 2 - 1];
				printf("%d", sum / 2);
				if (sum % 2 == 1) printf(".5");
				printf("\n");
			}
		}
	}
	return 0;
}
```



代码（思路 C，值域线段树）：

```cpp
#include <queue>
#include <cstdio>

using namespace std;

struct Node {
	int ls;
	int rs;
	int size;
};

int root = 0, id = 0;
char op[7];
Node tree[3100001];
queue<int> q;

void update(int x){
	tree[x].size = tree[tree[x].ls].size + tree[tree[x].rs].size;
}

void add(int &x, int l, int r, int pos, int val){
	if (x == 0) x = ++id;
	if (l == r){
		tree[x].size += val;
		return;
	}
	int mid = (l + r) >> 1;
	if (pos <= mid){
		add(tree[x].ls, l, mid, pos, val);
	} else {
		add(tree[x].rs, mid + 1, r, pos, val);
	}
	update(x);
}

int get_kth_number(int x, int l, int r, int k){
	if (l == r) return l;
	int ls = tree[x].ls;
	if (k <= tree[ls].size) return get_kth_number(ls, l, (l + r) >> 1, k);
	return get_kth_number(tree[x].rs, ((l + r) >> 1) + 1, r, k - tree[ls].size);
}

int main(){
	int n, len = 0;
	scanf("%d", &n);
	for (int i = 1; i <= n; i++){
		scanf("%s", op);
		if (op[0] == 'a'){
			int x;
			scanf("%d", &x);
			len++;
			q.push(x);
			add(root, 0, 1e9, x, 1);
		} else if (op[0] == 'd'){
			len--;
			add(root, 0, 1e9, q.front(), -1);
			q.pop();
		} else {
			if (len % 2 == 1){
				printf("%d\n", get_kth_number(root, 0, 1e9, (len + 1) / 2));
			} else {
				int sum = get_kth_number(root, 0, 1e9, len / 2) + get_kth_number(root, 0, 1e9, len / 2 + 1);
				printf("%d", sum / 2);
				if (sum % 2 == 1) printf(".5");
				printf("\n");
			}
		}
	}
	return 0;
}
```



## 



# Codeforces



## 20B. Equation

math, 2000, https://codeforces.com/problemset/problem/20/B



```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    double a, b, c;
    scanf("%lf%lf%lf", &a, &b, &c);
    if (a == 0)
    {
        if (b == 0)
            if (c == 0)
                printf("-1\n");
            else 
                printf("0\n");
        else
            printf("1\n%lf\n", -c / b);
        return 0;
    }
    double delta = b * b - 4 * a * c;
    if (delta < 0)
        printf("0\n");
    else if (delta == 0)
        printf("1\n%lf\n", -b / (2 * a));
    else if (a > 0)
        printf("2\n%lf\n%lf\n", (-b - sqrt(delta)) / (2 * a), (-b + sqrt(delta)) / (2 * a));
    else
        printf("2\n%lf\n%lf\n", (-b + sqrt(delta)) / (2 * a), (-b - sqrt(delta)) / (2 * a));
    return 0;
}
```





## 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



```python
# #include <iostream>
#include <queue>
using namespace std;

int main(){
    int a,b,h;
    h=0;
    cin>>a>>b;
    priority_queue<int> pq;
    while(a--){
        int x;
        cin>>x;
        if(x>=0) continue;
        pq.push(-x);
        h-=x;
    }
    int ans=0;
    if(b>pq.size()) cout<<h<<'\n';
    else{
        for(int i=0;i<b;i++){
            ans+=pq.top();
            pq.pop();
        }
        cout<<ans<<'\n';
    }
    return 0;
}

```



思路：按字典序选择起点与扩展顺序，保证得到的是全局字典序最小的完整骑士巡游路径；

```c++
#include <bits/stdc++.h>
using namespace std;

struct Pos { int r, c; }; 

string label(int r, int c) { // 转成例如 "A1"
    string s;
    s.push_back(char('A' + c));
    s += to_string(r + 1);
    return s;
}

int dr[8] = { 2, 2, 1, 1,-1,-1,-2,-2};
int dc[8] = { 1,-1, 2,-2, 2,-2, 1,-1};

bool dfs(int p, int q, Pos u, int step, vector<vector<int>>& vis, vector<Pos>& path) {
    if (step == p * q) return true;


    vector<Pos> cand;
    for (int k = 0; k < 8; ++k) {
        int nr = u.r + dr[k], nc = u.c + dc[k];
        if (nr >= 0 && nr < p && nc >= 0 && nc < q && !vis[nr][nc]) {
            cand.push_back({nr, nc});
        }
    }
    sort(cand.begin(), cand.end(), [&](const Pos& a, const Pos& b){
        // 先按列字母，再按行数字
        if (a.c != b.c) return a.c < b.c;
        return a.r < b.r;
    });

    for (auto v : cand) {
        vis[v.r][v.c] = 1;
        path.push_back(v);
        if (dfs(p, q, v, step + 1, vis, path)) return true;
        path.pop_back();
        vis[v.r][v.c] = 0;
    }
    return false;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n; 
    if (!(cin >> n)) return 0;
    for (int tc = 1; tc <= n; ++tc) {
        int p, q; // p 行(数字 1..p), q 列(字母 A..)
        cin >> p >> q;

        cout << "Scenario #" << tc << ":\n";

        bool found = false;
       
        for (int c0 = 0; c0 < q && !found; ++c0) {
            for (int r0 = 0; r0 < p && !found; ++r0) {
                vector<vector<int>> vis(p, vector<int>(q, 0));
                vector<Pos> path;
                vis[r0][c0] = 1;
                path.push_back({r0, c0});
                if (dfs(p, q, {r0, c0}, 1, vis, path)) {
                    // 输出路径（拼接标签）
                    string out;
                    for (auto &pt : path) out += label(pt.r, pt.c);
                    cout << out << "\n\n";
                    found = true;
                }
            }
        }
        if (!found) {
            cout << "impossible\n\n";
        }
    }
    return 0;
}
```





## 58A. Chat room

greedy, strings, 1000, http://codeforces.com/problemset/problem/58/A


思路：逐个检查即可，用时约10min

```c++
#include <iostream>

using namespace std;

const string standard = "hello";

bool check(string input)
{
	int p = 0;
	for (auto i : input)
	{
		if (i == standard[p])  p++;
		if (p == standard.length()) return true;
	}
    return false;
}

int main()
{
	string input;
	cin >> input;
	if (check(input)) 
		cout << "YES";
	else
        cout << "NO";
    return 0;
}
```



## 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A

思路：遇到元音continue，其余情况变成小写然后输出.和该字母，用时较长（处理输出次数太多），但代码较短
，用时约15min（没注意到y也算元音）

```c++
#include <iostream>

using namespace std;

class solution
{
    private:
        string str;
    public:
        bool isVowels(char c)
        {
            return (c == 'a' || c == 'y'|| c == 'e' || c == 'i' || c == 'o' || c == 'u' 
                || c == 'A' || c == 'Y' || c == 'E' || c == 'I' || c == 'O' || c == 'U');
        }

        bool isUppercase(char c)
        {
            return (c >= 'A' && c <= 'Z');
        }
        void getStr()
        {
            cin >> str;
        }
        void outPut()
        {
            for (auto i : str)
            {
                if (isVowels(i)) continue;
                if (isUppercase(i)) i = tolower(i);
                cout << '.' << i;
            }
        }
};



int main()
{
	solution ans;
    ans.getStr();
    ans.outPut();
    return 0;
}
```



思路：

遍历字符串，将字母转为小写；

若是元音（a, o, y, e, u, i）则跳过；

否则在结果中添加 '.' 和该字母；

最后输出处理后的字符串。

代码：

```c++
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main() {
    string s, result;
    cin >> s;

    for (char c : s) {
        c = tolower(c);
        if (c == 'a' || c == 'o' || c == 'y' || c == 'e' || c == 'u' || c == 'i')
            continue; // 跳过元音
        result += '.';
        result += c;
    }

    cout << result << endl;
    return 0;
}
```





## 158B. Taxi

*special problem, greedy, implementation, 1100,  https://codeforces.com/problemset/problem/158/B



```cpp
#include <iostream>
using namespace std;

int main()
{
    int n, input;
    cin >> n;
    int s[5] = {0};
    for (int i = 0; i < n; i++)
    {
        cin >> input;
        s[input]++;
    }
    int taxi = 0;
    
    taxi += s[4];

    taxi += s[3];
    s[1] -= s[3];
    if (s[1] < 0)
        s[1] = 0;
    
    taxi += s[2] / 2 + s[2] % 2;
    if (s[2] % 2 != 0)
        s[1] -= 2;
    if (s[1] < 0)
        s[1] = 0;
    
    taxi += s[1] / 4;
    if (s[1] % 4 > 0)
        taxi++;
    
    cout << taxi << endl;
    return 0;
}

```



## 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A



思路：怎么全是一个pq能解决的问题

```python
#include <iostream>
#include <queue>
using namespace std;

int main(){
    priority_queue<int> pq;
    int a,h=0;
    cin>>a;
    while(a--){
        int x;
        cin>>x;
        h+=x;
        pq.push(x);
    }
    int amount=0;
    int num=0;
    while(num<=h/2&&!pq.empty()){
        num+=pq.top();
        pq.pop();
        amount++;
    }
    cout<<amount<<'\n';
    return 0;
}

```





## 230B. T-primes

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B



```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6;
int T;
long long a;
bool np[N + 5]; // np[i] 表示 i 是否为合数（非质数）

// 检查 a 是否为完全平方数且其平方根是奇数质数
bool check() {
    if (a == 4) return 1;  // 特殊情况：4 = 2^2，但 2 是偶数质数，但题目可能允许？这里返回 true

    if (a == 1 || a % 2 == 0) return 0;  // 奇数且不为 1 和偶数

    long long s = sqrt(a);
    if (s * s != a || np[s]) return 0;  // 不是完全平方数 或 平方根不是质数
    return 1;
}

int main() {
    // 使用埃拉托斯特尼筛法预处理出所有小于等于 N 的合数
    for (int i = 3; i * i <= N; i += 2) {
        if (np[i]) continue;
        for (int j = i; j * i <= N; j += 2) {
            np[j * i] = 1;
        }
    }

    // 输入测试次数
    cin >> T;
    while (T--) {
        cin >> a;
        if (check()) {
            printf("YES\n");
        } else {
            printf("NO\n");
        }
    }

    return 0;
}
```



思路：确实体会到了cpp处理大整数太麻烦了。。。

```python
#include<iostream>
#include<cmath>
#include<unordered_set>
#include<vector>
using namespace std;

int main(){
    int t;
    vector<bool> check(1000001,true);
    unordered_set<int> st;
    cin>>t;
    for(int i=2;i<=1000000;i++){
        if(check[i]) {
            st.insert(i);
            if((long long)i*i<1000000){
                for(long long j=i*i;j<=1000000;j+=i){
                    check[j]=false;
                }
            }
        }
    }
    while(t--){
        long long a;
        cin>>a;
        long long c = sqrt(a);
        if(c*c==a && st.find(c)!=st.end()){cout<<"YES"<<'\n';}
        else {cout<<"NO"<<'\n';}
    }
    return 0;
}
```







## 313B. Ilya and Queries

https://codeforces.com/problemset/problem/313/B

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main()
{
    string str;
    cin >> str;
    int n;
    cin >> n;
    vector<int> pre(str.length(), 0);
    for (int i = 1; i < str.length(); i++)
        pre[i] = pre[i - 1] + (str[i] == str[i - 1] ? 1 : 0);
    while (n--)
    {
        int l, r;
        cin >> l >> r;
        cout << pre[r - 1] - pre[l - 1] << endl;
    }
    return 0;
}
```





## 339B Xenia and Ringroad

implementation, 1000, https://codeforces.com/problemset/problem/339/B

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n, m;
    scanf("%d%d", &n, &m);
    int curr = 1;
    long long step = 0;
    for (int i = 0; i < m; i++)
    {
        int a;
        scanf("%d", &a);
        if (curr <= a)
            step += a - curr;
        else
            step += n - curr + a;
        curr = a;
    }
    printf("%I64d\n", step);
    return 0;
}
```



## 508A. Pasha and Pixels

https://codeforces.com/problemset/problem/508/A

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int n, m, k;
    scanf("%d%d%d", &n, &m, &k);
    bool matrix[1002][1002] = {0};
    for (int i = 0; i < k; i++)
    {
        int x, y;
        scanf("%d%d", &x, &y);
        matrix[x][y] = true;
        if ((matrix[x + 1][y] && matrix[x + 1][y + 1] && matrix[x][y + 1]) || (matrix[x + 1][y] && matrix[x + 1][y - 1] && matrix[x][y - 1]) || (matrix[x][y + 1] && matrix[x - 1][y + 1] && matrix[x - 1][y]) || (matrix[x][y - 1] && matrix[x - 1][y - 1] && matrix[x - 1][y]))
        {
            cout << i + 1 << endl;
            return 0;
        }
    }
    cout << 0 << endl;
    return 0;
}
```



## 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main()
{
    int n;
    cin >> n;
    vector<pair<long long, long long>> range;
    while (n--)
    {
        long long x, h;
        cin >> x >> h;
        range.emplace_back(x - h, x + h);
    }

    long long currR = -1e9;
    int ans = 0;
    for (int i = 0; i < range.size(); i++)
    {
        if (i == 0 || range[i].first > currR)
        {
            ans++;
            currR = (range[i].first + range[i].second) / 2;
        }
        else if (i == range.size() - 1 || range[i].second < (range[i + 1].first + range[i + 1].second) / 2)
        {
            ans++;
            currR = range[i].second;
        }
        else
            currR = (range[i].first + range[i].second) / 2;
    }
    cout << ans << endl;
    return 0;
}
```



## 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B



```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 300005, inf = 1e9;
int T, n, a, b, min1, min2;
long long sum1, sum2;

int main() {
    scanf("%d", &T);
    while (T--) {
        sum1 = sum2 = 0;
        min1 = min2 = inf;
        scanf("%d", &n);
        for (int i = 1; i <= n; i++) {
            scanf("%d", &a);
            sum1 += 1ll * a;
            min1 = min(min1, a);
        }
        for (int i = 1; i <= n; i++) {
            scanf("%d", &b);
            sum2 += 1ll * b;
            min2 = min(min2, b);
        }
        printf("%lld\n", min(1ll * min1 * n + sum2, 1ll * min2 * n + sum1));
    }
    return 0;
}
```





# LeetCode



## E20.有效的括号

stack, https://leetcode.cn/problems/valid-parentheses/

思路：括号匹配问题 简单的一个栈数据结构即可

```python
class Solution {
public:
    bool isValid(string s) {
        //括号匹配问题 简单的一个栈数据结构即可
        stack<char> st;
        int n=s.size();
        int flag=0;
        for(int i=0;i<n;i++){
            //左进右出
            if(s[i]=='('||s[i]=='{'||s[i]=='['){
                st.push(s[i]);
            }else{
                if(st.empty()) return false;
                char tmp=st.top();
                if(s[i]==')'&&tmp!='('){
                    return false;
                }else if(s[i]==']'&&tmp!='['){
                    return false;
                }else if(s[i]=='}'&&tmp!='{'){
                    return false;
                }
                st.pop();

            }
        }
        if(st.empty())
            return true;
        else return false;
    }
};
```



思路：注意到括号的匹配与栈的后入先出是一样的，因此用栈的思路去解决，很顺利，用时约10min

```cpp
class Solution 
{
public:
    bool isValid(string s) 
    {
        map<char, char> map = { {'(', ')'}, {'[', ']'}, {'{', '}'} };
        vector<char> stack;
        for (char c : s)
        {
            if (map.find(c) != map.end())//左括号，入栈
            {
                stack.push_back(c);
            }
            else
            {
                if (stack.empty() || c != map[stack.back()])//右括号，栈为空或者不匹配，返回false
                {
                    return false;
                }
                stack.pop_back();//右括号，匹配，出栈
            }
        }
        return stack.empty();
        
    }
};
```





## M46.全排列

backtracking, https://leetcode.cn/problems/permutations/

思路：写一个回溯型的递归就行，非常简单，用时约15min

```cpp
class Solution 
{
public:
    void backtrack(vector<int>& nums, vector<int>& current, vector<bool>& used, vector<vector<int>>& ans)
    {
        if (current.size() == nums.size())
        {
            ans.push_back(current);
            return;
        }
        for (int i = 0; i < nums.size(); i++)
        {
            if (used[i]) continue;
            used[i] = true;
            current.push_back(nums[i]);
            backtrack(nums, current, used, ans);
            //回溯
            current.pop_back();
            used[i] = false;
        }
    }
    vector<vector<int>> permute(vector<int>& nums) 
    {
        vector<vector<int>> ans;
        
        vector<int> current;
        vector<bool> used(nums.size(), false);
        backtrack(nums, current, used, ans);
        return ans;

    }
};
```



思路：经典全排列构造思路,那就是依次将每个数字放在开头,然后考虑后面的从而进行递归,时间复杂度是n!

```c++
class Solution {
public:
    void backtrack(vector<vector<int>>& res, vector<int>& nums, int first, int len){
        // 所有数都填完了
        if (first == len) {
            res.emplace_back(nums);
            return;
        }
        for (int i = first; i < len; ++i) {
            // 动态维护数组
            swap(nums[i], nums[first]);
            // 继续递归填下一个数
            backtrack(res, nums, first + 1, len);
            // 撤销操作
            swap(nums[i], nums[first]);
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int> > res;
        backtrack(res, nums, 0, (int)nums.size());
        return res;
    }
};


```





## M78.子集

backtracking, https://leetcode.cn/problems/subsets/

思路：和 `M46.全排列` 相似，将上题递归函数的“== nums.size()”换成for(int k = 0 ; k < nums.size() ; k++) 即可，其余对应稍加修改即可。



思路：最棒的思路就是利用二进制关系,每个数字只有0/1两个状态,某一个子集中,那么这个子集就一共有2^n个,然后利用二进制枚举来实现,同样也可以进行递归考虑问题,也是每个位置进行0/1两种状态dfs,然后记录长度输出即可

```c++
class Solution {
public:
    vector<int> t;
    vector<vector<int>> ans;

    vector<vector<int>> subsets(vector<int>& nums) {
        int n = nums.size();
        for (int mask = 0; mask < (1 << n); ++mask) {
            t.clear();
            for (int i = 0; i < n; ++i) {
                if (mask & (1 << i)) {
                    t.push_back(nums[i]);
                }
            }
            ans.push_back(t);
        }
        return ans;
    }
};


```



## M79.单词搜索

回溯，https://leetcode.cn/problems/word-search/

思路：最暴力的就是直接dfs每一个点,然后进行判断即可,每个点dfs,长度为K(单词长度),然后一个个来找

```c++
class Solution {
public:
    bool check(vector<vector<char>>& board, vector<vector<int>>& visited, int i, int j, string& s, int k) {
        if (board[i][j] != s[k]) {
            return false;
        } else if (k == s.length() - 1) {
            return true;
        }
        visited[i][j] = true;
        vector<pair<int, int>> directions{{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        bool result = false;
        for (const auto& dir: directions) {
            int newi = i + dir.first, newj = j + dir.second;
            if (newi >= 0 && newi < board.size() && newj >= 0 && newj < board[0].size()) {
                if (!visited[newi][newj]) {
                    bool flag = check(board, visited, newi, newj, s, k + 1);
                    if (flag) {
                        result = true;
                        break;
                    }
                }
            }
        }
        visited[i][j] = false;
        return result;
    }

    bool exist(vector<vector<char>>& board, string word) {
        int h = board.size(), w = board[0].size();
        vector<vector<int>> visited(h, vector<int>(w));
        for (int i = 0; i < h; i++) {
            for (int j = 0; j < w; j++) {
                bool flag = check(board, visited, i, j, word, 0);
                if (flag) {
                    return true;
                }
            }
        }
        return false;
    }
};

```





## M102.二叉树的层序遍历

bfs, https://leetcode.cn/problems/binary-tree-level-order-traversal/


思路：利用bfs完成层序遍历，学过二叉树的前中后遍历之后就不算是很困难，但是还是不是很熟练，时间也是大多花在了代码优化，花费半个小时

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result; 
        if (root == nullptr) {
            return result;
        }
        
        queue<TreeNode*> q; 
        q.push(root); 
        while (!q.empty()) {
            int levelSize = q.size(); 
            vector<int> currentLevel; 
            
            for (int i = 0; i < levelSize; ++i) {
                TreeNode* node = q.front(); 
                q.pop();
                currentLevel.push_back(node->val); 
                if (node->left != nullptr) {
                    q.push(node->left);
                }
                if (node->right != nullptr) {
                    q.push(node->right);
                }
            }
            
            result.push_back(currentLevel); 
        }
        
        return result;
    }
};
```





## E118.杨辉三角

dp, https://leetcode.cn/problems/pascals-triangle/

思路：写两个循环即可

```cpp
class Solution 
{
public:
    vector<vector<int>> generate(int numRows) 
    {
        vector<vector<int>> ans;
        for (int i = 0; i < numRows; i++)
        {
            ans.push_back(vector<int>());
            for (int j = 0; j < i + 1; j++)
            {
                if (j == 0 || j == i)
                    ans[i].push_back(1);
                else
                    ans[i].push_back(ans[i - 1][j - 1] + ans[i - 1][j]);
            }
        }
        return ans;

    }
};
```



## M131.分割回文串

dp, backtracking, https://leetcode.cn/problems/palindrome-partitioning/

思路：

dp预先计算字符串所有子串的回文信息并存储在DP表中，然后通过回溯算法进行深度优先搜索，在每一步利用DP表快速判断子串是否回文来指导分割决策，当搜索到字符串末尾时将当前分割方案加入结果集，用时一个小时（还是不熟练，小错误不断，太菜了）

代码：

```c++
class Solution {
public:
    vector<vector<string>> partition(string s) {
        int n = s.size();
        vector<vector<bool>> dp(n, vector<bool>(n, false));
        for (int i = n - 1; i >= 0; --i) {
            for (int j = i; j < n; ++j) {
                if (i == j) {
                    dp[i][j] = true;  
                } else if (j == i + 1) {
                    dp[i][j] = (s[i] == s[j]);  
                } else {
                    dp[i][j] = (s[i] == s[j]) && dp[i + 1][j - 1]; 
                }
            }
        }

        vector<vector<string>> result;
        vector<string> path;  
        backtrack(s, 0, dp, path, result);
        return result;
    }
    void backtrack(const string& s, int start, const vector<vector<bool>>& dp, 
                   vector<string>& path, vector<vector<string>>& result) {
        if (start == s.size()) {  
            result.push_back(path);
            return;
        }
        for (int end = start; end < s.size(); ++end) {
            if (dp[start][end]) {  
                path.push_back(s.substr(start, end - start + 1));  
                backtrack(s, end + 1, dp, path, result);           
                path.pop_back();  
            }
        }
    }
};
```



## M146.LRU缓存

hash table, doubly-linked list, https://leetcode.cn/problems/lru-cache/

思路：先自己写一个链表，用字典存储键值和其对应的地址，然后完成函数即可，加上学习，用时约30min

```cpp
struct Listnode
{
    int key, value;
    Listnode* next, * prev;
    Listnode(int k, int v) :key(k), value(v), next(NULL), prev(NULL) {}
    Listnode() :key(0), value(0), next(NULL), prev(NULL) {}
};

class LRUCache 
{
private:
    unordered_map<int, Listnode*> map;
    Listnode* head, * tail;
    int capacity, size;
public:
    
    LRUCache(int capacity)
    {
        this->capacity = capacity;
        this->size = 0;
        head = new Listnode();//伪头节点
        tail = new Listnode();
        head->next = tail;
        tail->prev = head;
    }

    int get(int key)
    {
        if (map.find(key) == map.end())
            return -1;
        Listnode* node = map[key];
        toHead(node);
        return node->value;
    }

    void put(int key, int value)
    {
        if (map.find(key) == map.end())//不存在
        {
            Listnode* node = new Listnode(key, value);
            map[key] = node;
            addNodeToHead(node);
            size++;
            if (size > capacity)//超出容量
            {
                map.erase(tail->prev->key);
                removeTail();
                size--;
            }
        }
        else//存在
        {
            Listnode* node = map[key];
            node->value = value;
            toHead(node);
        }
    }

    void removeNode(Listnode* node)
    {
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }

    void addNodeToHead(Listnode* node)
    {
        node->prev = head;
        node->next = head->next;
        head->next->prev = node;
        head->next = node;
    }

    void toHead(Listnode* node)
    {
        removeNode(node);
        addNodeToHead(node);
    }

    void removeTail()
    {
        Listnode* node = tail->prev;
        removeNode(node);
    }
};
```



## E160.相交链表

two pinters, https://leetcode.cn/problems/intersection-of-two-linked-lists/

思路：一路存地址即可，用时约20min

```cpp
class Solution 
{
public:
    ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) 
	{
        map<ListNode*, int> m;
		while (headA != NULL)
		{
            m[headA] = 1;
            headA = headA->next;

		}
		while (headB != NULL)
		{
            if (m.find(headB) != m.end())
                return headB;
            headB = headB->next;
		}
        return NULL;

    }
};
```



## M200.岛屿数量

dfs, bfs, https://leetcode.cn/problems/number-of-islands/ 

思路：通过dfs，bfs遍历算法，在遇到陆地('1')时进行连通分量标记并计数，利用搜索过程将相邻陆地沉没为水域从而避免重复统计。

```c++
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        if (grid.empty()) return 0; 
        int m = grid.size();     
        int n = grid[0].size();     
        int count = 0;             
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == '1') { 
                    count++;             
                    dfs(grid, i, j, m, n); 
                }
            }
        }
        return count;
    }

private:
    void dfs(vector<vector<char>>& grid, int i, int j, int m, int n) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] != '1') {
            return;
        }
        grid[i][j] = '0'; 
        dfs(grid, i - 1, j, m, n);
        dfs(grid, i + 1, j, m, n); 
        dfs(grid, i, j - 1, m, n); 
        dfs(grid, i, j + 1, m, n); 
    }
};
```



## E206.反转链表

three pinters, recursion, https://leetcode.cn/problems/reverse-linked-list/

思路：直接写就行，0ms，一遍过，用时约10min

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* cur = head;
        while (cur) 
        {
            ListNode* nxt = cur->next;
            cur->next = prev;
            prev = cur;
            cur = nxt;
        }
        head = prev;
        return head;
    }
};
```



## M234.回文链表

linked list, https://leetcode.cn/problems/palindrome-linked-list/

<mark>请用快慢指针实现</mark> `O(1)` 空间复杂度。


思路：用快慢指针找出链表中间的地址，反转中间往后的链表，再查即可，用时约15Min

```cpp
class Solution 
{
public:
    //中间指针
    ListNode* midnote(ListNode* head)
    {
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast->next != nullptr && fast->next->next != nullptr)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
    //反转中间后面的
    void reverse(ListNode* head)
    {
        ListNode* pre = nullptr;
        ListNode* cur = head->next;
        while (cur != nullptr)
        {
            ListNode* temp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = temp;
        }
        head->next = pre;
    }

    bool isPalindrome(ListNode* head) 
    {
        ListNode* mid = midnote(head);
        reverse(mid);
        while (head != nullptr && mid->next != nullptr)
        {
            if (head->val != mid->next->val)
                return false;
            head = head->next;
            mid = mid->next;
        }
        return true;
    }
};
```





## E283.移动零

stack, two pinters, https://leetcode.cn/problems/move-zeroes/

思路：双指针处理即可,主要是考虑到各自的位置进行swap

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        //要保证相对顺序不变 双指针来记录
        //左指针指向处理好的尾部  右指针指向待处理的头部
        //要实现把0都放到最后面 只需要每次左指针指向处理好的第一个0,右指针把非0转移即可
        int l=0;
        int r;
        for(r=0;r<nums.size();r++){
            if(nums[r]!=0){
                swap(nums[l],nums[r]);
                l++;
            }
        }
    }
};
```





思路：只需要将0放到最后即可

```cpp
class Solution
{
public:
    void moveZeroes(vector<int>& nums)
    {
        int n = nums.size();
        vector<int> temp;
        for (int i = 0; i < n; i++)
        {
            if (nums[i] != 0)
                temp.push_back(nums[i]);
        }
        for (int i = 0; i < n; i++)
        {
            if (i < temp.size())
                nums[i] = temp[i];
            else
                nums[i] = 0;
        }

    }
};
```



## E1078: Bigram分词

https://leetcode.cn/problems/occurrences-after-bigram/

思路：注意到text是以空格分割的，因此可以用流函数来构建wordList，再寻找符合条件的答案插入到结果列表即可

```cpp
class Solution
{
public:
    vector<string> findOcurrences(string text, string first, string second)
    {
        vector<string> wordList;
        stringstream ss(text);
        string word;
        while (ss >> word) 
        {
            wordList.push_back(word);
        }

        vector<string> result;
        for (int i = 0; i < wordList.size() - 2; i++)
        {
            if (wordList[i] == first && wordList[i + 1] == second)
            {
                result.push_back(wordList[i + 2]);
            }
        }
        return result;
    }
};
```



思路：分词后遍历即可

```c++
class Solution {
public:
    vector<string> findOcurrences(string text, string first, string second) {
        //遍历即可
        //将text分词
        vector<string> dic;
        string tmp="";
        for(int i=0;i<text.size();i++){
            if(text[i]!=' ') tmp+=text[i];
            else{
                dic.push_back(tmp);
                tmp="";
            }
        }
        dic.push_back(tmp);
        vector<string> ans;
        for(int i=0;i<dic.size();i++){
            if(dic[i]==first){
                if(i+2<dic.size()&&dic[i+1]==second){
                    ans.push_back(dic[i+2]);
                }
            }
        }
        return ans;
    }
};
```



## M1123.最深叶节点的最近公共祖先

dfs, https://leetcode.cn/problems/lowest-common-ancestor-of-deepest-leaves/

思路：如果直接想还挺难,但是如果考虑到二叉树的通用递归思路,那么就可以有很好的解决方法,即利用递归的思路

如果左子树更深，最深叶节点在左子树中，我们返回 {左子树深度 + 1，左子树的 lca 节点}
如果右子树更深，最深叶节点在右子树中，我们返回 {右子树深度 + 1，右子树的 lca 节点}
如果左右子树一样深，左右子树都有最深叶节点，我们返回 {左子树深度 + 1，当前节点}

```c++
class Solution {
public:
    pair<TreeNode*, int> f(TreeNode* root) {
        if (!root) {
            return {root, 0};
        }

        auto left = f(root->left);
        auto right = f(root->right);

        if (left.second > right.second) {
            return {left.first, left.second + 1};
        }
        if (left.second < right.second) {
            return {right.first, right.second + 1};
        }
        return {root, left.second + 1};

    }

    TreeNode* lcaDeepestLeaves(TreeNode* root) {
        return f(root).first;
    }
};

```





## M1760.袋子里最少数目的球

binary search, https://leetcode.cn/problems/minimum-limit-of-balls-in-a-bag/




思路：一开始的想法是将最多的一个袋子拆成 m + n 暴力回溯，显然太暴力了，后来看了题解，反向设置最终目标加二分法才是最合适的，用时约30分钟

```c++
class Solution 
{
public:
    int minimumSize(vector<int>& nums, int maxOperations) 
    {
        int left = 1, right = *max_element(nums.begin(), nums.end());
        int ans = 0;
        while (left <= right)
        {
            int mid = (right + left) / 2;
            long long op = 0;
            for(int x : nums)
            {
                op += (x - 1) / mid;
            }
            if (op <= maxOperations)
            {
                ans = mid;
                right = mid - 1;
            }
            else
                left = mid + 1;
        }
        return ans;
    }
};

```





# Other



## 画矩形

https://programming.pku.edu.cn/problem/7f89efad1537471fae528e9c88601ee6/

根据参数，画出矩形。

**关于输入**

输入由多行组成，每行四个参数：前两个参数为整数，依次代表矩形的高和宽（高不少于3行，宽不少于5行）；第三个参数是一个字符，表示用来画图的矩形符号；第四个参数为1或0，0代表空心，1代表实心。
当用户输入0时表示输入结束。

**关于输出**

输出画出的图形

例子输入

```
6 5 * 1
7 7 @ 0
0
```

例子输出

```
*****
*****
*****
*****
*****
*****
@@@@@@@
@     @
@     @
@     @
@     @
@     @
@@@@@@@
```

提示信息

对于一个题里有多组测试数据的题目，可以读取一组测试数据后直接输出该组的运行结果，不必把多组测试数据储存起来后一起输出。



从标准输入读取多行，每行格式如 `H W C F`，当遇到单独一行 `0` 时结束。`F` 为 `1` 表示实心，`0` 表示空心。输出各个矩形，矩形之间不额外插入空行（与题目样例一致）。

```python
import sys

def draw_rectangle(h, w, ch, filled):
    # h >= 3, w >= 5（题目保证），ch 为单字符，filled 为 0/1
    line_full = ch * w
    if filled:
        for _ in range(h):
            print(line_full)
    else:
        print(line_full)                 # 第一行
        middle = ch + ' ' * (w - 2) + ch
        for _ in range(h - 2):
            print(middle)               # 中间行
        print(line_full)                 # 最后一行

def main():
    data = sys.stdin.read().splitlines()
    for line in data:
        s = line.strip()
        if not s:
            continue
        if s == '0':
            break
        parts = s.split()
        if len(parts) < 4:
            # 忽略格式错误的行（也可抛错），这里跳过
            continue
        try:
            h = int(parts[0])
            w = int(parts[1])
            ch = parts[2][0] if parts[2] else '#'
            filled = int(parts[3]) != 0
        except:
            continue
        draw_rectangle(h, w, ch, filled)

if __name__ == "__main__":
    main()
```





