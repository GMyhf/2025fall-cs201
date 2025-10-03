#  Problems in OJ, CF & others

*Updated 2025-10-03 23:05 GMT+8*
 *Compiled by Hongfei Yan (2025 Fall)*



> Logs:
>
> 2025/10/2: 加了些 数算 【张梓康 元培】、【潘彦璋 物院】同学的CPP代码。
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

思路：直接递归就可以，代码中采用了记录已访问过元素的值的方式，使运行时间降到了1ms，用时约10min

```c++
#include <iostream>

using namespace std;

int T[100] = {0, 1, 1, 2};

int T_n(int n)
{
    	if (n > 3 && T[n] == 0)
    	{
    		T[n] = T_n(n-1)+T_n(n-2)+T_n(n-3);
    	}
    	if (n == 0) return 0;
		if(n==1||n==2) return 1;
        return T[n];
}

int main()
{
	int n;
	cin >> n;
    cout << T_n(n);
}
```



## 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/

思路：
直接判断 i 和 n-i 是不是质数即可，不过令我震惊的是完全没有任何优化耗时竟然只有1ms，这就是c++的速度吗？用时约10min

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
    for (int i = 2; i <= n; i++)
    {
        if (isPrime(i) && isPrime(n - i))
        {
            cout << i << " " << n - i;
            return 0;
        }
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



## 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/

思路：用字典的方式记录选票，在查询最大票数的同时记录答案数组，非常简单，用时约10min

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





# Codeforces



## 58A. Chat room

greedy, strings, 1000, http://codeforces.com/problemset/problem/58/A


思路：
逐个检查即可，用时约10min


代码：

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





# LeetCode



## E20.有效的括号

stack, https://leetcode.cn/problems/valid-parentheses/

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



## M78.子集

backtracking, https://leetcode.cn/problems/subsets/

思路：和 `M46.全排列` 相似，将上题递归函数的“== nums.size()”换成for(int k = 0 ; k < nums.size() ; k++) 即可，其余对应稍加修改即可。



## E118.杨辉三角

dp, https://leetcode.cn/problems/pascals-triangle/

思路：写两个循环即可,用时约10min

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





## E283.移动零

stack, two pinters, https://leetcode.cn/problems/move-zeroes/


思路：只需要将0放到最后即可，用时约10min

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

思路：
注意到text是以空格分割的，因此可以用流函数来构建wordList，再寻找符合条件的答案插入到结果列表即可，用时约10min

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





