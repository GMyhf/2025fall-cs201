#  Problems in OJ, CF & LeetCode in CPP

*Updated 2026-04-07 14:29 GMT+8*
 *Compiled by Hongfei Yan (2025 Fall)*



> Logs:
>
> 2025fall～2026spring:  【张梓康 元培】、【潘彦璋 物院】、【李沁遥25医学预科办】、【王乾旭 信科】、【刘思哲 25工学院】、【张真铭25元陪】、【李傲挺 物院】、【罗锐，25工学院，】、【海博治 城市与环境学院】、【黄浩展 25工学院】、【江昊中 25数院】、【姚博骞 25物院】、【黄宇曦 地球与空间科学学院】、【竺景琦 25工学院】、【郑志远 25数院】、【赵林 数院】等同学的CPP代码。
>
> 鉴于每学期都有同学偏好C++编程，也开始提供C++题解支持。



# OJ简单

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



## E02039: 反反复复	

matrix, http://cs101.openjudge.cn/practice/02039/

【黄宇曦 地球与空间科学学院】思路：比较简单，没什么好说的。

```cpp
#include <bits/stdc++.h>

using namespace std;

#define all(x) begin(x), end(x)
#define sz(x) (int) (x).size()

using i64 = long long;
using u64 = unsigned long long;
using i128 = __int128_t;
using u128 = __uint128_t;
using pii = pair<int, int>;
using vi = vector<int>;
using usi = unordered_set<int>;

int main() {
    cin.tie(nullptr)->sync_with_stdio(false);
    int n;
    cin >> n;
    string str;
    cin >> str;
    string ans = "";
    for (int i = 0; i < n; i++) {
        for (int j = 0; j * n + i < str.size(); j++) {
            // cout << (j * n + (j % 2 == 0 ? i : n - i - 1)) << '\n';
            ans.push_back(str[j * n + (j % 2 == 0 ? i : n - i - 1)]);
        }
    }
    cout << ans << '\n';
    return 0;
}
```



## E02092: Grandpa is Famous	

implementation, http://cs101.openjudge.cn/practice/02092/


【黄宇曦 地球与空间科学学院】思路：比较简单，感觉乱搞也能过。

```cpp
#include <bits/stdc++.h>

using namespace std;

#define all(x) begin(x), end(x)
#define sz(x) (int) (x).size()

using i64 = long long;
using u64 = unsigned long long;
using i128 = __int128_t;
using u128 = __uint128_t;
using pii = pair<int, int>;
using vi = vector<int>;
using usi = unordered_set<int>;

int main() {
    cin.tie(nullptr)->sync_with_stdio(false);
    int n, m;
    while (cin >> n >> m) {
        if (!n && !m)
            return 0;
        vi cnt(10005, 0);
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                int t;
                cin >> t;
                cnt[t]++;
            }
        }
        auto tmp = cnt;
        sort(all(tmp), [](int a, int b) { return a > b; });

        for (int i = 1; i <= 10000; i++) {
            if (cnt[i] == tmp[1])
                cout << i << ' ';
        }
        cout << '\n';
    }
    return 0;
}
```





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



```cpp
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



```cpp
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

```cpp
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

```cpp
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



## E02734:十进制到八进制 

http://cs101.openjudge.cn/practice/02734

思路：直接除8取余，个人感觉最快捷

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int a;
    cin >> a;  
    string octal;  
    while (a > 0) {
        int remainder = a % 8;  
        octal = to_string(remainder) + octal; 
        a = a / 8;  
    }

    cout << octal << endl;  
    return 0;
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



```cpp
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

```cpp
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

```cpp
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

```cpp
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



## M04089: 电话号码

思路：

- 建立 Trie 树，插入一个字符串时需要检查是否存在存在其前缀或后缀。
- 对于“前缀”，只需在每个节点上记录 `end` 表示是否存在以之结尾的字符串；对于后缀，只需记录当前字符串结尾的 Trie 节点是否为新增的节点即可。

```cpp
#include <stdio.h>
#include <string.h>

struct Node {
	bool end;
	int nxt[10];
	
	void clear(){
		end = false;
		for (int i = 0; i <= 9; i++){
			nxt[i] = 0;
		}
	}
};

int id;
char phone[12];
Node tree[100002];

void init(){
	id = 0;
	tree[0].clear();
}

bool insert(char s[]){
	int len = strlen(&s[1]), x = 0;
	bool nsuffix, nprefix = true;
	for (int i = 1; i <= len; i++){
		int ch = s[i] - '0';
		if (i == len) nsuffix = tree[x].nxt[ch] == 0;
		if (tree[x].nxt[ch] == 0){
			id++;
			tree[x].nxt[ch] = id;
			tree[id].clear();
		}
		x = tree[x].nxt[ch];
		nprefix &= !tree[x].end;
	}
	tree[x].end = true;
	return nprefix && nsuffix;
}

int main(){
	int t;
	scanf("%d", &t);
	for (int i = 1; i <= t; i++){
		int n;
		bool ans = true;
		scanf("%d", &n);
		init();
		for (int j = 1; j <= n; j++){
			scanf("%s", &phone[1]);
			ans &= insert(phone);
		}
		if (ans){
			printf("YES\n");
		} else {
			printf("NO\n");
		}
	}
	return 0;
}
```



## E07218: 献给阿尔吉侬的花束

思路：bfs 求 01 最短路即可。

- **注意有多组数据，记得清空队列！**

```cpp
#include <iostream>
#include <queue>

using namespace std;

struct Node {
	int x;
	int y;
	
	Node(int _x, int _y) : x(_x), y(_y) {}
};

int dis[200][200];
string mp[200];
queue<Node> q;

void init(int r, int c){
	while (!q.empty()) q.pop();
	for (int i = 0; i < r; i++){
		for (int j = 0; j < c; j++){
			dis[i][j] = 0x7fffffff;
		}
	}
}

void find(int r, int c, int &x, int &y, char ch){
	for (int i = 0; i < r; i++){
		for (int j = 0; j < c; j++){
			if (mp[i][j] == ch){
				x = i;
				y = j;
				return;
			}
		}
	}
}

int main(){
	int t;
	cin >> t;
	for (int i = 1; i <= t; i++){
		int r, c, sx, sy;
		bool flag = false;
		cin >> r >> c;
		init(r, c);
		for (int j = 0; j < r; j++){
			cin >> mp[j];
		}
		find(r, c, sx, sy, 'S');
		dis[sx][sy] = 0;
		q.push(Node(sx, sy));
		while (!q.empty()){
			Node cur = q.front();
			q.pop();
			if (mp[cur.x][cur.y] == 'E'){
				flag = true;
				cout << dis[cur.x][cur.y] << endl;
				break;
			}
			for (int j : {-1, 1}){
				int nx = cur.x + j;
				if (nx >= 0 && nx < r && mp[nx][cur.y] != '#' && dis[nx][cur.y] == 0x7fffffff){
					dis[nx][cur.y] = dis[cur.x][cur.y] + 1;
					q.push(Node(nx, cur.y));
				}
			}
			for (int j : {-1, 1}){
				int ny = cur.y + j;
				if (ny >= 0 && ny < c && mp[cur.x][ny] != '#' && dis[cur.x][ny] == 0x7fffffff){
					dis[cur.x][ny] = dis[cur.x][cur.y] + 1;
					q.push(Node(cur.x, ny));
				}
			}
		}
		if (!flag) cout << "oop!" << endl;
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

```cpp
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



## E19943:图的拉普拉斯矩阵

http://cs101.openjudge.cn/practice/19943/



```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m;
    cin >> n >> m;
    vector<vector<int>> L(n, vector<int>(n, 0));
    while (m--)
    {
        int a, b;
        cin >> a >> b;
        L[a][a]++;
        L[b][b]++;
        L[a][b]--;
        L[b][a]--;
    }

    for (auto i : L)
    {
        for (auto j : i)
            cout << j << ' ';
        cout << '\n';
    }
    return 0;
}
```



## E20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/

思路：当 n = 0、1、2 时，直接返回对应的初始值。
从 T3 开始，每一项等于前三项之和。可以用三个变量循环更新，节省空间。

```cpp
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





```cpp
#include <array>
#include <iostream>

auto main() -> int {
  int n;
  std::array<int, 31> T = {0, 1, 1};
  std::cin >> n;
  if (n >= 1 && n <= 2) {
    std::cout << T[n] << "\n";
    return 0;
  }
  for (int i = 3; i <= n; i++) {
    T[i] = T[i - 1] + T[i - 2] + T[i - 3];
  }
  std::cout << T[n] << "\n";
  return 0;
}
```

>共用时5min





```cpp
#include<iostream>
#include<vector>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;
    vector<int> a(n + 1, 0);
	a[1] = a[2] = 1;
	for (int i = 3; i <= n; i++) {
		a[i] = a[i-1] + a[i-2] + a[i-3];
	}
	cout << a[n] << endl;
}
```





## E02753: 菲波那契数列

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

```cpp
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

```cpp
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

```cpp
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



思路：熟悉了cpp的OOP, 学会了怎么重载加法

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Fraction {
public:
    int numerator;
    int denominator;

    Fraction(int numerator, int denominator) : numerator(numerator), denominator(denominator) {
        int common_divisor = gcd(numerator, denominator);
        this->numerator /= common_divisor;
        this->denominator /= common_divisor;
    }

    Fraction operator+(const Fraction& other) const {
        int common_denominator = denominator * other.denominator;
        int new_numerator = numerator * other.denominator + other.numerator * denominator;
        return Fraction(new_numerator, common_denominator);
    }

    void print() const {
        cout << numerator << "/" << denominator << endl;
    }
};

int main() {
    int a1, b1, a2, b2;
    cin >> a1 >> b1 >> a2 >> b2;
    Fraction f1(a1, b1), f2(a2, b2);
    Fraction result = f1 + f2;
    result.print();
    return 0;
}
```

> 用时10min





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



## E29950: 稳定的符文序列

two pointers, http://cs101.openjudge.cn/practice/E29950

```cpp
#include <iostream>
#include <vector>

auto main() -> int {
  std::cin.tie(nullptr)->sync_with_stdio(false);

  std::string s;
  std::cin >> s;
  int maxLen = 0;
  int left = 0;
  std::vector<int> last(26, -1);
  for (int right = 0; right < s.length(); ++right) {
    int char_idx = s[right] - 'a';
    if (last[char_idx] >= left)
      left = last[char_idx] + 1;

    last[char_idx] = right;
    maxLen = std::max(maxLen, right - left + 1);
  }

  std::cout << maxLen << '\n';
  return 0;
}
```

>共用时20min



思路：双指针, 遇到重复字母, 就不断右移左指针, 直到弹出那个重复字母, 用 `mask` 的二进制第 `i` 记录第 `i` 个字母是否出现

```cpp
#include <bits/stdc++.h>
using namespace std;

int get(char c) {
	return (1 << (c - 'a'));
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    string s;
    cin >> s;
    int l = 0, r = 0;
    int max_len = 0, mask = 0;
    while (r < s.length()) {
    	if ((get(s[r]) & mask)) {
    		while (s[l] != s[r]) {
				mask -= get(s[l]);
				l++;
			}
			mask -= get(s[l]);
			l++;
		}
		mask += get(s[r]);
    	max_len = max(max_len, r - l + 1);
    	r++;
	}
	cout << max_len << '\n';
	return 0;
}
```





## E29952: 咒语序列

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



## E29982: 一种等价类划分问题

hashing, http://cs101.openjudge.cn/practice/29982



```cpp
#include <iostream>

using namespace std;
int cg(int t){
    int ret=0;
    while(t>0){
        ret+=t%10;
        t=t/10;
    }
    return ret;
}

int main(){
    int m,n,k;
    char u,v;
    cin>>m>>u>>n>>v>>k;
    int a[100000]={};
    int b[100000]={};
    for(int i=m+1;i<n;i++){
        a[i]=cg(i);
        if(cg(i)%k==0){
            b[i]=cg(i)/k;
        }
    }
    for(int p=1;p*k<=36;p++){
        int id=0;
        int idd=0;
        for(int i=m+1;i<n;i++){
            if(b[i]==p){
                idd=1;
                if(id==0){
                    cout<<i;
                    id++;
                }else{
                    cout<<","<<i;
                }
            }
        }
        if(idd==0)continue;
        cout<<'\n';
    }
    return 0;
}
```





## E30086: dance

greedy, http://cs101.openjudge.cn/practice/30086

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int main(){
    int n,d;
    cin>>n>>d;
    vector<int> a(2*n,0);
    for(int i=0;i<2*n;i++){
        cin>>a[i];
    }
    sort(a.begin(),a.end());
    for(int i=0;i<2*n;i+=2){
        if(a[i+1]-a[i]>d){cout<<"No"<<'\n';return 0;}
    }
    cout<<"Yes"<<'\n';
    return 0;
}
```



## E30571: 十进制整数的反码

bit manipulation, http://cs101.openjudge.cn/practice/E30571/

```cpp
#include <array>
#include <iostream>

auto main() -> int {
  int n;
  std::array<int, 31> T = {0, 1, 1};
  std::cin >> n;
  if (n >= 1 && n <= 2) {
    std::cout << T[n] << "\n";
    return 0;
  }
  for (int i = 3; i <= n; i++) {
    T[i] = T[i - 1] + T[i - 2] + T[i - 3];
  }
  std::cout << T[n] << "\n";
  return 0;
}
```

>共用时10min



简单的位运算

```cpp
#include<iostream>
#include<vector>
#include<string>
#include<algorithm>
#include<cmath>
using namespace std;

int get(int n) {
	if (n == 0) return 1;
	int ans = 0;
	while (n) {
		n >>= 1;
		ans++;
	}
	return (1 << ans) - 1;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;
    cout << get(n) - n << endl;
	return 0;
}
```





# OJ中等



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

```cpp
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



```cpp
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



```cpp
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



## 07218: 献给阿尔吉侬的花束

Bfs, http://cs101.openjudge.cn/practice/07218/



```cpp
#include<iostream>
#include<queue>
#include<algorithm>
#include<cstring>

using namespace std;

int main() {
    char map[201][201];
    bool vst[201][201] = {0};
    
    int n, x, y, r0, c0;
    cin >> n;
    for(int i = 0; i < n; i ++) {
        cin >> x >> y;
        memset(vst, 0, sizeof(vst));

        for(int r = 0; r < x; r ++) {
            for(int c = 0; c < y; c ++) {
                cin >> map[r][c];
                if(map[r][c] == 'S') {
                    r0 = r;
                    c0 = c;
                }
            }
        }

        queue<pair<int,int>> q;
        q.push({r0, c0});
        vst[r0][c0] = 1;
        int steps = 0;
        bool found = 0;
        while(!q.empty() && !found) {
            int k = q.size();
            for(int j = 0; j < k; j ++) {
                int curr = q.front().first;
                int curc = q.front().second;
                q.pop();
                if(map[curr][curc] == 'E') {
                    cout << steps << endl;
                    found = 1;
                    break;
                } if(curr > 0 && map[curr - 1][curc] != '#' && !vst[curr - 1][curc]) {
                    q.push({curr - 1, curc});
                    vst[curr - 1][curc] = 1;
                } if(curr < x - 1 && map[curr + 1][curc] != '#' && !vst[curr + 1][curc]) {
                    q.push({curr + 1, curc});
                    vst[curr + 1][curc] = 1;
                } if(curc > 0 && map[curr][curc - 1] != '#' && !vst[curr][curc - 1]) {
                    q.push({curr, curc - 1});
                    vst[curr][curc - 1] = 1;
                } if(curc < y - 1 && map[curr][curc + 1] != '#' && !vst[curr][curc + 1]) {
                    q.push({curr, curc + 1});
                    vst[curr][curc + 1] = 1;
                }
            }
            steps ++;
        }
        if(!found) cout << "oop!" << endl;

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



## M01328: Radar Installation

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



```cpp
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







## M02255: 重建二叉树

http://cs101.openjudge.cn/practice/02255/



```cpp
#include <iostream>

using namespace std;

string preorder, midorder;

void dfs(int lp, int rp, int lm, int rm){
	if (lp > rp) return;
	int rootm = lm;
	while (midorder[rootm] != preorder[lp]) rootm++;
	dfs(lp + 1, lp + rootm - lm, lm, rootm - 1);
	dfs(lp + rootm - lm + 1, rp, rootm + 1, rm);
	cout << preorder[lp];
}

int main(){
	while (cin >> preorder >> midorder){
		int n = preorder.size() - 1;
		dfs(0, n, 0, n);
		cout << endl;
	}
	return 0;
}
```


## M02299: Ultra-QuickSort

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



思路：树状数组的模板题 (考试的时候把 `solve` 的返回值写成 `int` 了, 导致一直RE)

```cpp
#include<bits/stdc++.h>
using namespace std;

class BIT {
private:
	long long n;
	vector<long long> tree;
	long long lowbit(long long n) {
		return n & -n;
	}
public:
	BIT(long long n) : n(n), tree(n + 1, 0) {};

	void update(long long idx, long long v=1) {
		for (long long i = idx; i <= n; i += lowbit(i)) {
			tree[i] += v;
		}
	}
	
	long long query(long long idx) {
		long long sum = 0;
		for (long long i = idx; i > 0; i -= lowbit(i)) {
			sum += tree[i];
		}
		return sum;
	}
};

void solve(long long n) {
	vector<long long> a(n);
	for (long long i = 0; i < n; i++) {
		cin >> a[i];
	}
	vector<long long> b = a;
	sort(b.begin(), b.end());
	BIT bit(n);
	
	long long ans = 0;
	for (long long i = 0; i < n; i++) {
		long long rank = lower_bound(b.begin(), b.end(), a[i]) - b.begin() + 1;
		ans += i - bit.query(rank);
		bit.update(rank);
	}
	cout << ans << endl;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

	while (1) {
		long long n;
		cin >> n;
		if (n == 0) break;
		solve(n);
	}
	return 0;
}
```



## 02406:字符串乘方

KMP, http://cs101.openjudge.cn/practice/02406/



【张真铭 25元培】

```cpp
#include <iostream>
#include <vector>

auto main() -> int {
  std::cin.tie(nullptr)->sync_with_stdio(false);

  std::string s;
  while (std::cin >> s) {
    if (s == ".")
      break;

    int n = static_cast<int>(s.length());
    std::vector<int> lps(n, 0);
    int length = 0;
    for (int i = 1; i < n; ++i) {
      while (length > 0 && s[i] != s[length])
        length = lps[length - 1];
      if (s[i] == s[length])
        ++length;
      lps[i] = length;
    }

    int p = n - lps.back();
    if (n % p == 0)
      std::cout << n / p << '\n';
    else
      std::cout << 1 << '\n';
  }
}
```





## M02431: Expedition

heap,greedy, http://cs101.openjudge.cn/practice/02431/

【姚博骞 25物院】思路：构建一个堆，永远只吃堆里面最多的那个
其实有点后悔贪心的想法。

```cpp
#include<iostream>
#include<vector>
#include<queue>
#include<algorithm>
using namespace std;
int main()//greedy heap
{
    int n;
    cin>>n;
    vector<pair<int,int>> stop;
    for(int i=0;i<n;i++)
    {
        int p,q;
        cin>>p>>q;
        stop.push_back({p,q});
    }
    int l,p;
    cin>>l>>p;
    sort(stop.begin(),stop.end(),[](pair<int,int> &a,pair<int,int> &b){
        return a.first>b.first;
    });
    priority_queue<int> pq;//大顶堆；
    int ans=0;
    int i=0;
    int dist=l-p;
    while(i<n&&dist>0)
    {
        while(i<n&&stop[i].first>=dist)
        {
            pq.push(stop[i].second);
            i++;
        }
        if(pq.empty()) break;
        dist-=pq.top();
        pq.pop();
        ans++;
    }
    if(dist<=0)
    {
        cout<<ans;
    }
    else
    {
        cout<<-1;
    }
    return 0;
}

```





## M02692: 假币问题

http://cs101.openjudge.cn/practice/02692

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;
    while (n--)
    {
        string l[3], r[3], stat[3];
        for (int i = 0; i < 3; i++)
            cin >> l[i] >> r[i] >> stat[i];

        for (char c = 'A'; c <= 'L'; ++c)
            for (int fakeType = 0; fakeType < 2; fakeType++)
            {
                bool ok = true;
                for (int i = 0; i < 3; ++i)
                {
                    int left = 0, right = 0;
                    for (char x : l[i])
                        if (x == c)
                            left += (fakeType ? 1 : -1);
                    for (char x : r[i])
                        if (x == c)
                            right += (fakeType ? 1 : -1);
                    if (stat[i] == "even" && left != right)
                        ok = false;
                    if (stat[i] == "up" && left <= right)
                        ok = false;
                    if (stat[i] == "down" && left >= right)
                        ok = false;
                }
                if (ok)
                {
                    cout << c << " is the counterfeit coin and it is " << (fakeType ? "heavy." : "light.") << '\n';
                    goto next_case;
                }
            }
    next_case:;
    }
    return 0;
}
```





## M02749: 分解因数

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

```cpp
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



## M02766: 最大子矩阵

binary, dp,kadane http://cs101.openjudge.cn/pctbook/M02766/

【姚博骞 25物院】思路：三种算法我都写了，其中分治比我想的难写很多，比一维要难，且复杂度只降到O(n^3log n)
dp其实也包含了kadane的思想，无非是直接用kadane还是间接，两个方法的复杂度都是O(n^3)

```cpp
#include<iostream>
#include<vector>
using namespace std;//kadane 算法
int max(int a,int b)
{
    return (a>b)?a:b;
}
int min(int a,int b)
{
    return(a<b)?a:b;
}
int juxing(int p,int q,int r,int s,vector<vector<int>>&qz)
{
    return qz[p][r]+qz[q][s]-qz[p][s]-qz[q][r];
}
int fenzhi(vector<vector<int>>&qz,int i1,int i2,int j1,int j2)
{
    int midi=0.5*(i1+i2);
    int midj=0.5*(j1+j2);
    int ans=-100000000;
    if((j2==j1)||(i2==i1)) return -10000000;
    if(i1!=i2)
    {
        int ans1=fenzhi(qz,i1,midi,j1,j2);
        int ans2=fenzhi(qz,midi+1,i2,j1,j2);
        ans=max(ans,max(ans1,ans2));
    }
    if(j1!=j2)
    {
        int ans1=fenzhi(qz,i1,i2,j1,midj);
        int ans2=fenzhi(qz,i1,i2,midj+1,j2);
        ans=max(ans,max(ans1,ans2));
    }
    int ans3,ans4;
    ans3=ans4=-100000000;
    for(int i=i1;i<=i2;i++)
    {
        for(int i_=i+1;i_<=i2;i_++)
        {
            int p,q;
            p=100000000;
            q=-100000000;
            for(int j=j1;j<=midj;j++)
            {
                p=min(p,juxing(i,i_,j1,j,qz));
            }
            for(int j=midj+1;j<=j2;j++)
            {
                q=max(q,juxing(i,i_,j1,j,qz));
            }
            ans3=max(q-p,ans3);
        }
    }
    for(int j=j1;j<=j2;j++)
    {
        for(int j_=j+1;j_<=j2;j_++)
        {
            int p,q;
            p=100000000;
            q=-100000000;
            for(int i=i1;i<=midi;i++)
            {
                p=min(p,juxing(i1,i,j,j_,qz));
            }
            for(int i=midi+1;i<=i2;i++)
            {
                q=max(q,juxing(i1,i,j,j_,qz));
            }
            ans4=max(q-p,ans4);
        }
    }
    ans=max(ans,max(ans3,ans4));
    return ans; 
}
int maxSubmatrix(vector<vector<int>>& a)
{
    int n = a.size();
    int m = a[0].size();
    int ans = -1e9;

    // 枚举上边界
    for(int top = 0; top < n; top++)
    {
        vector<int> sum(m, 0);  // 压缩后的数组

        // 枚举下边界
        for(int bottom = top; bottom < n; bottom++)
        {
            // 把这一行加进去（压缩列）
            for(int j = 0; j < m; j++)
                sum[j] += a[bottom][j];

            // ⭐ 在 sum 上跑一维 Kadane
            int cur = sum[0], best = sum[0];
            for(int j = 1; j < m; j++)
            {
                cur = max(sum[j], cur + sum[j]);
                best = max(best, cur);
            }

            ans = max(ans, best);
        }
    }
    return ans;
}
int kadane(vector<vector<int>>&a)
{
    int n=a.size();
    vector<vector<int>>lieqianzhui(n+1,vector<int>(n,0));
    vector<vector<int>>hangqianzhui(n,vector<int>(n+1,0));
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            hangqianzhui[i][j+1]=hangqianzhui[i][j]+a[i][j];
        }   
    }
    for(int j=0;j<n;j++)
    {
        for(int i=0;i<n;i++)
        {
            lieqianzhui[i+1][j]=lieqianzhui[i][j]+a[i][j];
        }   
    }
    vector<vector<int>>dp(n,vector<int>(n,-10000000));
    vector<vector<vector<int>>>dpx(n,vector<vector<int>>(n));
    vector<vector<vector<int>>>dpy(n,vector<vector<int>>(n));
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            int ans1,ans2;
            ans1=ans2=-100000000;
            for(int i1=0;i1<i;i1++)
            {
                dpx[i][j].push_back(((j>0)?max(0, dpx[i][j-1][i1]):0)+lieqianzhui[i+1][j]-lieqianzhui[i1+1][j]);
                ans1=max(ans1,dpx[i][j][i1]);
            }
            for(int j1=0;j1<j;j1++)
            {
                dpy[i][j].push_back(((i>0)?max(0,dpy[i-1][j][j1]):0)+hangqianzhui[i][j+1]-hangqianzhui[i][j1+1]);
                ans2=max(ans2,dpy[i][j][j1]);
            }
            dp[i][j]=max(max(ans1,ans2),a[i][j]);//kadane算法
        }
    }
    int ans=-1000000000;
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            ans=max(ans,dp[i][j]);
        }
    }
    return ans;
}
int main()
{
    int n;
    cin>>n;
    vector<vector<int>>a(n,vector<int>(n));
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            cin>>a[i][j];
        }
    }
    vector<vector<int>>qianzhui(n+1,vector<int>(n+1,0));
    vector<vector<int>>hangqianzhui(n,vector<int>(n+1,0));
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            hangqianzhui[i][j+1]=hangqianzhui[i][j]+a[i][j];
            qianzhui[i+1][j+1]=hangqianzhui[i][j+1]+qianzhui[i][j+1];
        }   
    }
    cout<<maxSubmatrix(a);
    return 0;
}

```





## M02774: 木材加工

binary search, http://cs101.openjudge.cn/practice/02774/



```cpp
#include <stdio.h>

int len[10001];

bool check(int n, int m, int k){
	int cnt = 0;
	for (int i = 1; i <= n; i++){
		cnt += len[i] / m;
	}
	return cnt >= k;
}

int main(){
	int n, k, l = 1, r = 10000, ans = 0;
	scanf("%d %d", &n, &k);
	for (int i = 1; i <= n; i++){
		scanf("%d", &len[i]);
	}
	while (l <= r){
		int mid = (l + r) >> 1;
		if (check(n, mid, k)){
			l = mid + 1;
			ans = mid;
		} else {
			r = mid - 1;
		}
	}
	printf("%d", ans);
	return 0;
}
```



【黄宇曦 地球与空间科学学院】思路：直接二分解决，空间复杂度本来就是 $O(1)$。

```cpp
#include <bits/stdc++.h>

using namespace std;

#define all(x) begin(x), end(x)
#define sz(x) (int) (x).size()

using i64 = long long;
using u64 = unsigned long long;
using i128 = __int128_t;
using u128 = __uint128_t;
using pii = pair<int, int>;
using vi = vector<int>;
using usi = unordered_set<int>;

int main() {
    cin.tie(nullptr)->sync_with_stdio(false);
    int n, k;
    cin >> n >> k;
    vi a(n);
    for (int i = 0; i < n; i++)
        cin >> a[i];
    if (k > accumulate(all(a), 0ll)) {
        cout << 0 << '\n';
        return 0;
    }
    int l = 1, r = *max_element(all(a));
    auto check = [&](int x) {
        i64 ans = 0;
        for (int t : a)
            ans += t / x;
        return ans >= k;
    };
    int ans = 0;
    while (l <= r) {
        int mid = l + r >> 1;
        if (check(mid))
            l = mid + 1, ans = mid;
        else
            r = mid - 1;
    }
    cout << ans << '\n';
    return 0;
}
```








## M02783: Holiday Hotel

greedy, http://cs101.openjudge.cn/practice/02783/


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

```cpp
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



## M02788: 二叉树（2）

http://cs101.openjudge.cn/practice/02788/

思路：

- $m$ 子树也是**完全二叉树**，故我们只需要关心与 $n$ 在同一层的点有哪些能取到。
- 考虑 dfs 搜索：对于 $(m, n)$，若 $m$ 子树内不存在与 $n$ 在同一层且编号 $\leq n$ 的点则答案为 $0$，若 $m$ 子树内所有与 $n$ 在同一层的点的编号都 $\leq n$ 则答案为 $2^{\lfloor \log_2 n \rfloor - \lfloor \log_2 m \rfloor}$。
- 否则，我们考虑直接对 $m$ 的两个儿子递归求解再将答案相加。
- 注意到两个儿子之中至少有一个不会再往下递归，则递归层数是 $O(\log \dfrac{n}{m})$ 的。
- 故时间复杂度为 $O(\sum \log \dfrac{n}{m})$，可以通过。

代码：

```cpp
#include <stdio.h>
#include <math.h>

int solve(int m, int n, int delta){
	int l = m << delta;
	if (l > n) return 0;
	int r = l + (1 << delta) - 1;
	if (r <= n) return 1 << delta;
	return solve(m << 1, n, delta - 1) + solve(m << 1 | 1, n, delta - 1);
}

int main(){
	int m, n;
	while (true){
		scanf("%d %d", &m, &n);
		if (m == 0 && n == 0) break;
		int delta = (int)log2(n) - (int)log2(m);
		printf("%d\n", solve(m, n, delta) + ((1 << delta) - 1));
	}
	return 0;
}
```



## M03129: 魔兽世界之一：备战

OOP implementation , http://cs101.openjudge.cn/practice/03129/

魔兽世界的西面是红魔军的司令部，东面是蓝魔军的司令部。两个司令部之间是依次排列的若干城市。 
红司令部，City 1，City 2，……，City n，蓝司令部

两军的司令部都会制造武士。武士一共有 dragon 、ninja、iceman、lion、wolf 五种。每种武士都有编号、生命值、攻击力这三种属性。 

双方的武士编号都是从1开始计算。红方制造出来的第n个武士，编号就是n。同样，蓝方制造出来的第n个武士，编号也是n。 

武士在刚降生的时候有一个生命值。 

在每个整点，双方的司令部中各有一个武士降生。 

红方司令部按照iceman、lion、wolf、ninja、dragon的顺序循环制造武士。 

蓝方司令部按照lion、dragon、ninja、iceman、wolf的顺序循环制造武士。 

制造武士需要生命元。 

制造一个初始生命值为m的武士，司令部中的生命元就要减少m个。 

如果司令部中的生命元不足以制造某个按顺序应该制造的武士，那么司令部就试图制造下一个。如果所有武士都不能制造了，则司令部停止制造武士。

给定一个时间，和双方司令部的初始生命元数目，要求你将从0点0分开始到双方司令部停止制造武士为止的所有事件按顺序输出。
一共有两种事件，其对应的输出样例如下： 

1) 武士降生 

输出样例： 004 blue lion 5 born with strength 5,2 lion in red headquarter
表示在4点整，编号为5的蓝魔lion武士降生，它降生时生命值为5，降生后蓝魔司令部里共有2个lion武士。（为简单起见，不考虑单词的复数形式）注意，每制造出一个新的武士，都要输出此时司令部里共有多少个该种武士。

2) 司令部停止制造武士

输出样例： 010 red headquarter stops making warriors
表示在10点整，红方司令部停止制造武士

输出事件时： 

首先按时间顺序输出； 

同一时间发生的事件，先输出红司令部的，再输出蓝司令部的。

**输入**

第一行是一个整数，代表测试数据组数。

每组测试数据共两行。 

第一行：一个整数M。其含义为， 每个司令部一开始都有M个生命元( 1 <= M <= 10000)。

第二行：五个整数，依次是 dragon 、ninja、iceman、lion、wolf 的初始生命值。它们都大于0小于等于10000。

**输出**

对每组测试数据，要求输出从0时0分开始，到双方司令部都停止制造武士为止的所有事件。
对每组测试数据，首先输出"Case:n" n是测试数据的编号，从1开始 。
接下来按恰当的顺序和格式输出所有事件。每个事件都以事件发生的时间开头，时间以小时为单位，有三位。

样例输入

```
1
20
3 4 5 6 7
```

样例输出

```
Case:1
000 red iceman 1 born with strength 5,1 iceman in red headquarter
000 blue lion 1 born with strength 6,1 lion in blue headquarter
001 red lion 2 born with strength 6,1 lion in red headquarter
001 blue dragon 2 born with strength 3,1 dragon in blue headquarter
002 red wolf 3 born with strength 7,1 wolf in red headquarter
002 blue ninja 3 born with strength 4,1 ninja in blue headquarter
003 red headquarter stops making warriors
003 blue iceman 4 born with strength 5,1 iceman in blue headquarter
004 blue headquarter stops making warriors
```





【张真铭 25元培】

```cpp
#include <array>
#include <cstdint>
#include <iomanip>
#include <iostream>
#include <string_view>

enum class WarriorType : std::uint8_t {
  DRAGON = 0,
  NINJA,
  ICEMAN,
  LION,
  WOLF,
  COUNT
};

constexpr int WARRIOR_COUNT = static_cast<int>(WarriorType::COUNT);

constexpr std::array<std::string_view, WARRIOR_COUNT> WARRIOR_NAMES = {
    "dragon", "ninja", "iceman", "lion", "wolf"};

constexpr std::array<WarriorType, 5> RED_ORDER = {
    WarriorType::ICEMAN, WarriorType::LION, WarriorType::WOLF,
    WarriorType::NINJA, WarriorType::DRAGON};

constexpr std::array<WarriorType, 5> BLUE_ORDER = {
    WarriorType::LION, WarriorType::DRAGON, WarriorType::NINJA,
    WarriorType::ICEMAN, WarriorType::WOLF};

class Headquarter {
public:
  Headquarter(std::string_view name, int initial_m,
              const std::array<int, WARRIOR_COUNT> &hp_costs,
              const std::array<WarriorType, 5> &build_order)
      : m_name(name), m_total_m(initial_m), m_costs(hp_costs),
        m_order(build_order) {}

  void step(int time) {
    if (m_stopped)
      return;

    for (int i = 0; i < 5; ++i) {
      WarriorType type = m_order[m_iter];
      int cost = m_costs[static_cast<int>(type)];

      if (m_total_m >= cost) {
        m_total_m -= cost;
        m_counts[static_cast<int>(type)]++;
        m_total_count++;

        log_production(time, type, cost);

        m_iter = (m_iter + 1) % 5;
        return;
      }

      m_iter = (m_iter + 1) % 5;
    }

    m_stopped = true;
    log_stop(time);
  }

  [[nodiscard]] auto is_stopped() const noexcept -> bool { return m_stopped; }

private:
  std::string_view m_name;
  int m_total_m;
  const std::array<int, WARRIOR_COUNT> &m_costs;
  const std::array<WarriorType, 5> &m_order;

  std::array<int, WARRIOR_COUNT> m_counts{0};
  int m_total_count{0};
  int m_iter{0};
  bool m_stopped{false};

  void print_time(int time) const {
    std::cout << std::setfill('0') << std::setw(3) << time << ' ';
  }

  void log_production(int time, WarriorType type, int cost) const {
    print_time(time);
    auto type_idx = static_cast<int>(type);
    std::cout << m_name << ' ' << WARRIOR_NAMES[type_idx] << ' '
              << m_total_count << " born with strength " << cost << ','
              << m_counts[type_idx] << ' ' << WARRIOR_NAMES[type_idx] << " in "
              << m_name << " headquarter\n";
  }

  void log_stop(int time) const {
    print_time(time);
    std::cout << m_name << " headquarter stops making warriors\n";
  }
};

auto main() -> int {
  std::cin.tie(nullptr)->sync_with_stdio(false);

  int t;
  if (!(std::cin >> t))
    return 0;

  for (int caseIdx = 1; caseIdx <= t; ++caseIdx) {
    int M;
    std::cin >> M;
    std::array<int, WARRIOR_COUNT> warrior_HP;
    for (int &hp : warrior_HP) {
      std::cin >> hp;
    }

    std::cout << "Case:" << caseIdx << '\n';

    Headquarter red("red", M, warrior_HP, RED_ORDER);
    Headquarter blue("blue", M, warrior_HP, BLUE_ORDER);

    int time = 0;
    while (!red.is_stopped() || !blue.is_stopped()) {
      red.step(time);
      blue.step(time);
      time++;
    }
  }
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

```cpp
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



## M04077: 出栈序列统计

dp, dfs, math, http://cs101.openjudge.cn/practice/04077/

【黄宇曦 地球与空间科学学院】思路：直接思考 dp。考虑第一个在什么时候被弹出不难发现转移方程。事实上这也是所谓的 Catalan 数。

```cpp
#include <bits/stdc++.h>

using namespace std;

#define all(x) begin(x), end(x)
#define sz(x) (int) (x).size()

using i64 = long long;
using u64 = unsigned long long;
using i128 = __int128_t;
using u128 = __uint128_t;
using pii = pair<int, int>;
using vi = vector<int>;
using usi = unordered_set<int>;

int main() {
    cin.tie(nullptr)->sync_with_stdio(false);
    int n;
    cin >> n;
    vi dp(n + 1, 0);
    dp[0] = dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        for (int j = 0; j < i; j++) {
            dp[i] += dp[j] * dp[i - 1 - j];
        }
    }
    cout << dp[n] << '\n';
    return 0;
}
```



【张真铭 元培】思路：Catalan数 $𝐶_𝑛$ 的递推关系有着天然的递归结构：规模为 $𝑛$ 的计数问题 $𝐶_𝑛$ ，可以通过枚举分界点，分拆为两个规模分别为 $𝑖$ 和 $(𝑛−1-𝑖)$ 的子问题。这一递推关系使得Catalan数广泛出现于各类具有类似递归结构的问题中。

**路径计数问题**：有一个大小为 $n\times n$ 的方格图，左下角为 $(0,0)(0, 0)$，右上角为 $(𝑛,𝑛)(n, n)$ 。从左下角开始，每次都只能向右或者向上走一单位，不走到对角线 $y=x$ 上方（但可以触碰）的情况下，到达右上角的路径总数为 $C_n$ 。

**圆内不相交弦计数问题**：圆上有 $2n$ 个点，将这些点成对连接起来且使得所得到的 $n$ 条线段两两不交的方案数是 $C_n$。

**三角剖分计数问题**：对角线不相交的情况下，将一个凸 $(n + 2)$ 边形区域分成三角形区域的方法数为 $C_n$ 。

**二叉树计数问题**：含有 $n$ 个结点的形态不同的二叉树数目为 $C_n$ 。等价地，含有 $n$ 个非叶结点的形态不同的满二叉树数目为 $C_{n}$ 。

**括号序列计数问题**：由 $n$ 对括号构成的合法括号序列数为 $C_n$ 。

**出栈序列计数问题**：一个栈（无穷大）的进栈序列为 $1,2,3, \ldots ,n$ ，合法出栈序列的数目为 $C_n$ 。

**数列计数问题**：由 $n$ 个 $+1$ 和 $n$ 个 $-1$ 组成的数列 $a_1,a_2, \ldots ,a_{2n}$ 中，部分和满足 $a_1+a_2+ \ldots +a_k \geq 0~(k=1,2,3, \ldots ,2n)$ 的数列数目为 $C_n$ 。


$C_n = \frac{(4n - 2)}{n + 1} C_{n-1},\ n > 0,\ C_0 = 1.$


代码：

```cpp
#include <iostream>

auto main() -> int {
  std::cin.tie(nullptr)->sync_with_stdio(false);

  int n;
  std::cin >> n;
  int c_prev = 1;
  int c_curr = 1;
  for (int i = 1; i <= n; ++i) {
    c_prev = c_curr;
    c_curr = (4 * i - 2) * c_prev / (i + 1);
  }
  std::cout << c_curr << '\n';
}
```





## M04078: 实现堆结构

http://cs101.openjudge.cn/practice/04078/

要求手搓堆实现。

思路：根据课上所讲直接写即可，用时约20min

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

struct TreeNode
{
    int value;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int v) : value(v), left(nullptr), right(nullptr) {}
    TreeNode(int v, TreeNode* l, TreeNode* r) : value(v), left(l), right(r) {}
};
class quque//手搓最小堆
{
    public:
        vector<int> q;
        void push(int value)
        {
            q.push_back(value);
            int i = q.size()-1;
            while (i > 0)
            {
                int parent = (i-1)/2;
                if (q[parent] > q[i])
                {
                    int tmp = q[parent];
                    q[parent] = q[i];
                    q[i] = tmp;
                    i = parent;
                }
                else
                    break;
            }
        }
        void pop()
        {
            q[0] = q[q.size()-1];
            q.pop_back();
            int i = 0;
            while (2 * i + 1 < q.size())
            {
                int left = 2 * i + 1;
                int right = 2 * i + 2;
                int min = left;
                if (right < q.size() && q[right] < q[left])
                    min = right;
                if (q[min] < q[i])
                {
                    int tmp = q[min];
                    q[min] = q[i];
                    q[i] = tmp;
                    i = min;
                }
                else
                    break;
            }
        }
        int top()
        {
            return q[0];
        }
};
int main() 
{
    int n;
    cin >> n;
    quque q;
    while (n--)
    {
        int type;
        cin >> type;
        if (type == 1)
        {
            int value;
            cin >> value;
            q.push(value);

        }
        else
        {
            cout << q.top() << endl;
            q.pop();
        }
    }
    return 0;
}
```





## 04080: Huffman编码树

greedy, http://cs101.openjudge.cn/practice/04080/

思路：根据huffman编码的定义，每次将权重最小的两个合并成一个，一直合并直到最后只剩一个，该节点即为根节点

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

struct TreeNode
{
    int weight;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int w) : weight(w), left(nullptr), right(nullptr) {}
    TreeNode(int w, TreeNode* l, TreeNode* r) : weight(w), left(l), right(r) {}
};
class Solution
{
    public:
        vector<pair<int,TreeNode*>> heights;
        void getheights()
        {
            int length;
            cin >> length;
            heights.resize(length);
            for (int i = 0; i < length; i++)
            {
                cin >> heights[i].first;
                heights[i].second = new TreeNode(heights[i].first);
                //一定是叶节点，因此可以直接建立
            }
        }
        void buildTree(vector<pair<int, TreeNode*>>& heights)//这个&我debug了半天才发现没写
        {
            while (heights.size() > 1)
            {
                sort(heights.begin(), heights.end());
                TreeNode* left = heights[0].second;
                TreeNode* right = heights[1].second;
                int sum = heights[0].first + heights[1].first;
                heights.erase(heights.begin(), heights.begin() + 2);
                heights.push_back({sum, new TreeNode(sum, left, right)});
                //合二为一，一为二的父节点
            }
        }
        int length(TreeNode* root, int height)
        {
            if (!root) return 0;//理论上这行不会执行
            if (root->left == nullptr && root->right == nullptr)//叶节点
                return (height * root->weight);
            return length(root->left, height + 1) + length(root->right, height + 1) ;
        }
        void solve()
        {
            getheights();
            buildTree(heights);
            cout << length(heights[0].second, 0);
        }
};
int main() 
{
    Solution s;
    s.solve();
    return 0;
}
```






## M04081: 树的转换 

http://cs101.openjudge.cn/practice/04081/

代码：

```cpp
#include <iostream>
#include <stack>
#include <vector>

using namespace std;

int depth[10001];
stack<int> stk;
vector<int> v[10001];

int main(){
	int id = 0, h1 = 0;
	string s;
	cin >> s;
	stk.push(0);
	for (char i : s){
		if (i == 'd'){
			id++;
			v[stk.top()].push_back(id);
			stk.push(id);
		} else {
			stk.pop();
		}
		h1 = max(h1, (int)stk.size() - 1);
	}
	for (int i = id; i >= 0; i--){
		int size = v[i].size();
		for (int j = 0; j < size; j++){
			depth[i] = max(depth[i], depth[v[i][j]] + j + 1);
		}
	}
	cout << h1 << " => " << depth[0];
	return 0;
}
```



## M04100: 进程检测

http://cs101.openjudge.cn/practice/04100

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

struct Node
{
    int s, d;
};

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int k;
    cin >> k;
    while (k--)
    {
        int n;
        cin >> n;
        vector<Node> p(n);
        for (int i = 0; i < n; i++)
            cin >> p[i].s >> p[i].d;

        int testCounter = 0;
        sort(p.begin(), p.end(), [](Node &a, Node &b) -> bool
             { return a.s < b.s; });
        int it = 0;
        while (it < n)
        {
            int j = it;
            int maxs = p[it].s, mind = p[it].d;
            while (j < n && p[j].s >= maxs && p[j].s <= mind)
            {
                maxs = max(maxs, p[j].s);
                mind = min(mind, p[j].d);
                j++;
            }
            it = j;
            testCounter++;
        }

        cout << testCounter << '\n';
    }
    return 0;
}
```





## M04117: 简单的整数划分问题

dfs, dp, http://cs101.openjudge.cn/practice/04117/

思路：

- 设 $dp_{i, j}$ 表示把 $i$ 划分称若干正整数之和、且其中最大者为 $j$ 的方案数。
- 初值：$dp_{0, 0} = 1$。
- 转移：枚举次大者，可知 $dp_{i, j} = \displaystyle\sum_{k = 0}^j dp_{i - j, k}$。
- 答案：$\displaystyle\sum_{i = 1}^n dp_{n, i}$。
- 时间复杂度为 $O(N^3 + \sum n)$，其中 $N = 50$。
- **注意本题要多测！**

代码：

```cpp
#include <stdio.h>

const int N = 50;
int dp[N + 1][N + 1];

int main(){
	int n;
	dp[0][0] = 1;
	for (int i = 1; i <= N; i++){
		for (int j = 1; j <= i; j++){
			for (int k = 0; k <= j; k++){
				dp[i][j] += dp[i - j][k];
			}
		}
	}
	while (scanf("%d", &n) != EOF){
		int ans = 0;
		for (int i = 1; i <= n; i++){
			ans += dp[n][i];
		}
		printf("%d\n", ans);
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

```cpp
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

```cpp
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



## M04137: 最小新整数

monotonous-stack, http://cs101.openjudge.cn/practice/04137/

思路：

- 法一（考场 ver.）：注意到 $n$ 最多只有 $9$ 位，因此可以直接枚举出所有可能的删除方案，再取最小值即可。时间复杂度视实现可能为 $O(t 2^m m)$ 或 $O(t C_m^k (m - k))$，其中 $m = \lfloor \log_{10} n \rfloor + 1$。
- 法二：考虑 dp，设 $dp_{i, j}$ 表示在前 $i$ 位中删去 $j$ 位所能得到的最小数，答案即为 $dp_{m, k}$。时间复杂度为 $O(tmk)$。
- 法三：考虑贪心，令 $k' = m - k$，则我们需要给新数依次确定尽可能小的第 $i$ 位，其中 $i = 1, \cdots, k$。
- 设新数的第 $t$ 位为原数的第 $p_t$ 位，原数从高到低的第 $t$ 位为 $d_t$，则对于 $p_i$，我们有如下限制：
- (1) $p_{i - 1} < p_i \leq n - (k' - i) = i + k$，左边确保了新数的前 $i$ 位可以通过删除原数得到，右边确保了第 $i + 1 \sim k'$ 位还有的选。
- (2) $d_{p_i}$ 尽可能小。**那要是有多个，我们应该怎么办呢？**
- (3) 在满足 (2) 的前提下，$p_i$ 尽可能小，这样的话可以给后面留下更大的选择余地。
- 类似滑动窗口地单调队列即可。时间复杂度为 $O(tm)$。
- ~~那么问题来了，为什么 $n$ 不开到 $10^{10^5}$ 卡掉上面两种做法？~~

代码（法三）：

```cpp
#include <iostream>
#include <algorithm>
#include <queue>

using namespace std;

int digit[10];
deque<int> q;

int main(){
	int t;
	cin >> t;
	for (int i = 1; i <= t; i++){
		int n, k, k_, len = 0;
		cin >> n >> k;
		while (n > 0){
			digit[++len] = n % 10;
			n /= 10;
		}
		reverse(digit + 1, digit + len + 1);
		k_ = len - k;
		q.clear();
		for (int j = 1; j <= k; j++){
			while (!q.empty() && digit[q.back()] > digit[j]) q.pop_back();
			q.push_back(j);
		}
		for (int j = 1; j <= k_; j++){
			int add = j + k, cur;
			while (!q.empty() && digit[q.back()] > digit[add]) q.pop_back();
			q.push_back(add);
			cur = q.front();
			q.pop_front();
			cout << digit[cur];
		}
		cout << endl; 
	}
	return 0;
}
```



## M04147: 汉诺塔问题(Tower of Hanoi)

```cpp
dfs, [http://cs101.openjudge.cn/pctbook/M04147](http://cs101.openjudge.cn/pctbook/M04147)

#include <iostream>  
#include <vector>  
using namespace std;  
  
void moveDisk(int numDisk, char fromPole, char toPole)  
{  
    printf("%d:%c->%c\n", numDisk, fromPole, toPole);  
}  
  
void moveTower(int height, char fromPole, char withPole, char toPole)  
{  
    if (height == 1)  
        moveDisk(1, fromPole, toPole);  
    else  
    {  
        moveTower(height - 1, fromPole, toPole, withPole);  
        moveDisk(height, fromPole, toPole);  
        moveTower(height - 1, withPole, fromPole, toPole);  
    }  
}  
  
int main()  
{  
    ios::sync_with_stdio(false);  
    cin.tie(nullptr);  
  
    int n;  
    char a, b, c;  
    cin >> n >> a >> b >> c;  
    moveTower(n, a, b, c);  
    return 0;  
}
```




## M05585: 晶矿的个数

matrices, dfs similar, [http://cs101.openjudge.cn/pctbook/M05585](http://cs101.openjudge.cn/pctbook/M05585)

 

```cpp
#include <iostream>  
#include <cstring>  
#include <vector>  
using namespace std;  
  
int xy[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};  
char m[30][30];  
  
void dfs(int x, int y, char c)  
{  
    m[x][y] = '#';  
    for (int i = 0; i < 4; i++)  
    {  
        int newX = x + xy[i][0];  
        int newY = y + xy[i][1];  
        if (m[newX][newY] == c)  
            dfs(newX, newY, c);  
    }  
}  
  
int main()  
{  
    ios::sync_with_stdio(false);  
    cin.tie(nullptr);  
  
    int k;  
    cin >> k;  
    for (int i = 0; i < k; i++)  
    {  
        int n;  
        cin >> n;  
        memset(m, '\0', sizeof(m));  
        for (int j = 0; j < n * n; j++)  
            cin >> m[j / n][j % n];  
          
        int r = 0, b = 0;  
        for (int x = 0; x < n; x++)  
            for (int y = 0; y < n; y++)  
                if (m[x][y] == 'r')  
                {  
                    dfs(x, y, 'r');  
                    r++;  
                }  
                else if (m[x][y] == 'b')  
                {  
                    dfs(x, y, 'b');  
                    b++;  
                }  
          
        cout << r << ' ' << b << '\n';  
    }  
    return 0;  
}
```



## M06640: 倒排索引

data structures, http://cs101.openjudge.cn/pctbook/M06640/

思路：用 `map<string, set<int>>` 建立倒排索引：key 为单词，value 为出现该单词的文档编号集合。

```cpp
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



## M07161: 森林的带度数层次序列存储

tree, http://cs101.openjudge.cn/practice/07161/


思路：根据**带度数的层次序列**恢复树，再进行后根遍历输出

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

struct Node {
    char val;
    vector<Node*> children;
    Node(char c) : val(c) {}
};


void postorder(Node* root) {
    if (!root) return;
    for (int i = 0; i < (int)root->children.size(); ++i)
        postorder(root->children[i]);
    cout << root->val << " ";
}


Node* buildTree() {
    vector<char> vals;
    vector<int> degs;
    char c;
    int d;


    while (cin >> c >> d) {
        vals.push_back(c);
        degs.push_back(d);
        if (cin.peek() == '\n') break; 
    }

    if (vals.empty()) return nullptr;

    queue<Node*> q;
    Node* root = new Node(vals[0]);
    q.push(root);

    int idx = 1;
    for (int i = 0; !q.empty() && idx < (int)vals.size(); ++i) {
        Node* parent = q.front();
        q.pop();

        int cnt = degs[i]; 
        for (int j = 0; j < cnt && idx < (int)vals.size(); ++j) {
            Node* child = new Node(vals[idx]);
            parent->children.push_back(child);
            q.push(child);
            idx++;
        }
    }
    return root;
}

int main() {
    int n;
    cin >> n;

    vector<Node*> forest;
    forest.reserve(n);


    for (int i = 0; i < n; ++i) {
        Node* t = buildTree();
        forest.push_back(t);
    }


    for (int i = 0; i < n; ++i)
        postorder(forest[i]);

    cout << endl;
    return 0;
}
```



思路：读取每个测试用例的节点信息，利用队列构建树结构，然后进行后序遍历输出所有节点值。

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <sstream>
#include <string>

using namespace std;
struct Node {
    char val;
    vector<Node*> children;
    Node(char c) : val(c) {}
};
vector<string> split(const string &s) {
    vector<string> res;
    stringstream ss(s);
    string token;
    while (ss >> token) {
        res.push_back(token);
    }
    return res;
}
Node* buildTree(const vector<pair<char, int>> &nodes) {
    if (nodes.empty()) return nullptr;
    Node* root = new Node(nodes[0].first);
    queue<pair<Node*, int>> q; 
    q.push({root, nodes[0].second});
    
    int i = 1;
    while (i < nodes.size() && !q.empty()) {
        auto [parent, need] = q.front();
        q.pop();
        for (int j = 0; j < need && i < nodes.size(); ++j) {
            char val = nodes[i].first;
            int degree = nodes[i].second;
            Node* child = new Node(val);
            parent->children.push_back(child);
            if (degree > 0) {
                q.push({child, degree}); 
            }
            ++i;
        }
    }
    return root;
}
void postOrder(Node* node, string &s) {
    if (!node) return;
    for (Node* child : node->children) {
        postOrder(child, s);
    }
    s += node->val;
    s += " ";
}

int main() {
    int n;
    cin >> n;
    cin.ignore(); 
    string result;
    for (int i = 0; i < n; ++i) {
        string line;
        getline(cin, line);
        vector<string> tokens = split(line);
        vector<pair<char, int>> nodes;
        for (int j = 0; j + 1 < tokens.size(); j += 2) {
            char c = tokens[j][0];
            int d = stoi(tokens[j + 1]);
            nodes.emplace_back(c, d);
        }
        Node* root = buildTree(nodes);
        postOrder(root, result);
    }
    if (!result.empty()) {
        result.pop_back();
    }
    cout << result << endl;
    
    return 0;
}
```



思路：用队列读取数据建树再后序遍历即可

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

struct TreeNode {
    char val;
    vector<TreeNode*> children;
    TreeNode(char c) : val(c) {}
};

void postOrder(TreeNode* root, string& res) {
    if (!root) return;
    for (TreeNode* child : root->children) {
        postOrder(child, res);
    }
    res += root->val;
    res += ' ';
}

void solve() {
    char c;
    int n;
    cin >> c >> n;
    queue<pair<TreeNode*, int>> q;
    TreeNode* root = new TreeNode(c);
    q.push({root, n});

    while (!q.empty()) {
        auto [node, n] = q.front();
        q.pop();

        for (int i = 0; i < n; i++) {
            char ch;
            int num;
            cin >> ch >> num;
            TreeNode* child = new TreeNode(ch);
            node->children.push_back(child);
            q.push({child, num});
        }
    }

    string res = "";
    postOrder(root, res);
    cout << res;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t;
    cin >> t;
    while (t--) {
        solve();
    }
    cout << endl;
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

```cpp
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



## M12560: 生存游戏

matrices, http://cs101.openjudge.cn/pctbook/M12560/

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=105;
int n,m,cnt;
bool a[N][N];
int main(){
    scanf("%d %d",&n,&m);
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++)
            scanf("%d",&a[i][j]);
    }
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cnt=a[i-1][j-1]+a[i-1][j]+a[i-1][j+1]+a[i][j-1]+a[i][j+1]+a[i+1][j-1]+a[i+1][j]+a[i+1][j+1];
            if(a[i][j]){
                if(cnt<2 || cnt>3)
                    printf("0 ");
                else
                    printf("1 ");
            }
            else{
                if(cnt==3)
                    printf("1 ");
                else
                    printf("0 ");
            }
        }
        printf("\n");
    }
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



```cpp
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

```cpp
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



## M19943 图的拉普拉斯矩阵



```cpp
#include <iostream>
#include <vector>

using namespace std;

class Vertex {
private:
	vector<int> adj;
	
public:
	void add_edge_to(int v){
		adj.push_back(v);
	}
	
	int get_degree(){
		return adj.size();
	}
	
	vector<int> get_adjacent(){
		return adj;
	}
};

class Graph {
private:
	int n;
	vector<Vertex> node;
	
public:
	void init(int _n){
		n = _n;
		node.resize(n);
	}
	
	void add_edge(int u, int v){
		node[u].add_edge_to(v);
		node[v].add_edge_to(u);
	}
	
	vector<vector<int>> get_laplace(){
		vector<vector<int>> ans(n, vector<int>(n));
		for (int i = 0; i < n; i++){
			ans[i][i] += node[i].get_degree();
			for (int j : node[i].get_adjacent()){
				ans[i][j]--;
			}
		}
		return ans;
	}
};

void output(vector<vector<int>> mat){
	for (vector<int> i : mat){
		for (int j : i){
			cout << j << " ";
		}
		cout << endl;
	}
}

int main(){
	int n, m;
	Graph g;
	cin >> n >> m;
	g.init(n);
	for (int i = 1; i <= m; i++){
		int a, b;
		cin >> a >> b;
		g.add_edge(a, b);
	}
	output(g.get_laplace());
	return 0;
}
```



## 20018: 蚂蚁王国的越野跑

http://cs101.openjudge.cn/practice/20018/

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Fenwick
{
private:
    int n;
    vector<int> tree;

public:
    Fenwick(int n) : n(n), tree(n + 1, 0) {}

    void update(int i)
    {
        while (i <= n)
        {
            ++tree[i];
            i += (i & -i);
        }
    }

    long long query(int i)
    {
        long long s = 0;
        while (i > 0)
        {
            s += tree[i];
            i &= i - 1;
        }
        return s;
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    int N;
    cin >> N;
    vector<int> v(N), vals(N);
    for (int i = 0; i < N; ++i)
    {
        int ipt;
        cin >> ipt;
        v[i] = ipt, vals[i] = ipt;
    }

    sort(v.begin(), v.end());
    v.erase(unique(v.begin(), v.end()), v.end());

    Fenwick BIT(N);

    long long ans = 0;
    for (const auto &x : vals)
    {
        int r = lower_bound(v.begin(), v.end(), x) - v.begin() + 1;
        ans += BIT.query(r - 1);
        BIT.update(r);
    }

    cout << ans << '\n';
    return 0;
}
```



### M20744: 土豪购物

dp, greedy, http://cs101.openjudge.cn/pctbook/M20744/


思路：很标准的dp题目，把两种可能的情况都考虑进取就行，练习从底向上的dp写法

```cpp
#include<vector>
#include<stdio.h>
using namespace std;
int max(int a,int b){
    return(a>b)?a:b;
}
int min(int a,int b){
    return(a<b)?a:b;
}
int main(){
    int p,q;
    q=1;
    char s=',';
    vector<int> w;
    while(q!=-1){
        scanf("%d",&p);
        w.push_back(p);
        q=scanf("%c",&s);//最后会读到一个换行
    }
    int n=w.size();
    vector<pair<int,int>>dp(n,{-100000,-100000});
    dp[n-1].first=w[n-1];
    dp[n-3].second=w[n-1]+w[n-3];
    for(int i=n-2;i>=0;i--){
        dp[i].first=max(w[i],dp[i+1].first+w[i]);
        if(i<n-3){        dp[i].second=max(dp[i+2].first,dp[i+1].second)+w[i];
        }
    }
    int ans=-100000;
    for(int i=0;i<n;i++){
        ans=max(ans,max(dp[i].first,dp[i].second));
    }
    printf("%d",ans);
    return 0;
}
```






## M21509: 序列的中位数

heap, http://cs101.openjudge.cn/practice/21509

思路：大顶堆＋小顶堆

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int num_count;  
    cin >> num_count;
    priority_queue<long long> lower_half;
    priority_queue<long long, vector<long long>, greater<long long>> upper_half;
    for (int i = 1; i <= num_count; ++i) {
        long long current_num; 
        cin >> current_num;
        lower_half.push(current_num);
        if (!upper_half.empty() && lower_half.top() > upper_half.top()) {
            long long temp = lower_half.top();
            lower_half.pop();
            upper_half.push(temp);

            temp = upper_half.top();
            upper_half.pop();
            lower_half.push(temp);
        }
        if (lower_half.size() > upper_half.size() + 1) {
            upper_half.push(lower_half.top());
            lower_half.pop();
        } else if (upper_half.size() > lower_half.size()) {
            lower_half.push(upper_half.top());
            upper_half.pop();
        }
        if (i % 2 == 1) {
            cout << lower_half.top() << endl;  
        }
    }

    return 0;
}
```



## M21554: 排队做实验

greedy, http://cs101.openjudge.cn/pctbook/M21554/

思路：cpp对pair的sort完美适配此题，不用重写cmp函数

```cpp
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



## M22275: 二叉搜索树的遍历

http://cs101.openjudge.cn/practice/22275/


思路：左子树所有节点值小于根节点，右子树所有节点值大于根节点。结合前序遍历，通过递归划分左右子树，最终得到后序遍历

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> getPostorder(vector<int>& pre, int l, int r) {
    if (l > r) return {}; 
    int root = pre[l];   
    int mid = l + 1;
    while (mid <= r && pre[mid] < root) {
        mid++;
    }
 
    vector<int> left = getPostorder(pre, l + 1, mid - 1);
    vector<int> right = getPostorder(pre, mid, r);
    vector<int> res;
    res.insert(res.end(), left.begin(), left.end());
    res.insert(res.end(), right.begin(), right.end());
    res.push_back(root);
    return res;
}

int main() {
    int n;
    cin >> n;
    vector<int> pre(n);
    for (int i = 0; i < n; ++i) {
        cin >> pre[i];
    }
    vector<int> post = getPostorder(pre, 0, n - 1);
    for (size_t i = 0; i < post.size(); ++i) {
        if (i > 0) cout << " ";
        cout << post[i];
    }
    cout << endl;
    return 0;
}
```





## M23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555

要求用节省内存的方式实现，不能还原矩阵的方式实现。

思路：利用STL容器思路，对矩阵Y采用行优先的存储方式，实现稀疏矩阵的存储与计算，本题难度可以接受，算上思考时间使用20分钟左右。

```cpp
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

```cpp
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





```cpp
#include <bits/stdc++.h>

using namespace std;

#define all(x) begin(x), end(x)
#define sz(x) (int) (x).size()

using i64 = long long;
using u64 = unsigned long long;
using i128 = __int128_t;
using u128 = __uint128_t;
using pii = pair<int, int>;
using vi = vector<int>;
using usi = unordered_set<int>;

void solve() {
    string str;
    cin >> str;
    stack<char> op;
    stack<string> val;
    vector<string> ans;
    string cur = "";
    for (auto ch : str) {
        if (isdigit(ch) || ch == '.') {
            cur.push_back(ch);
            continue;
        }
        if (!cur.empty()) {
            val.push(cur);
            cur.clear();
        }
        if (ch == '(') {
            op.push('(');
        } else if (ch == '+' || ch == '-') {
            while (!op.empty() &&
                   (op.top() == '*' || op.top() == '/')) {
                char tmp = op.top();
                op.pop();
                string val1 = val.top();
                val.pop();
                string val2 = val.top();
                val.pop();
                val.push(val2 + " " + val1 + " " + tmp);
            }
            while (!op.empty() &&
                   (op.top() == '+' || op.top() == '-')) {
                char tmp = op.top();
                op.pop();
                string val1 = val.top();
                val.pop();
                string val2 = val.top();
                val.pop();
                val.push(val2 + " " + val1 + " " + tmp);
            }
            op.push(ch);
        } else if (ch == '*' || ch == '/') {
            while (!op.empty() &&
                   (op.top() == '*' || op.top() == '/')) {
                char tmp = op.top();
                op.pop();
                string val1 = val.top();
                val.pop();
                string val2 = val.top();
                val.pop();
                val.push(val2 + " " + val1 + " " + tmp);
            }
            op.push(ch);
        } else {
            while (op.top() != '(') {
                char tmp = op.top();
                op.pop();
                string val1 = val.top();
                val.pop();
                string val2 = val.top();
                val.pop();
                val.push(val2 + " " + val1 + " " + tmp);
            }
            op.pop();
        }
    }
    if (!cur.empty()) { val.push(cur); }
    while (!val.empty() && !op.empty()) {
        char tmp = op.top();
        op.pop();
        string val1 = val.top();
        val.pop();
        string val2 = val.top();
        val.pop();
        val.push(val2 + " " + val1 + " " + tmp);
    }
    cout << val.top() << '\n';
}

int main() {
    cin.tie(nullptr)->sync_with_stdio(false);
    int t;
    cin >> t;
    while (t--) { solve(); }
    return 0;
}
```





## M24684: 直播计票

http://cs101.openjudge.cn/practice/24684/

思路：用字典的方式记录选票，在查询最大票数的同时记录答案数组

```cpp
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



## M24729: 括号嵌套树

dfs, stack, [http://cs101.openjudge.cn/practice/24729/](http://cs101.openjudge.cn/practice/24729/)

思路：注意到树的构建与栈是一致的，用栈来辅助构建会很方便，非常简单，用时约15min

 

```cpp
#include <iostream>  
#include <vector>  
#include <map>  
#include <string>  
#include <sstream>  
using namespace std;  
struct TreeNode  
{  
    char name;  
    vector<TreeNode*> children;  
    TreeNode(char c) : name(c) {}  
};  
class Solution   
{  
public:  
    TreeNode* root;  
    void getTree()  
    {  
        char c;  
        TreeNode* lastnode;  
        vector<TreeNode*> stack;  
        while (cin >> c)  
        {  
            if (c == ',')continue;  
            if (c == '(')  
                stack.push_back(lastnode);  
            else if (c == ')')  
                stack.pop_back();  
            else  
            {  
                TreeNode* node = new TreeNode(c);  
                if (stack.empty())  
                    root = node;  
                else  
                    stack.back()->children.push_back(node);  
                lastnode = node;  
            }  
        }     
    }  
    void printTree_1(TreeNode* node)  
    {  
        if (node == nullptr)return;  
        cout << node->name;  
        for (auto child : node->children)  
            printTree_1(child);  
    }  
    void printTree_2(TreeNode* node)  
    {  
        if (node == nullptr)return;  
        for (auto child : node->children)  
            printTree_2(child);  
        cout << node->name;  
    }  
};  
int main()   
{  
    Solution s;  
    s.getTree();  
    s.printTree_1(s.root);  
    cout << endl;  
    s.printTree_2(s.root);  
    return 0;  
}  

```

 ​

思路：用栈解析括号表达式建树，再递归输出前序与后序序列。

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <cctype>
using namespace std;

struct Node {
    char val;
    vector<Node*> children;
    Node(char c) : val(c) {}
};

void preorder(Node* root) {
    if (!root) return;
    cout << root->val;
    for (auto child : root->children)
        preorder(child);
}

void postorder(Node* root) {
    if (!root) return;
    for (auto child : root->children)
        postorder(child);
    cout << root->val;
}

int main() {
    string s;
    cin >> s;
    stack<Node*> st;
    Node* root = nullptr;
    Node* last = nullptr;

    for (int i = 0; i < (int)s.size(); ++i) {
        char c = s[i];
        if (isupper(c)) { 
            Node* node = new Node(c);
            if (!st.empty())
                st.top()->children.push_back(node);
            else
                root = node;
            last = node;
        } else if (c == '(') {
            st.push(last);
        } else if (c == ')') {
            st.pop();
        } else if (c == ',') {
            continue;
        }
    }

    preorder(root);
    cout << "\n";
    postorder(root);
    cout << "\n";

    return 0;
}
```





## M25145: 猜二叉树（按层次遍历）

http://cs101.openjudge.cn/practice/25145/

思路：先根据二叉树的中序遍历和后序遍历序列构建二叉树，然后进行层次遍历

```cpp
#include <iostream>
#include <string>
#include <queue>
using namespace std;

struct TreeNode {
    char val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(char c) : val(c), left(nullptr), right(nullptr) {}
};
TreeNode* buildTree(string& inorder, int inStart, int inEnd, string& postorder, int postStart, int postEnd) {
    if (inStart > inEnd) return nullptr; 
    char rootVal = postorder[postEnd];  
    TreeNode* root = new TreeNode(rootVal);
    int rootIdx = inorder.find(rootVal, inStart); 
    int leftLen = rootIdx - inStart;          
    root->left = buildTree(inorder, inStart, rootIdx - 1, postorder, postStart, postStart + leftLen - 1);
    root->right = buildTree(inorder, rootIdx + 1, inEnd, postorder, postStart + leftLen, postEnd - 1);
    return root;
}
string levelOrder(TreeNode* root) {
    if (!root) return "";
    queue<TreeNode*> q;
    q.push(root);
    string res;
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        res += node->val;
        if (node->left) q.push(node->left);
        if (node->right) q.push(node->right);
    }
    return res;
}

int main() {
    int n;
    cin >> n;
    while (n--) {
        string inorder, postorder;
        cin >> inorder >> postorder;
        TreeNode* root = buildTree(inorder, 0, inorder.size() - 1, postorder, 0, postorder.size() - 1);
        cout << levelOrder(root) << endl;
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



```cpp
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



```cpp
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
> ```cpp
> class Model {
>     string name;
>     double value;
> };
> ```
>
> - 默认是 **private**
> - 你必须提供 getter 或者把成员改成 `public`：
>
> ```cpp
> class Model {
> public:
>     string name;
>     double value;
> };
> ```



思路：核心在数据的接收上，排序可以直接sort()，只要数据接收正确就可以，用时约10分钟

```cpp
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



思路：学习了cpp的正则表达式 (感觉没python的好用)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Model {
public:
    string name;
    double arg;
    string raw_arg;

    Model(string name, double arg, string raw_arg) : name(name), arg(arg), raw_arg(raw_arg) {}

    // 重载小于运算符
    bool operator<(const Model& other) const {
        if (this->name != other.name) {
            return this->name < other.name;
        }
        return this->arg < other.arg;
    }

    // 从字符串中解析出Model对象
    static Model parse(const string& s) {
        const regex pattern(R"(^(.+)-([\d.]+)([MB])$)");
        smatch match;

        if (regex_match(s, match, pattern)) {
            string name = match.str(1);
            double num = stod(match.str(2));
            string unit = match.str(3);
            string raw_arg = match.str(2) + unit;
            double value = num * (unit == "B" ? 1e9 : (unit == "M" ? 1e6 : 1));
            return Model(name, value, raw_arg);
        }
        throw invalid_argument("Invalid model format");
    }
};

int main() {
    int n;
    cin >> n;
    vector<Model> models;
    for (int i = 0; i < n; i++) {
        string s;
        cin >> s;
        models.push_back(Model::parse(s));
    }
    sort(models.begin(), models.end());

    for (int i = 0; i < n; i++) {
        cout << models[i].name << ": " << models[i].raw_arg;
        while (i + 1 < n && models[i].name == models[i + 1].name) {
            i++;
            cout << ", " << models[i].raw_arg;
        }
        cout << endl;
    }
    return 0;
}
```

> 用时30min



## M27306: 植物观察

disjoint set, bfs, http://cs101.openjudge.cn/practice/27306/

思路：典型二分图判断

```cpp
#include <iostream>
#include <vector>
using namespace std;

const int MAX_N = 105;  
int parent[MAX_N];     
int relation[MAX_N];    
void init(int n) {
    for (int i = 0; i < n; ++i) {
        parent[i] = i;  
        relation[i] = 0; 
    }
}
int find(int x) {
    if (parent[x] != x) {
        int origin_parent = parent[x];
        parent[x] = find(parent[x]); 
        relation[x] ^= relation[origin_parent];
    }
    return parent[x];
}

int main() {
    int n, m;
    cin >> n >> m;
    init(n);
    bool possible = true;  
    for (int i = 0; i < m; ++i) {
        int a, b, op;
        cin >> a >> b >> op;
        int root_a = find(a);
        int root_b = find(b);
        if (root_a == root_b) {
            if ((relation[a] ^ relation[b]) != op) {
                possible = false;
            }
        } else {
            parent[root_b] = root_a;
            relation[root_b] = relation[a] ^ relation[b] ^ op;
        }
    }
    cout << (possible ? "YES" : "NO") << endl;
    return 0;
}
```



思路：和LC886 可能的二分法一样，唯一不同的就是不仅要求某两个不在一组，还要求某两个在一组。

```cpp
#include<iostream>
#include<vector>
#include<queue>
#include<algorithm>
using namespace std;
int find(vector<int>& parent,int i){
    if(i!=parent[i]){
        return find(parent,parent[i]);
    }
    return i;
}
void Union(vector<int>& parent,int i,int j){
    parent[find(parent,i)]=find(parent,j);
}
int main(){
    int n,m;
    cin>>n>>m;
    int flag=1;
    vector<vector<int>>different(n);
    vector<int>parent(n);
    for(int i=0;i<n;i++){
        parent[i]=i;
    }
    for(int i=0;i<m;i++){
        int p,q,r;
        cin>>p>>q>>r;
        if(r==0){
            Union(parent,p,q);
        }
        else{
            different[p].push_back(q);
            different[q].push_back(p);
        }
    }
    for(int i=0;i<n;i++){
        if(different[i].size()==0) 
        {continue;}
        int p=find(parent,i);
        int q=find(parent,different[i][0]);
        if(q==p)
        {
            flag=0;
            break;
        }
        if(different[i].size()>=2)
        {
            for(int j=1;j<different[i].size();j++)
            {
                if(find(parent,i)==find(parent,different[i][j])) {
                    flag=0;
                    break;
                }
                Union(parent,different[i][0],different[i][j]);
            } 
            if(flag==0) break;  
        }
    }
    if (flag==1){
        cout<<"YES";
    }
    else{
        cout<<"NO";
    }
    return 0;
}
  
```

### 



## M27925 小组队列

思路：

- 考虑维护一个**双向**链表，链表节点中除当前点的编号外，存储**在队列中**的上一个点和下一个点和**在当前小组中**的上一个点和下一个点。
- ~~好像做麻烦了？~~

- 之前一直没写过 C++ 指针版的链表啊！于是来写了一发，踩了不少坑 /ll
- 总的来说，需要注意的地方有：(1) 检查“小组队列”的始末 `ahead`、`atail` 和每个小组的末端 `ttail[bel]` 是否需要更新；(2) 判断指针是否为空。

```cpp
#include <iostream>
#include <sstream>

using namespace std;

struct LinkList {
	int id;
	LinkList *aprev;
	LinkList *anext;
	LinkList *tprev;
	LinkList *tnext;
	
	LinkList(int _id) : id(_id), aprev(nullptr), anext(nullptr), tprev(nullptr), tnext(nullptr) {}
};

int team;
LinkList *ahead = nullptr, *atail = nullptr;
int belong[1000000];
LinkList *ttail[50099];

void insert(int x){
	LinkList *cur = new LinkList(x);
	if (belong[x] == 0) belong[x] = ++team;
	if (ttail[belong[x]] == nullptr){
		ttail[belong[x]] = cur;
		cur->aprev = atail;
		if (atail != nullptr) atail->anext = cur;
		atail = cur;
		if (ahead == nullptr) ahead = cur;
	} else {
		LinkList *aft = ttail[belong[x]];
		cur->anext = aft->anext;
		if (aft->anext != nullptr) aft->anext->aprev = cur;
		cur->aprev = aft;
		aft->anext = cur;
		cur->tprev = aft;
		aft->tnext = cur;
		ttail[belong[x]] = cur;
		if (atail == aft) atail = cur;
	}
}

void pop(){
	LinkList *nxt = ahead->anext;
	if (ahead->anext != nullptr){
		ahead->anext->aprev = nullptr;
		ahead->anext = nullptr;
	} else {
		atail = nullptr;
	}
	if (ahead->tnext != nullptr){
		ahead->tnext->tprev = nullptr;
		ahead->tnext = nullptr;
	} else {
		ttail[belong[ahead->id]] = nullptr;
	}
	delete ahead;
	ahead = nxt;
}

void finalize(){
	while (ahead != nullptr){
		LinkList *nxt = ahead->anext;
		delete ahead;
		ahead = nxt;
	}
}

int main(){
	cin >> team;
	getchar();
	for (int i = 1; i <= team; i++){
		int id;
		string line;
		getline(cin, line);
		stringstream scin(line);
		while (scin >> id){
			belong[id] = i;
		}
	}
	while (true){
		string op;
		cin >> op;
		if (op == "STOP") break;
		if (op == "ENQUEUE"){
			int x;
			cin >> x;
			insert(x);
		} else {
			cout << ahead->id << endl;
			pop();
		}
	}
	finalize();
	return 0;
}
```





## M27928: 遍历树

 adjacency list, dfs, http://cs101.openjudge.cn/practice/27928/

思路：对每个节点，将它与所有子节点的值一起按从小到大排序，先递归遍历比它小的子节点，最后输出自己，这样整棵树按规则完成遍历。

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <set>
#include <algorithm>
using namespace std;

void dfs(int u, map<int, vector<int>>& son) {

    vector<int> tmp = son[u];
    tmp.push_back(u);
    sort(tmp.begin(), tmp.end());
    
    for (int v : tmp) {
        if (v == u) {
            cout << u << "\n";  
        } else {
            dfs(v, son);       
        }
    }
}

int main() {
    int n;
    cin >> n;

    map<int, vector<int>> son;  
    set<int> all_nodes;         
    set<int> non_roots;         


    for (int i = 0; i < n; ++i) {
        int parent;
        cin >> parent;
        all_nodes.insert(parent);
        string line;
        getline(cin, line);  
        int num = 0;
        bool has_num = false;


        for (char c : line) {
            if (isdigit(c)) {
                num = num * 10 + (c - '0');
                has_num = true;
            } else if (has_num) {
                son[parent].push_back(num);
                non_roots.insert(num);
                all_nodes.insert(num);
                num = 0;
                has_num = false;
            }
        }
        if (has_num) { 
            son[parent].push_back(num);
            non_roots.insert(num);
            all_nodes.insert(num);
        }
    }


    vector<int> roots;
    for (int x : all_nodes)
        if (!non_roots.count(x))
            roots.push_back(x);

    sort(roots.begin(), roots.end());


    for (int r : roots)
        dfs(r, son);

    return 0;
}
```



思路：需要用 `getline` 一行行读取数据, 且题目没有给出根节点, 以及节点的顺序不固定, 因此用 `unordered_map` 邻接表存储树, 建树并找到根结点后遍历即可

```cpp
#include <bits/stdc++.h>
using namespace std;

// 用邻接表存储树结构
unordered_map<int, vector<int>> tree;

void dfs(int root) {
    vector<int> children = tree[root];
    children.push_back(root);
    sort(children.begin(), children.end());

    for (int child : children) {
        if (child == root) {
            cout << root << '\n';
        } else {
            dfs(child);
        }
    }
}

int main() {
    int n;
    cin >> n;
    string line;
    getline(cin, line); // 读取剩余的换行符
    unordered_set<int> child;
    unordered_set<int> all_nodes;
    
    for (int i = 0; i < n; i++) {
        getline(cin, line);
        stringstream ss(line);  // 初始化 stringstream 对象
        int u, v;
        ss >> u;
        all_nodes.insert(u);
    
        while (ss >> v) {
            tree[u].push_back(v);
            child.insert(v);
        }
    }

    // 找到根节点
    int root = -1;
    for (int node : all_nodes) {
        if (child.count(node) == 0) {
            root = node;
            break;
        }
    }

    dfs(root);
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





## M28906:数的划分

dfs, dp, http://cs101.openjudge.cn/practice/28906

```cpp
#include <iostream>

using namespace std;

int main(){
    int n,k;
    cin>>n>>k;
    int a[n+1][k+1]={};
    for(int i=1;i<=n;i++){
        a[i][1]=1;
    }
    for(int i=1;i<=n;i++){
        for(int j=2;j<=k;j++){
            if(i-j>=0){
                a[i][j]=a[i-j][j]+a[i-1][j-1];
            }
        }
    }
    cout<<a[n][k];
    return 0;
}
```



## M29896:购物

greedy, http://cs101.openjudge.cn/practice/29896



```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main(){
    int x,n;
    cin>>x>>n;
    vector<int> a(n,0);
    for(int i=0;i<n;i++){
        cin>>a[i];
    }
    sort(a.begin(),a.end());
    if(a[0]>1) {cout<<-1;}
    else{
        if(n==1)cout<<x;
        else{
        int sum=a[0];
        int ans=1;
        for(int i=2;i<=x;i++){
            if(i>sum){
                for(int j=n-1;j>=0;j--){
                    if(a[j]<=sum+1){
                        ans++;
                        sum+=a[j];
                        break;
                    }
                }
            }
        }
        cout<<ans;
    }
    }
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



bfs

```cpp
#include <iostream>
#include <queue>
#include <vector>

auto main() -> int {
  std::cin.tie(nullptr)->sync_with_stdio(false);

  int R, C, K;
  std::cin >> R >> C >> K;
  std::vector<std::vector<char>> p(R, std::vector<char>(C));

  int sx, sy, dx, dy;
  for (int i = 0; i < R; ++i)
    for (int j = 0; j < C; ++j) {
      std::cin >> p[i][j];
      if (p[i][j] == 'S')
        sx = i, sy = j;
      if (p[i][j] == 'E')
        dx = i, dy = j;
    }

  std::vector<std::vector<std::vector<int>>> visited(
      R, std::vector<std::vector<int>>(C, std::vector<int>(K + 1, -1)));

  std::queue<std::pair<std::pair<int, int>, int>> q;
  q.push({{sx, sy}, K});
  visited[sx][sy][K] = 0;

  int dict[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

  while (!q.empty()) {
    auto [x, y] = q.front().first;
    int k = q.front().second;
    q.pop();

    if (dx == x && dy == y) {
      std::cout << visited[x][y][k] << '\n';
      return 0;
    }

    for (auto &i : dict) {
      int newX = x + i[0], newY = y + i[1];

      if (newX >= 0 && newX < R && newY >= 0 && newY < C) {
        char c = p[newX][newY];
        int next_k = k;
        if (c == '#') {
          if (next_k > 0)
            --next_k;
          else
            continue;
        }

        if (visited[newX][newY][next_k] == -1) {
          q.push({{newX, newY}, next_k});
          visited[newX][newY][next_k] = visited[x][y][k] + 1;
        }
      }
    }
  }

  std::cout << -1 << '\n';
  return 0;
}
```

>共用时30min



思路：BFS, 队列里存储一个包含当前行, 列, 剩余能量的三元组, 用 `visited` 记录到达当前位置剩余能量的最大值

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int r, c, k, start_row, start_col;
    cin >> r >> c >> k;
    vector<string> maze;
    for (int i = 0; i < r; i++) {
        string s;
        cin >> s;
        maze.push_back(s);
        for (int j = 0; j < c; j++) {
            if (s[j] == 'S') {
                start_row = i;
                start_col = j;
            }
        }
    }

    int step = 0;
    vector<vector<int>> visited(r, vector<int>(c, -1));  // remain k when visited[row][col] is reached
    visited[start_row][start_col] = k;
    queue<tuple<int, int, int>> q; // row, col, remain
    q.push({start_row, start_col, k});
    vector<pair<int, int>> directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    
    while (!q.empty()) {
        int sz = q.size();
        for (int i = 0; i < sz; i++) {
            auto [row, col, remain] = q.front();
            q.pop();

            if (maze[row][col] == 'E') {
                cout << step << endl;
                return 0;
            }
            
            for (auto [dr, dc] : directions) {
                int new_row = row + dr;
                int new_col = col + dc;
                if (new_row >= 0 && new_row < r && new_col >= 0 && new_col < c) {
                    int new_remain = remain;  // Create a new variable to store the updated remain value, instead of modifying the original remain variable
                    if (maze[new_row][new_col] == '#') {
                        new_remain--;
                    }

                    if (new_remain >= 0 && visited[new_row][new_col] < new_remain) {
                        visited[new_row][new_col] = new_remain;
                        q.push({new_row, new_col, new_remain});
                    }
                }
            }
        }
        step++;
    }
    cout << -1 << endl;
    return 0;
}
```







## M30178: 数字华容道（Easy Version）

merge sort, binary indexed tree, http://cs101.openjudge.cn/practice/30178/



思路：容易猜到把二维数组展平后统计逆序对, 但充分性的证明还没想到. (看了群里的 Hard Version 的证明确实觉得优雅)

```c++
#include <bits/stdc++.h>
using namespace std;

class BIT {
private:
    int n;
    vector<int> tree;

    int lowbit(int x) {
        return x & (-x);
    }
    
public:
    BIT(int n) : n(n), tree(n + 1, 0) {}

    void update(int i, int delta=1) {
        for (int j = i; j <= n; j += lowbit(j)) {
            tree[j] += delta;
        }
    }

    int query(int i) {
        int sum = 0;
        for (int j = i; j > 0; j -= lowbit(j)) {
            sum += tree[j];
        }
        return sum;
    }
};

bool is_solvable(const vector<int>& nums, int n, int blank_row) {
    int N = n * n - 1;
    int inverse = 0;
    BIT bit(N);
    vector<int> sorted_nums = nums;
    sort(sorted_nums.begin(), sorted_nums.end());

    for (int i = N - 1; i >= 0; i--) {
        int rank = lower_bound(sorted_nums.begin(), sorted_nums.end(), nums[i]) - sorted_nums.begin() + 1;
        inverse += bit.query(rank - 1);
        bit.update(rank);
    }
    
    if (n & 1) {
        return inverse % 2 == 0;
    } else {
        return (inverse + blank_row) % 2 == 0;
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;
    int blank_row = 0;
    vector<int> nums;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            int x;
            cin >> x;
            if (x == 0) {
                blank_row = n - i - 1;
            } else {
                nums.push_back(x);
            }
        }
    }
    cout << (is_solvable(nums, n, blank_row) ? "yes" : "no") << "\n";
    return 0;
}
```

> 35min



```cpp
#include <iostream>
#include <vector>
using namespace std;

class Fenwick
{
private:
    int n;
    vector<int> tree;

public:
    Fenwick(int n) : n(n), tree(n + 1, 0) {}

    void update(int i)
    {
        while (i <= n)
        {
            ++tree[i];
            i = i + (i & -i);
        }
    }

    int query(int i)
    {
        int sum = 0;
        while (i > 0)
        {
            sum += tree[i];
            i &= i - 1;
        }
        return sum;
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    int n;
    cin >> n;
    int sz = n * n;
    vector<int> matrix;
    int bottom_up;
    for (int i = 0; i < n; ++i)
        for (int j = 0; j < n; ++j)
        {
            int x;
            cin >> x;
            if (x == 0)
                bottom_up = n - i;
            else
                matrix.push_back(x);
        }

    Fenwick bit(sz);
    long long cnt = 0;

    for (int i = matrix.size() - 1; i >= 0; --i)
    {
        cnt += bit.query(matrix[i] - 1);
        bit.update(matrix[i]);
    }

    bool flag = false;
    if (n % 2 != 0)
    {
        if (cnt % 2 == 0)
            flag = true;
    }
    else
    {
        if ((cnt + bottom_up) % 2 == 1)
            flag = true;
    }

    cout << (flag == true ? "yes\n" : "no\n");
    return 0;
}
```

>共用时1h



【姚博骞 25物院】思路：方法是计算每行的逆序数然后分n奇数欧树讨论，这个证明还暂时不会，目前会先把这些相对偏组合数学一些的一些证明先放一放，但是像是kmp算法包括树状数组的证明这种直观上能理解的可以接受即可，严格证明以后可以一起写，现在还是主要提升代码能力。
目前写的是分治法计算逆序数组，需要变归并边排序，时间复杂度较高
还有一种方法是树状数组记录前缀和，考虑一个巨大的数组，从前向后读入，出现了的数字记作1，没出现的记作0，计算当前该数为下标的前缀和，即为前面出现的比该数小的元素个数，用树状数组可以O（logn）进行跟新和查询，故两种方法复杂度均为O(n^2logn),但是树状数组本身写起来比较简单故更快（记得加到cheatsheet上）

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

int nixu(vector<int>& a,int p,int q)
{
    if(p==q) return 0;
    int mid=(p+q)/2;
    int ans=nixu(a,p,mid)+nixu(a,mid+1,q);
    vector<int>b(a.begin()+p,a.begin()+q+1);
    int s,r,nx,leiji;
    s=r=nx=leiji=0;
    int i=p;
    while(s<mid-p+1&&r<q-mid)
    {
        if(b[s]<=b[mid-p+1+r]){
            a[i]=b[s];
            s++;
            nx+=leiji;
        }
        else{
            a[i]=b[mid-p+1+r];
            r++;
            leiji++;
        }
        i++;
    }
    if(s==mid-p+1){
        for(int j=i;j<=q;j++){
            a[j]=b[mid-p+1+r];
            r++;
        }
    }
    else{
        for(int j=i;j<=q;j++){
            a[j]=b[s];
            s++;
            nx+=leiji;
        }
    }
    ans+=nx;
    return ans;
}
int main()
{
    int n;
    cin>>n;
    vector<vector<int>>a(n,vector<int>(n));
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++)
        {
            cin>>a[i][j];
        }
    }
    vector<int>c;
    int p;  // 记录空格所在行
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            if(a[i][j]!=0){
                c.push_back(a[i][j]);
            }
            else{
                p=i;  // 空格所在行
            }
        }
    }
    int ans=nixu(c,0,c.size()-1);  // 逆序对数
    if(n%2==1)  // 奇数列
    {
        if(ans%2==0) cout<<"yes";
        else cout<<"no";
    }
    else  // 偶数列
    {
        if((ans+n-p)%2==1) cout<<"yes";
        else cout<<"no";
    }
    return 0;
}
```



思路：化归到标准情形，然后统计逆序对数．时间复杂度为 $O(n^{2}\log n)$．

一般地，在二分图 $G=(L,R)$ 上可以利用逆序对给出（一个空位的）数字华容道可复原的一个必要条件：将左右部点交替排列 $l_{1},r_{1},l_{2},r_{2},\cdots,l_{n},r_{n}$（若 $|L|\ne|R|$，只需增加一些棋子为 $0$ 的孤点，使之参与逆序对数的统计），则忽略空位后长度为 $2n-1$ 的序列的逆序对数奇偶性是一个操作不变量，从而当前局面与目标局面逆序对数奇偶性相同是复原的必要条件．然而，充分性似乎没有统一的解法，只能根据 $G$ 的结构给出具体构造．

> 充分性其实很好证，因为`n*n`的盘面可以被降阶成 `n-1*n-1`的盘面

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1000 * 1000 + 5;
int a[N];
struct BIT {
    void modify(int n) {
        for(; n < N; n += n & -n) c[n] ^= 1;
    }
    bool query(int n) {
        bool ans = 0;
        for(; n; n -= n & -n) ans ^= c[n];
        return ans;
    }
    bool c[N];
} B;
int main() {
    int n;
    cin >> n;
    bool ans = n % 2 == 0;
    for(int i = 0; i < n * n; i++) {
        int t;
        cin >> t;
        if(t == 0)
            ans ^= (n % 2 == 0) && ((n - 1 - i / n) % 2);
        else {
            ans ^= B.query(t);
            B.modify(t);
        }
    }
    cout << (ans ? "no" : "yes") << '\n';
    return 0;
}
```





## M30218: 狭路相逢

stack, http://cs101.openjudge.cn/practice/M30218/

```cpp
#include <iostream>
#include <vector>

auto main() -> int {
  std::cin.tie(nullptr)->sync_with_stdio(false);

  int N;
  std::cin >> N;
  std::vector<int> st;

  while (N--) {
    int v;
    std::cin >> v;

    bool flag = true;
    while (flag && v < 0 && !st.empty() && st.back() > 0) {
      if (st.back() < -v)
        v = st.back() + v, st.pop_back();
      else if (st.back() == -v)
        st.pop_back(), flag = false;
      else
        st.back() += v, flag = false;
    }

    if (flag)
      st.push_back(v);
  }

  std::cout << st.size() << '\n';

  for (const auto &a : st)
    std::cout << a << ' ';
  return 0;
}
```

>共用时30min



思路：简单的模拟, 维护两个栈即可. 被输出格式卡了一会, 一开始忘记输出存活总数了

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }

    deque<int> soldiers;
    vector<int> monsters;
    for (int i = 0; i < n; i++) {
        if (a[i] < 0) {
            int monster = -a[i];
            while (!soldiers.empty()) {
                int top = soldiers.back();
                soldiers.pop_back();
                if (top > monster) {
                    soldiers.push_back(top - monster);
                    break;
                } else if (top == monster) {
                    monster = 0;
                    break;
                } else {
                    monster -= top;
                }
            }

            if (soldiers.empty() && monster > 0) {
                monsters.push_back(-monster);
            }
        } else {
            soldiers.push_back(a[i]);
        }
    }

    cout << monsters.size() + soldiers.size() << endl;
    for (int monster : monsters) {
        cout << monster << " ";
    }
    for (int soldier : soldiers) {
        cout << soldier << " ";
    }
    return 0;
}
```



## M30637: 合法出栈序列pub

stack, http://cs101.openjudge.cn/practice/M30637/

【黄宇曦 地球与空间科学学院】思路：贪心。直接模拟一下过程就行了。

```cpp
#include <bits/stdc++.h>

using namespace std;

#define all(x) begin(x), end(x)
#define sz(x) (int) (x).size()

using i64 = long long;
using u64 = unsigned long long;
using i128 = __int128_t;
using u128 = __uint128_t;
using pii = pair<int, int>;
using vi = vector<int>;
using usi = unordered_set<int>;

int main() {
    cin.tie(nullptr)->sync_with_stdio(false);
    string str;
    cin >> str;
    cin.ignore();
    string q;
    while (getline(cin, q)) {
        if (q.size() != str.size()) {
            cout << "NO\n";
            continue;
        }
        stack<char> st;
        int i = 0;
        for (auto ch : str) {
            st.push(ch);
            while (st.size() && i < q.size() && st.top() == q[i]) {
                st.pop();
                i++;
            }
        }
        if (st.empty() && i == q.size())
            cout << "YES\n";
        else
            cout << "NO\n";
    }
    return 0;
}
```



【江昊中 数学科学学院】思路：合法字符串的充要条件是每一字符后的所有比它序号更小的字符必须是降序排列的 (至于 `cin` 会跳过空行, 以及会出现原字符串里没有的字符的情况我是完全没考虑)

```c++
#include<bits/stdc++.h>
using namespace std;
const int M = 10005;

int main() {
    string s;
    getline(cin, s);
    int n = s.length();
    unordered_map<char, int> mp;
    for (int i = 0; i < n; i++) {
        mp[s[i]] = i;
    }

    while (getline(cin, s)) {
        if (s.length() != n) {
            cout << "NO" << endl;
            continue;
        }
        bool possible = true;
        for (int i = 0; i < n; i++) {
            if (!mp.count(s[i])) {
                possible = false;
                break;
            }
            int idx = mp[s[i]];
            int last = idx;
            for (int j = i + 1; j < n; j++) {
                int cur_idx = mp[s[j]];
                if (cur_idx < idx) {
                    if (cur_idx > last) {
                        possible = false;
                        break;
                    }
                    last = cur_idx;
                }
            }

        }
        if (possible) {
            cout << "YES" << endl;
        } else {
            cout << "NO" << endl;
        }
    }
    return 0;
}
```





# OJ挑战

## 01019: Number Sequence

http://cs101.openjudge.cn/practice/01019/

```cpp
#include <iostream>
using namespace std;

typedef long long ll;
class Solution
{
private:
    ll get_Sk_len(ll k)
    {
        ll len = 0;
        for (ll start = 1, digits = 1; start <= k; start *= 10, digits++)
        {
            ll end = start * 10 - 1;
            if (end > k)
                end = k;
            len += (end - start + 1) * digits;
        }
        return len;
    }

    ll get_total_len(ll k)
    {
        ll total = 0;
        for (ll start = 1, digits = 1; start <= k; start *= 10, digits++)
        {
            ll end = start * 10 - 1;
            if (end > k)
                end = k;

            ll first_Sk_len = get_Sk_len(start);
            ll last_Sk_len = get_Sk_len(end);
            ll n = (end - start + 1);

            total += (first_Sk_len + last_Sk_len) * n / 2;
        }
        return total;
    }

public:
    char solve(int x)
    {
        ll l = 1, r = 31268, k = 1;
        while (l <= r)
        {
            ll mid = l + (r - l) / 2;
            if (get_total_len(mid) >= x)
            {
                k = mid;
                r = mid - 1;
            }
            else
            {
                l = mid + 1;
            }
        }

        x -= get_total_len(k - 1);

        l = 1, r = k;
        ll num = 1;
        while (l <= r)
        {
            ll mid = l + (r - l) / 2;
            if (get_Sk_len(mid) >= x)
            {
                num = mid;
                r = mid - 1;
            }
            else
            {
                l = mid + 1;
            }
        }

        x -= get_Sk_len(num - 1);
        string s = to_string(num);
        return s[x - 1];
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);
    int t;
    cin >> t;
    Solution sol;
    while (t--)
    {
        ll x;
        cin >> x;
        cout << sol.solve(x) << '\n';
    }
    return 0;
}
```





## T01661: Help Jimmy

dfs/dp, [http://cs101.openjudge.cn/practice/01661](http://cs101.openjudge.cn/practice/01661) 做了4-5h才完全搞明白这道题...... 一开始忘记考虑`y - p[i].h > MaxVal`时的返回值了，导致返回的是默认值0，在这里卡了很久，也就是说它作为一个单纯的DFS题就已经不是很容易了，结果写完以后发现超时了，做了剪枝之后发现还是超时，然后就借助ai得知了记忆化搜索这个工具，然后又在key上面卡了好久，最后还是写出来了。

 

```cpp
#include <iostream>  
#include <algorithm>  
#include <vector>  
#include <unordered_map>  
using namespace std;  

int minTime, MaxVal;  
 
struct Node  
{  
    int r, l, h;  
};  
 
bool cmp(Node a, Node b)  
{  
    return a.h > b.h;  
}  
 
unordered_map<long long, int> memo;  

long long encode(int x, int y, int it)  
{  
    return ((long long)x << 32) | ((long long)y << 16) | it;  
}  

int dfs(vector<Node>& p, int x, int y, int it)  
{  
    long long key = encode(x, y, it);  
    if (memo.count(key))  
        return memo[key];  
    for (int i = it + 1; i < p.size(); i++)  
    {  
        if (y - p[i].h > MaxVal)  
            return memo[key] = 1e9;  
        else if (x >= p[i].l && x <= p[i].r)  
        {  
            int l = x - p[i].l + dfs(p, p[i].l, p[i].h, i);  
            int r = p[i].r - x + dfs(p, p[i].r, p[i].h, i);  
            return memo[key] = l < r ? l : r;  
        }  
    }  
    return memo[key] = 0;  
}  

int main()  
{  
    ios::sync_with_stdio(false);  
    cin.tie(nullptr);  

    int k;  
    cin >> k;  
    while (k--)  
    {  
        int n, inix, iniy;  
        cin >> n >> inix >> iniy >> MaxVal;  
        vector<Node> plat;  
        Node floor;  
        floor.l = inix, floor.r = inix, floor.h = iniy;  
        plat.push_back(floor);  
        while (n--)  
        {  
            Node ipt;  
            cin >> ipt.l >> ipt.r >> ipt.h;  
            plat.push_back(ipt);  
        }  
        sort(plat.begin(), plat.end(), cmp);  
        cout << iniy + dfs(plat, inix, iniy, 0) << '\n';  
    }  
    return 0;  
}
```



## T01958: Strange Towers of Hanoi

[http://cs101.openjudge.cn/practice/01958/](http://cs101.openjudge.cn/practice/01958/)

 

```cpp
#include <iostream>  
#include <cmath>  
using namespace std;  

int dp(int n)  
{  
    if (n == 1)  
        return 1;  
    int maxMov = 1e9;  
    for (int k = 1; k < n; k++)  
        maxMov = min(maxMov, 2 * dp(n - k) + int(pow(2, k)) - 1);  
    return maxMov;  
}  

int main()  
{  
    for (int i = 1; i <= 12; i++)  
        cout << dp(i) << '\n';  
    return 0;  
}
```



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


## T02754: 八皇后

dfs and similar, [http://cs101.openjudge.cn/pctbook/T02754](http://cs101.openjudge.cn/pctbook/T02754)

 

```cpp
#include <iostream>  
#include <algorithm>  
#include <vector>  
using namespace std;  
  
bool is_valid(string& queen, int x, int y)  
{  
    for (int i = 1; i < x; i++)  
        if (int(queen[i] - '0') == y || abs(i - x) == abs(int(queen[i] - '0') - y))  
            return false;  
    return true;  
}  
  
void sovle_8_queens(vector<string>& sol, string& queen, int n)  
{  
    if (n == 9)  
        sol.push_back(queen);  
    else  
        for (int i = 1; i <= 8; i++)  
            if (is_valid(queen, n, i))  
            {  
                queen[n] = i + '0';  
                sovle_8_queens(sol, queen, n + 1);  
                queen[n] = '0';  
            }  
}  
  
int main()  
{  
    ios::sync_with_stdio(false);  
    cin.tie(nullptr);  
  
    int n;  
    cin >> n;  
  
    vector<string> solutions;  
    string queen = "000000000";  
    sovle_8_queens(solutions, queen, 1);  
    vector<int> sol;  
    for (auto i : solutions)  
        sol.push_back(stoi(i));  
    sort(sol.begin(), sol.end());  
  
    while (n--)  
    {  
        int k;  
        cin >> k;  
        cout << sol[k - 1] << '\n';  
    }  
    return 0;  
}
```




## T02775: 文件结构“图”

tree, http://cs101.openjudge.cn/practice/02775/

思路：用栈维护当前目录层次，每遇到目录就入栈、遇到 ] 出栈，递归输出目录与文件。

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <stack>
#include <algorithm>
using namespace std;

bool isDir(const string& name) {
    return !name.empty() && name[0] == 'd';
}

void dfs(int dir, const string& prefix,
         const vector<string>& name,
         const vector<vector<int>>& subdirs,
         const vector<vector<string>>& subfiles) {
    cout << prefix << name[dir] << "\n";
    string subprefix = prefix + "|     ";
    for (int subdir : subdirs[dir]) {
        dfs(subdir, subprefix, name, subdirs, subfiles);
    }
    vector<string> files = subfiles[dir];
    sort(files.begin(), files.end());
    for (const string& f : files) {
        cout << prefix << f << "\n";
    }
}

bool solve(int cas) {
    int id = 0;
    vector<string> name(1, "ROOT");
    vector<vector<int>> subdirs(1);
    vector<vector<string>> subfiles(1);
    stack<int> stk;
    stk.push(0);
    string line;

    while (true) {
        if (!getline(cin, line))
            return false;
        if (line == "#") return false;
        if (line == "*") break;

        if (isDir(line)) {
            ++id;
            name.push_back(line);
            subdirs.push_back({});
            subfiles.push_back({});
            subdirs[stk.top()].push_back(id);
            stk.push(id);
        } else if (line == "]") {
            stk.pop();
        } else {
            subfiles[stk.top()].push_back(line);
        }
    }

    cout << "DATA SET " << cas << ":\n";
    dfs(0, "", name, subdirs, subfiles);
    cout << "\n";
    return true;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int cas = 1;
    while (solve(cas)) {
        ++cas;
    }
    return 0;
}
```



## T16926: 魔兽世界三(开战)

OOP implementation, http://cs101.openjudge.cn/practice/16926/

魔兽世界的西面是红魔军的司令部，东面是蓝魔军的司令部。两个司令部之间是依次排列的若干城市，城市从西向东依次编号为1,2,3 .... N ( N <= 20)。红魔军的司令部算作编号为0的城市，蓝魔军的司令部算作编号为N+1的城市。司令部有生命元，用于制造武士。



两军的司令部都会制造武士。武士一共有dragon 、ninja、iceman、lion、wolf 五种。每种武士都有编号、生命值、攻击力这三种属性。



双方的武士编号都是从1开始计算。红方制造出来的第n 个武士，编号就是n。同样，蓝方制造出来的第n 个武士，编号也是n。



武士在刚降生的时候有一个初始的生命值，生命值在战斗中会发生变化，如果生命值减少到0（生命值变为负数时应当做变为0处理），则武士死亡（消失）。

武士可以拥有武器。武器有三种，sword, bomb,和arrow，编号分别为0,1,2。

sword的攻击力是使用者当前攻击力的20%(去尾取整)。

bomb的攻击力是使用者当前攻击力的40%(去尾取整)，但是也会导致使用者受到攻击，对使用者的攻击力是对敌人取整后的攻击力的1/2(去尾取整)。Bomb一旦使用就没了。

arrow的攻击力是使用者当前攻击力的30%(去尾取整)。一个arrow用两次就没了。





武士降生后就朝对方司令部走，在经过的城市如果遇到敌人（同一时刻每个城市最多只可能有1个蓝武士和一个红武士），就会发生战斗。战斗的规则是：

1. 在奇数编号城市，红武士先发起攻击
2. 在偶数编号城市，蓝武士先发起攻击
3. 战斗开始前，双方先对自己的武器排好使用顺序，然后再一件一件地按顺序使用。编号小的武器，排在前面。若有多支arrow，用过的排在前面。排好序后，攻击者按此排序依次对敌人一件一件地使用武器。如果一种武器有多件，那就都要用上。每使用一件武器，被攻击者生命值要减去武器攻击力。如果任何一方生命值减为0或小于0即为死去。有一方死去，则战斗结束。
4. 双方轮流使用武器，甲用过一件，就轮到乙用。某一方把自己所有的武器都用过一轮后，就从头开始再用一轮。如果某一方没有武器了，那就挨打直到死去或敌人武器用完。武器排序只在战斗前进行，战斗中不会重新排序。
5. 如果双方武器都用完且都还活着，则战斗以平局结束。如果双方都死了，也算平局。
6. 有可能由于武士自身攻击力太低，而导致武器攻击力为0。攻击力为0的武器也要使用。如果战斗中双方的生命值和武器的状态都不再发生变化，则战斗结束，算平局。
7. 战斗的胜方获得对方手里的武器。武士手里武器总数不超过10件。缴获武器时，按照武器种类编号从小到大缴获。如果有多件arrow，优先缴获没用过的。
8. 如果战斗开始前双方都没有武器，则战斗视为平局。如果先攻击方没有武器，则由后攻击方攻击。

不同的武士有不同的特点。

编号为n的dragon降生时即获得编号为n%3 的武器。dragon在战斗结束后，如果还没有战死，就会欢呼。



编号为n的ninjia降生时即获得编号为n%3 和(n+1)%3的武器。ninja 使用bomb不会让自己受伤。



编号为n的iceman降生时即获得编号为n%3 的武器。iceman每前进一步，生命值减少10%(减少的量要去尾取整)。



编号为n的lion降生时即获得编号为n%3 的武器。lion 有“忠诚度”这个属性，其初始值等于它降生之后其司令部剩余生命元的数目。每前进一步忠诚度就降低K。忠诚度降至0或0以下，则该lion逃离战场,永远消失。但是已经到达敌人司令部的lion不会逃跑。lion在己方司令部可能逃跑。



wolf降生时没有武器，但是在战斗开始前会抢到敌人编号最小的那种武器。如果敌人有多件这样的武器，则全部抢来。Wolf手里武器也不能超过10件。如果敌人arrow太多没法都抢来，那就先抢没用过的。如果敌人也是wolf，则不抢武器。



以下是不同时间会发生的不同事件：



在每个整点，即每个小时的第0分， 双方的司令部中各有一个武士降生。



红方司令部按照iceman、lion、wolf、ninja、dragon 的顺序制造武士。



蓝方司令部按照lion、dragon、ninja、iceman、wolf 的顺序制造武士。



制造武士需要生命元。



制造一个初始生命值为m 的武士，司令部中的生命元就要减少m 个。



如果司令部中的生命元不足以制造某本该造的武士，那就从此停止制造武士。



在每个小时的第5分，该逃跑的lion就在这一时刻逃跑了。



在每个小时的第10分：所有的武士朝敌人司令部方向前进一步。即从己方司令部走到相邻城市，或从一个城市走到下一个城市。或从和敌军司令部相邻的城市到达敌军司令部。



在每个小时的第35分：在有wolf及其敌人的城市，wolf要抢夺对方的武器。



在每个小时的第40分：在有两个武士的城市，会发生战斗。



在每个小时的第50分，司令部报告它拥有的生命元数量。



在每个小时的第55分，每个武士报告其拥有的武器情况。



武士到达对方司令部后就算完成任务了，从此就呆在那里无所事事。 



任何一方的司令部里若是出现了敌人，则认为该司令部已被敌人占领。

任何一方的司令部被敌人占领，则战争结束。战争结束之后就不会发生任何事情了。



给定一个时间，要求你将从0点0分开始到此时间为止的所有事件按顺序输出。事件及其对应的输出样例如下：



1) 武士降生

输出样例：000:00 blue dragon 1 born 

表示在0点0分，编号为1的蓝魔dragon武士降生



如果造出的是lion，那么还要多输出一行，例:

000:00 blue lion 1 born

Its loyalty is 24

表示该lion降生时的忠诚度是24



2) lion逃跑

输出样例：000:05 blue lion 1 ran away 

表示在0点5分，编号为1的蓝魔lion武士逃走



3) 武士前进到某一城市



输出样例：



000:10 red iceman 1 marched to city 1 with 20 elements and force 30

表示在0点10分，红魔1号武士iceman前进到1号城市，此时他生命值为20,攻击力为30

对于iceman,输出的生命值应该是变化后的数值



4) wolf抢敌人的武器

000:35 blue wolf 2 took 3 bomb from red dragon 2 in city 4

表示在0点35分，4号城市中，红魔1号武士wolf 抢走蓝魔2号武士dragon 3个bomb。为简单起见，武器不写复数形式



5) 报告战斗情况

战斗只有3种可能的输出结果：



000:40 red iceman 1 killed blue lion 12 in city 2 remaining 20 elements 

表示在0点40分，1号城市中，红魔1号武士iceman 杀死蓝魔12号武士lion后，剩下生命值20



000:40 both red iceman 1 and blue lion 12 died in city 2

注意，把红武士写前面

000:40 both red iceman 1 and blue lion 12 were alive in city 2

注意，把红武士写前面



6) 武士欢呼

输出样例：003:40 blue dragon 2 yelled in city 4



7) 武士抵达敌军司令部

输出样例：001:10 red iceman 1 reached blue headquarter with 20 elements and force 30

（此时他生命值为20,攻击力为30）对于iceman,输出的生命值和攻击力应该是变化后的数值



8) 司令部被占领

输出样例：003:10 blue headquarter was taken



9)司令部报告生命元数量

000:50 100 elements in red headquarter 

000:50 120 elements in blue headquarter

表示在0点50分，红方司令部有100个生命元，蓝方有120个



10)武士报告情况

000:55 blue wolf 2 has 2 sword 3 bomb 0 arrow and 7 elements

为简单起见，武器都不写复数形式。elements一律写复数，哪怕只有1个



交代武器情况时，次序依次是：sword,bomb, arrow。



输出事件时：



首先按时间顺序输出；

同一时间发生的事件，按发生地点从西向东依次输出. 武士前进的事件, 算是发生在目的地。

在一次战斗中有可能发生上面的 5 至 6 号事件。这些事件都算同时发生，其时间就是战斗开始时间。一次战斗中的这些事件，序号小的应该先输出。

两个武士同时抵达同一城市，则先输出红武士的前进事件，后输出蓝武士的。

对于同一城市，同一时间发生的事情，先输出红方的，后输出蓝方的。

显然，8号事件发生之前的一瞬间一定发生了7号事件。输出时，这两件事算同一时间发生，但是应先输出7号事件

虽然任何一方的司令部被占领之后，就不会有任何事情发生了。但和司令部被占领同时发生的事件，全都要输出。



**输入**

第一行是t,代表测试数据组数

每组样例共三行。

第一行，4个整数 M,N,K, T。其含义为：
每个司令部一开始都有M个生命元( 1 <= M <= 100000)
两个司令部之间一共有N个城市( 1 <= N <= 20 )
lion每前进一步，忠诚度就降低K。(0<=K<=100)
要求输出从0时0分开始，到时间T为止(包括T) 的所有事件。T以分钟为单位，0 <= T <= 6000

第二行：五个整数，依次是 dragon 、ninja、iceman、lion、wolf 的初始生命值。它们都大于0小于等于200

第三行：五个整数，依次是 dragon 、ninja、iceman、lion、wolf 的攻击力。它们都大于0小于等于200

**输出**

对每组数据，先输出一行：

Case n:

如对第一组数据就输出 Case 1:

然后按恰当的顺序和格式输出到时间T为止发生的所有事件。每个事件都以事件发生的时间开头，时间格式是“时: 分”，“时”有三位，“分”有两位。

样例输入

```
1
20 1 10 400
20 20 30 10 20
5 5 5 5 5
```

样例输出

```
Case 1:
000:00 blue lion 1 born
Its loyalty is 10
000:10 blue lion 1 marched to city 1 with 10 elements and force 5
000:50 20 elements in red headquarter
000:50 10 elements in blue headquarter
000:55 blue lion 1 has 0 sword 1 bomb 0 arrow and 10 elements
001:05 blue lion 1 ran away
001:50 20 elements in red headquarter
001:50 10 elements in blue headquarter
002:50 20 elements in red headquarter
002:50 10 elements in blue headquarter
003:50 20 elements in red headquarter
003:50 10 elements in blue headquarter
004:50 20 elements in red headquarter
004:50 10 elements in blue headquarter
005:50 20 elements in red headquarter
005:50 10 elements in blue headquarter
```

提示

请注意浮点数精度误差问题。OJ上的编译器编译出来的可执行程序，在这方面和你电脑上执行的程序很可能会不一致。5 * 0.3 的结果，有的机器上可能是 15.00000001，去尾取整得到15,有的机器上可能是14.9999999，去尾取整后就变成14。因此,本题不要写 5 * 0.3，要写 5 * 3 / 10。

来源

Guo Wei



【张真铭 25元培】

> @🗿:当暴力成为主流，人类科研的希望将不复存在……

做了一下程设魔兽三，感觉就是暴力翻译，把人话翻译成代码（

主要就是练习oop里的继承多态，其实不太需要动脑子，还有就是这种复杂的程序对代码稳健性还是有要求的

再次吐槽cout的流输出，丑的批爆，oj快点用c++23吧，其实我早就是```std::print```和```std::ranges```的粉丝了，至于cout，我祝他好运。

码力耗尽，一段时间之内不会写代码了，歇逼。

```cpp
#include <algorithm>
#include <array>
#include <cstddef>
#include <cstdint>
#include <format>
#include <iostream>
#include <memory>
#include <print>
#include <ranges>
#include <string>
#include <string_view>
#include <utility>
#include <vector>

enum class WarriorType : std::uint8_t {
  DRAGON = 0,
  NINJA,
  ICEMAN,
  LION,
  WOLF,
  COUNT
};

constexpr int WARRIOR_COUNT = std::to_underlying(WarriorType::COUNT);

constexpr std::array<std::string_view, WARRIOR_COUNT> WARRIOR_NAMES = {
    "dragon", "ninja", "iceman", "lion", "wolf"};

constexpr std::array<WarriorType, 5> RED_ORDER = {
    WarriorType::ICEMAN, WarriorType::LION, WarriorType::WOLF,
    WarriorType::NINJA, WarriorType::DRAGON};

constexpr std::array<WarriorType, 5> BLUE_ORDER = {
    WarriorType::LION, WarriorType::DRAGON, WarriorType::NINJA,
    WarriorType::ICEMAN, WarriorType::WOLF};

enum class WeaponType : std::uint8_t { SWORD = 0, BOMB, ARROW, COUNT };

constexpr int WEAPON_COUNT = std::to_underlying(WeaponType::COUNT);

constexpr std::array<std::string_view, WEAPON_COUNT> WEAPON_NAMES = {
    "sword", "bomb", "arrow"};

struct Config {
  int id;
  int hp;
  int atk;
  int res_m;
  WarriorType type;
  std::string_view headquarter;
};

class Warrior {
public:
  explicit Warrior(const Config &cfg)
      : m_id(cfg.id), m_hp(cfg.hp), m_atk(cfg.atk),
        m_headquarter(cfg.headquarter), m_type(cfg.type) {}

  virtual ~Warrior() = default;

  void get_damage(int damage) {
    m_hp -= damage;
    if (m_hp < 0)
      m_hp = 0;
  }

  [[nodiscard]] auto get_id() const noexcept -> int { return m_id; }
  [[nodiscard]] auto get_hp() const noexcept -> int { return m_hp; }
  [[nodiscard]] auto get_atk() const noexcept -> int { return m_atk; }
  [[nodiscard]] auto get_type() const noexcept -> WarriorType { return m_type; }
  [[nodiscard]] auto get_headquarter_name() const noexcept -> std::string_view {
    return m_headquarter;
  }

  [[nodiscard]] auto get_weapons_state() const noexcept -> int {
    int state = 0;
    for (const auto &w : m_weapons)
      state += w.usage;
    return state;
  }

  struct WeaponInfo {
    WeaponType type;
    int usage;
    WeaponInfo(WeaponType t, int c) : type(t), usage(c) {}
  };
  std::vector<WeaponInfo> m_weapons;

  void before_fight() {
    std::ranges::sort(m_weapons, [](const WeaponInfo &a, const WeaponInfo &b) {
      if (a.type == b.type)
        return a.usage < b.usage;
      return std::to_underlying(a.type) < std::to_underlying(b.type);
    });
  }

  void cleanup_weapons() {
    std::erase_if(m_weapons, [](const WeaponInfo &w) { return w.usage <= 0; });
    m_iter = 0;
  }

  void loot(Warrior *obj) {
    if (!obj)
      return;
    int size = static_cast<std::uint8_t>(obj->m_weapons.size());
    int i = 0;
    for (; i < size && m_weapons.size() < m_max_weapons &&
           obj->m_weapons[i].type != WeaponType::ARROW;
         ++i) {
      m_weapons.emplace_back(obj->m_weapons[i]);
    }
    for (int j = size - 1; j >= i && m_weapons.size() < m_max_weapons &&
                           obj->m_weapons[j].type == WeaponType::ARROW;
         --j) {
      m_weapons.emplace_back(obj->m_weapons[j]);
    }
  }

  void report_weapons(std::string_view time) const noexcept {
    std::array<int, 3> counts{0, 0, 0};
    for (const auto &w : m_weapons) {
      if (w.usage > 0)
        ++counts[std::to_underlying(w.type)];
    }
    std::println("{} {} {} {} has {} sword {} bomb {} arrow and {} elements",
                 time, get_headquarter_name(),
                 WARRIOR_NAMES[std::to_underlying(get_type())], m_id, counts[0],
                 counts[1], counts[2], m_hp);
  }

  virtual void print_extra_info() const noexcept = 0;

  virtual void attack(Warrior *obj) noexcept {
    if (!obj || m_weapons.empty() || m_hp == 0)
      return;

    int n = static_cast<std::uint8_t>(m_weapons.size());
    for (int i : std::views::iota(0, n)) {
      auto &weapon = m_weapons[m_iter];

      if (weapon.usage > 0) {
        int damage = weapon_damage(weapon.type);
        obj->get_damage(damage);

        if (weapon.type == WeaponType::BOMB) {
          if (m_type != WarriorType::NINJA) {
            m_hp -= (damage / 2);
            if (m_hp < 0)
              m_hp = 0;
          }
          weapon.usage = 0;
        } else if (weapon.type == WeaponType::ARROW) {
          --weapon.usage;
        }

        m_iter = (m_iter + 1) % n;
        return;
      }
      m_iter = (m_iter + 1) % n;
    }
  }

  void reset_iter() { m_iter = 0; }
  virtual void yell(std::string_view time, int pos) const noexcept {}

protected:
  int m_id;
  int m_hp;
  int m_atk;
  WarriorType m_type;
  const int m_max_weapons = 10;
  std::string_view m_headquarter;
  int m_iter{0};

  [[nodiscard]] auto weapon_damage(WeaponType type) const noexcept -> int {
    switch (type) {
    case WeaponType::ARROW:
      return m_atk * 3 / 10;
    case WeaponType::BOMB:
      return m_atk * 4 / 10;
    case WeaponType::SWORD:
      return m_atk * 2 / 10;
    default:
      return 0;
    }
  }
};

class Dragon : public Warrior {
public:
  explicit Dragon(const Config &cfg) : Warrior(cfg) {
    m_weapons.emplace_back(
        static_cast<WeaponType>(cfg.id % 3),
        static_cast<WeaponType>(cfg.id % 3) == WeaponType::ARROW ? 2 : 1);
  }
  void yell(std::string_view time, int pos) const noexcept override {
    std::println("{} {} dragon {} yelled in city {}", time,
                 get_headquarter_name(), get_id(), pos);
  }
  void print_extra_info() const noexcept override {}
};

class Ninja : public Warrior {
public:
  explicit Ninja(const Config &cfg) : Warrior(cfg) {
    m_weapons.emplace_back(
        static_cast<WeaponType>(cfg.id % 3),
        static_cast<WeaponType>(cfg.id % 3) == WeaponType::ARROW ? 2 : 1);
    m_weapons.emplace_back(
        static_cast<WeaponType>((cfg.id + 1) % 3),
        static_cast<WeaponType>((cfg.id + 1) % 3) == WeaponType::ARROW ? 2 : 1);
  }
  void print_extra_info() const noexcept override {}
};

class Iceman : public Warrior {
public:
  explicit Iceman(const Config &cfg) : Warrior(cfg) {
    m_weapons.emplace_back(
        static_cast<WeaponType>(cfg.id % 3),
        static_cast<WeaponType>(cfg.id % 3) == WeaponType::ARROW ? 2 : 1);
  }

  void move_take_blood() { m_hp -= m_hp / 10; }
  void print_extra_info() const noexcept override {}
};

int K;
class Lion : public Warrior {
public:
  explicit Lion(const Config &cfg) : Warrior(cfg) {
    m_loyalty = cfg.res_m;
    m_weapons.emplace_back(
        static_cast<WeaponType>(cfg.id % 3),
        static_cast<WeaponType>(cfg.id % 3) == WeaponType::ARROW ? 2 : 1);
  }
  [[nodiscard]] auto is_loyal() const noexcept -> bool { return m_loyalty > 0; }
  void down_loyalty() { m_loyalty -= m_K; }
  void print_extra_info() const noexcept override {
    std::println("Its loyalty is {}", m_loyalty);
  }

private:
  int m_loyalty;
  const int m_K = K;
};

class Wolf : public Warrior {
public:
  using Warrior::Warrior;

  void snatch(Warrior *obj, int city_pos, std::string_view time) {
    if (!obj)
      return;
    before_fight();
    obj->before_fight();

    if (!obj->m_weapons.empty() && m_weapons.size() < m_max_weapons) {
      int snatch_num = 0;
      auto obj_type = obj->m_weapons.front().type;

      if (obj_type == WeaponType::ARROW) {
        for (int i = static_cast<std::uint8_t>(obj->m_weapons.size() - 1);
             i >= 0 && m_weapons.size() < m_max_weapons; --i) {
          m_weapons.emplace_back(obj->m_weapons[i]);
          obj->m_weapons.erase(obj->m_weapons.begin() + i);
          ++snatch_num;
        }
      } else {
        while (!obj->m_weapons.empty() &&
               obj->m_weapons.front().type == obj_type &&
               m_weapons.size() < m_max_weapons) {
          m_weapons.emplace_back(obj->m_weapons.front());
          obj->m_weapons.erase(obj->m_weapons.begin());
          ++snatch_num;
        }
      }

      if (snatch_num > 0) {
        std::println("{} {} wolf {} took {} {} from {} {} {} in city {}", time,
                     m_headquarter, m_id, snatch_num,
                     WEAPON_NAMES[std::to_underlying(obj_type)],
                     obj->get_headquarter_name(),
                     WARRIOR_NAMES[std::to_underlying(obj->get_type())],
                     obj->get_id(), city_pos);
      }
    }
  }
  void print_extra_info() const noexcept override {}
};

class Headquarter {
public:
  explicit Headquarter(const std::array<int, WARRIOR_COUNT> &atk, int initial_m,
                       const std::array<int, WARRIOR_COUNT> &hp_costs, int N)
      : m_atk(atk), m_total_m(initial_m), m_costs(hp_costs), m_N(N) {}

  virtual ~Headquarter() = default;

  [[nodiscard]] virtual auto get_name() const noexcept -> std::string_view = 0;
  [[nodiscard]] virtual auto get_order() const noexcept
      -> const std::array<WarriorType, 5> & = 0;

  void report_elements(std::string_view time) const {
    std::println("{} {} elements in {} headquarter", time, m_total_m,
                 get_name());
  }

  [[nodiscard]] auto step(std::string_view time) noexcept
      -> std::unique_ptr<Warrior> {
    if (m_stopped)
      return nullptr;

    const auto &order = get_order();
    WarriorType type = order[m_iter];
    int cost = m_costs[std::to_underlying(type)];

    if (m_total_m >= cost) {
      m_total_m -= cost;
      ++m_counts[std::to_underlying(type)];
      int id = ++m_total_count;
      int atk = m_atk[std::to_underlying(type)];

      auto warrior = create_warrior(id, type, cost, atk);
      log_production(time, type);
      warrior->print_extra_info();

      m_iter = (m_iter + 1) % 5;
      return warrior;
    }

    m_stopped = true;
    return nullptr;
  }

  [[nodiscard]] auto is_stopped() const noexcept -> bool { return m_stopped; }

protected:
  int m_total_m;
  int m_N;
  const std::array<int, WARRIOR_COUNT> &m_costs;
  const std::array<int, WARRIOR_COUNT> &m_atk;
  std::array<int, WARRIOR_COUNT> m_counts{0};
  int m_total_count{0};
  int m_iter{0};
  bool m_stopped{false};

private:
  void log_production(std::string_view time, WarriorType type) const {
    std::println("{} {} {} {} born", time, get_name(),
                 WARRIOR_NAMES[std::to_underlying(type)], m_total_count);
  }

  [[nodiscard]] auto create_warrior(int id, WarriorType type, int cost,
                                    const int atk) const noexcept
      -> std::unique_ptr<Warrior> {
    Config cfg = {.id = id,
                  .hp = cost,
                  .atk = atk,
                  .res_m = m_total_m,
                  .type = type,
                  .headquarter = get_name()};
    switch (type) {
    case WarriorType::DRAGON:
      return std::make_unique<Dragon>(cfg);
    case WarriorType::NINJA:
      return std::make_unique<Ninja>(cfg);
    case WarriorType::ICEMAN:
      return std::make_unique<Iceman>(cfg);
    case WarriorType::LION:
      return std::make_unique<Lion>(cfg);
    case WarriorType::WOLF:
      return std::make_unique<Wolf>(cfg);
    default:
      return nullptr;
    }
  }
};

class RedHeadquarter : public Headquarter {
public:
  using Headquarter::Headquarter;
  [[nodiscard]] auto get_name() const noexcept -> std::string_view override {
    return "red";
  }
  [[nodiscard]] auto get_order() const noexcept
      -> const std::array<WarriorType, 5> & override {
    return RED_ORDER;
  }
};

class BlueHeadquarter : public Headquarter {
public:
  using Headquarter::Headquarter;
  [[nodiscard]] auto get_name() const noexcept -> std::string_view override {
    return "blue";
  }
  [[nodiscard]] auto get_order() const noexcept
      -> const std::array<WarriorType, 5> & override {
    return BLUE_ORDER;
  }
};

class City {
public:
  explicit City(int i) : m_pos(i) {}

  [[nodiscard]] auto get_red() const noexcept -> Warrior * {
    return m_red_warrior.get();
  }
  [[nodiscard]] auto get_blue() const noexcept -> Warrior * {
    return m_blue_warrior.get();
  }
  [[nodiscard]] auto red_leaves() -> std::unique_ptr<Warrior> {
    return std::move(m_red_warrior);
  }
  [[nodiscard]] auto blue_leaves() -> std::unique_ptr<Warrior> {
    return std::move(m_blue_warrior);
  }

  void produce_red(std::unique_ptr<Warrior> w) { m_red_warrior = std::move(w); }
  void produce_blue(std::unique_ptr<Warrior> w) {
    m_blue_warrior = std::move(w);
  }
  void accept_incoming_red(std::unique_ptr<Warrior> w) {
    m_incoming_red = std::move(w);
  }
  void accept_incoming_blue(std::unique_ptr<Warrior> w) {
    m_incoming_blue = std::move(w);
  }

  [[nodiscard]] auto is_taken() const noexcept -> bool {
    return m_enemy_count >= 1;
  }

  void check_lion(std::string_view time, int N) {
    if (m_red_warrior && m_red_warrior->get_type() == WarriorType::LION &&
        m_pos < N + 1) {
      auto *lion = static_cast<Lion *>(m_red_warrior.get());
      if (!lion->is_loyal()) {
        std::println("{} red lion {} ran away", time, lion->get_id());
        m_red_warrior = nullptr;
      }
    }
    if (m_blue_warrior && m_blue_warrior->get_type() == WarriorType::LION &&
        m_pos > 0) {
      auto *lion = static_cast<Lion *>(m_blue_warrior.get());
      if (!lion->is_loyal()) {
        std::println("{} blue lion {} ran away", time, lion->get_id());
        m_blue_warrior = nullptr;
      }
    }
  }

  void commit_arrivals(std::string_view time, int N) {
    if (m_incoming_red) {
      m_red_warrior = std::move(m_incoming_red);
      if (m_red_warrior->get_type() == WarriorType::ICEMAN)
        static_cast<Iceman *>(m_red_warrior.get())->move_take_blood();
      else if (m_red_warrior->get_type() == WarriorType::LION)
        static_cast<Lion *>(m_red_warrior.get())->down_loyalty();

      std::print("{} red {} {} ", time,
                 WARRIOR_NAMES[std::to_underlying(m_red_warrior->get_type())],
                 m_red_warrior->get_id());

      if (m_pos == N + 1) {
        std::println("reached blue headquarter with {} elements and force {}",
                     m_red_warrior->get_hp(), m_red_warrior->get_atk());
        ++m_enemy_count;
        if (is_taken())
          std::println("{} blue headquarter was taken", time);
      } else {
        std::println("marched to city {} with {} elements and force {}", m_pos,
                     m_red_warrior->get_hp(), m_red_warrior->get_atk());
      }
    }

    if (m_incoming_blue) {
      m_blue_warrior = std::move(m_incoming_blue);
      if (m_blue_warrior->get_type() == WarriorType::ICEMAN)
        static_cast<Iceman *>(m_blue_warrior.get())->move_take_blood();
      else if (m_blue_warrior->get_type() == WarriorType::LION)
        static_cast<Lion *>(m_blue_warrior.get())->down_loyalty();

      std::print("{} blue {} {} ", time,
                 WARRIOR_NAMES[std::to_underlying(m_blue_warrior->get_type())],
                 m_blue_warrior->get_id());

      if (m_pos == 0) {
        std::println("reached red headquarter with {} elements and force {}",
                     m_blue_warrior->get_hp(), m_blue_warrior->get_atk());
        ++m_enemy_count;
        if (is_taken())
          std::println("{} red headquarter was taken", time);
      } else {
        std::println("marched to city {} with {} elements and force {}", m_pos,
                     m_blue_warrior->get_hp(), m_blue_warrior->get_atk());
      }
    }
  }

  void wolf_snatch(std::string_view time) {
    if (!m_red_warrior || !m_blue_warrior)
      return;
    bool red_is_wolf = (m_red_warrior->get_type() == WarriorType::WOLF);
    bool blue_is_wolf = (m_blue_warrior->get_type() == WarriorType::WOLF);

    if (red_is_wolf && !blue_is_wolf)
      static_cast<Wolf *>(m_red_warrior.get())
          ->snatch(m_blue_warrior.get(), m_pos, time);
    else if (!red_is_wolf && blue_is_wolf)
      static_cast<Wolf *>(m_blue_warrior.get())
          ->snatch(m_red_warrior.get(), m_pos, time);
  }

  void fight(std::string_view time) {
    if (!m_red_warrior || !m_blue_warrior)
      return;
    bool both_no_weapons =
        m_red_warrior->m_weapons.empty() && m_blue_warrior->m_weapons.empty();

    if (!both_no_weapons) {
      m_red_warrior->before_fight();
      m_blue_warrior->before_fight();
      m_red_warrior->reset_iter();
      m_blue_warrior->reset_iter();

      Warrior *first =
          (m_pos % 2 == 1) ? m_red_warrior.get() : m_blue_warrior.get();
      Warrior *second =
          (m_pos % 2 == 1) ? m_blue_warrior.get() : m_red_warrior.get();

      int unchanged_rounds = 0;

      while (true) {
        int r_hp = m_red_warrior->get_hp(),
            r_ws = m_red_warrior->get_weapons_state();
        int b_hp = m_blue_warrior->get_hp(),
            b_ws = m_blue_warrior->get_weapons_state();

        first->attack(second);
        if (first->get_hp() <= 0 || second->get_hp() <= 0)
          break;

        second->attack(first);
        if (first->get_hp() <= 0 || second->get_hp() <= 0)
          break;

        if (r_hp == m_red_warrior->get_hp() &&
            r_ws == m_red_warrior->get_weapons_state() &&
            b_hp == m_blue_warrior->get_hp() &&
            b_ws == m_blue_warrior->get_weapons_state()) {
          unchanged_rounds++;
        } else {
          unchanged_rounds = 0;
        }

        if (unchanged_rounds >= 20)
          break;
      }
    }

    handle_result_and_logs(time);
  }

  void report_warrior_status(std::string_view time) const {
    if (m_red_warrior)
      m_red_warrior->report_weapons(time);
    if (m_blue_warrior)
      m_blue_warrior->report_weapons(time);
  }

private:
  int m_pos;
  int m_enemy_count{0};
  std::unique_ptr<Warrior> m_red_warrior;
  std::unique_ptr<Warrior> m_blue_warrior;
  std::unique_ptr<Warrior> m_incoming_red;
  std::unique_ptr<Warrior> m_incoming_blue;

  void print_both_died_log(std::string_view time) const noexcept {
    std::println("{} both red {} {} and blue {} {} died in city {}", time,
                 WARRIOR_NAMES[std::to_underlying(m_red_warrior->get_type())],
                 m_red_warrior->get_id(),
                 WARRIOR_NAMES[std::to_underlying(m_blue_warrior->get_type())],
                 m_blue_warrior->get_id(), m_pos);
  }

  void print_alive_log(std::string_view time) const noexcept {
    std::println("{} both red {} {} and blue {} {} were alive in city {}", time,
                 WARRIOR_NAMES[std::to_underlying(m_red_warrior->get_type())],
                 m_red_warrior->get_id(),
                 WARRIOR_NAMES[std::to_underlying(m_blue_warrior->get_type())],
                 m_blue_warrior->get_id(), m_pos);
  }

  void handle_result_and_logs(std::string_view time) noexcept {
    bool red_dead = (m_red_warrior->get_hp() <= 0);
    bool blue_dead = (m_blue_warrior->get_hp() <= 0);

    if (red_dead && blue_dead) {
      print_both_died_log(time);
      m_red_warrior = nullptr;
      m_blue_warrior = nullptr;
    } else if (red_dead) {
      m_red_warrior->cleanup_weapons();
      m_blue_warrior->cleanup_weapons();
      m_blue_warrior->loot(m_red_warrior.get());
      std::println(
          "{} blue {} {} killed red {} {} in city {} remaining {} elements",
          time, WARRIOR_NAMES[std::to_underlying(m_blue_warrior->get_type())],
          m_blue_warrior->get_id(),
          WARRIOR_NAMES[std::to_underlying(m_red_warrior->get_type())],
          m_red_warrior->get_id(), m_pos, m_blue_warrior->get_hp());
      m_red_warrior = nullptr;
      if (m_blue_warrior->get_type() == WarriorType::DRAGON)
        m_blue_warrior->yell(time, m_pos);
    } else if (blue_dead) {
      m_blue_warrior->cleanup_weapons();
      m_red_warrior->cleanup_weapons();
      m_red_warrior->loot(m_blue_warrior.get());
      std::println(
          "{} red {} {} killed blue {} {} in city {} remaining {} elements",
          time, WARRIOR_NAMES[std::to_underlying(m_red_warrior->get_type())],
          m_red_warrior->get_id(),
          WARRIOR_NAMES[std::to_underlying(m_blue_warrior->get_type())],
          m_blue_warrior->get_id(), m_pos, m_red_warrior->get_hp());
      m_blue_warrior = nullptr;
      if (m_red_warrior->get_type() == WarriorType::DRAGON)
        m_red_warrior->yell(time, m_pos);
    } else {
      m_red_warrior->cleanup_weapons();
      m_blue_warrior->cleanup_weapons();
      print_alive_log(time);
      if (m_red_warrior->get_type() == WarriorType::DRAGON)
        m_red_warrior->yell(time, m_pos);
      if (m_blue_warrior->get_type() == WarriorType::DRAGON)
        m_blue_warrior->yell(time, m_pos);
    }
  }
};

auto main() -> int {
  std::cin.tie(nullptr)->sync_with_stdio(false);

  int t;
  if (!(std::cin >> t))
    return 0;

  for (int caseIdx : std::views::iota(1, t + 1)) {
    int M, N, T;
    std::cin >> M >> N >> K >> T;
    std::array<int, WARRIOR_COUNT> warrior_HP;
    for (int &hp : warrior_HP)
      std::cin >> hp;
    std::array<int, WARRIOR_COUNT> warrior_ATK;
    for (int &atk : warrior_ATK)
      std::cin >> atk;

    std::println("Case {}:", caseIdx);

    std::array<std::unique_ptr<Headquarter>, 2> bases = {
        std::make_unique<RedHeadquarter>(warrior_ATK, M, warrior_HP, N),
        std::make_unique<BlueHeadquarter>(warrior_ATK, M, warrior_HP, N)};

    std::vector<City> cities;
    cities.reserve(N + 2);
    for (int i : std::views::iota(0, N + 2))
      cities.emplace_back(i);

    int hour = 0;
    bool game_over = false;

    while (true) {
      if (hour * 60 > T || game_over)
        break;

      std::string time_00 = std::format("{:03}:00", hour);
      cities[0].produce_red(bases[0]->step(time_00));
      cities[N + 1].produce_blue(bases[1]->step(time_00));

      if (hour * 60 + 5 > T)
        break;
      std::string time_05 = std::format("{:03}:05", hour);
      for (int i : std::views::iota(0, N + 2))
        cities[i].check_lion(time_05, N);

      if (hour * 60 + 10 > T)
        break;
      std::string time_10 = std::format("{:03}:10", hour);

      for (int i : std::views::iota(0, N + 2)) {
        if (cities[i].get_red() && i < N + 1)
          cities[i + 1].accept_incoming_red(cities[i].red_leaves());
        if (cities[i].get_blue() && i > 0)
          cities[i - 1].accept_incoming_blue(cities[i].blue_leaves());
      }

      for (int i : std::views::iota(0, N + 2)) {
        cities[i].commit_arrivals(time_10, N);
        if (cities[i].is_taken())
          game_over = true;
      }
      if (game_over)
        break;

      if (hour * 60 + 35 > T)
        break;
      std::string time_35 = std::format("{:03}:35", hour);
      for (int i : std::views::iota(1, N + 1))
        cities[i].wolf_snatch(time_35);

      if (hour * 60 + 40 > T)
        break;
      std::string time_40 = std::format("{:03}:40", hour);
      for (int i : std::views::iota(1, N + 1))
        cities[i].fight(time_40);

      if (hour * 60 + 50 > T)
        break;
      std::string time_50 = std::format("{:03}:50", hour);
      bases[0]->report_elements(time_50);
      bases[1]->report_elements(time_50);

      if (hour * 60 + 55 > T)
        break;
      std::string time_55 = std::format("{:03}:55", hour);
      for (int i : std::views::iota(0, N + 2))
        cities[i].report_warrior_status(time_55);

      ++hour;
    }
  }
  return 0;
}
```





## T20052: 最大点数（同2048规则）

dfs, matrices, http://cs101.openjudge.cn/pctbook/T20052/

【黄浩展 25工学院】思路：先写最简单的左移操作，右移可直接翻转，上移对每列转化为数组进行左移操作，下移为上移翻转，之后递归搜索并更新最大值

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

void mergeleft(vector<int>& line) {
	vector<int>nxt, tmp;
	for (int n : line)
		if (n != 0)
			nxt.push_back(n);
	line = vector<int>(line.size(), 0);
	for (int i = 0; i < nxt.size();) {
		if (i + 1 < nxt.size() && nxt[i] == nxt[i + 1]) {
			tmp.push_back(2 * nxt[i]);
			i += 2;
		}
		else {
			tmp.push_back(nxt[i]);
			i++;
		}
	}
	for(int i=0;i<tmp.size();i++)
		line[i] = tmp[i];
}

void mergeright(vector<int>& line) {
	reverse(line.begin(), line.end());
	mergeleft(line);
	reverse(line.begin(), line.end());
}

void ml(vector <vector<int>>& grid) {
	for (auto &r : grid)
		mergeleft(r);
}

void mr(vector<vector<int>>& grid) {
	for (auto &r : grid)
		mergeright(r);
}

void mu(vector<vector<int>>& grid) {
	for (int i = 0; i < grid[0].size(); i++) {
		vector<int>tmp;
		for (int j = 0; j < grid.size(); j++)
			tmp.push_back(grid[j][i]);
		mergeleft(tmp);
		for (int k = 0; k < grid.size(); k++)
			grid[k][i] = (k<tmp.size()?tmp[k]:0);
	}
}

void md(vector<vector<int>>& grid) {
	reverse(grid.begin(), grid.end());
	mu(grid);
	reverse(grid.begin(), grid.end());
}

int findmax(vector<vector<int>>& grid) {
	int res = 0, m = grid.size(), n = grid[0].size();
	for (int i = 0; i < m; i++)
		for (int j = 0; j < n; j++)
			res = max(res, grid[i][j]);
	return res;
}

void dfs(vector<vector<int>>& grid, int step, int& ans, int p) {
	ans = max(ans, findmax(grid));
	if (step == p) return;
	vector<vector<int>>tl = grid, tr = grid, tu = grid, td = grid;
	ml(tl);
	if(tl!= grid)
		dfs(tl, step + 1, ans, p);
	mr(tr);
	if (tr!= grid)
		dfs(tr, step + 1, ans, p);
	mu(tu);
	if (tu!= grid)
		dfs(tu, step + 1, ans, p);
	md(td);
	if (td!= grid)
		dfs(td, step + 1, ans, p);
}

int main() {
	int m, n, p; 
	cin >> m >> n >> p;
	vector<vector<int>>grid(m, vector<int>(n));
	for (int i = 0; i < m; i++)
		for (int j = 0; j < n; j++)
			cin >> grid[i][j];
	int ans = 0;
	dfs(grid, 0, ans, p);
	cout << ans << endl;
	return 0;
}
```



【江昊中 25数院】思路：一开始觉得题里给的left函数不够优雅, 于是自己重写了一个, 并写了一个统一的滑动接口. 提交后WA, 以为是dfs出错了, 调了二十多分钟才意识到自己的left的移动算法写错了

```cpp
#include <bits/stdc++.h>
using namespace std;

using Board = vector<vector<int>>;

// 左右反转矩阵
void reverseRow(Board& board) {
    for (auto& row : board) {
        reverse(row.begin(), row.end());
    }
}

// 转置矩阵
void transpose(Board& board) {
    int n = board.size();
    int m = board[0].size();
    Board tmp(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            tmp[i][j] = board[j][i];
        }
    }
    board = move(tmp);
}

bool left(Board& board) {
    bool changed = false;
    int n = board.size();
    int m = board[0].size();
    for (auto& row : board) {
        // 使用快慢指针将非零元素移动到左侧
        int blank_idx = 0;
        for (int j = 0; j < m; j++) {
            if (row[j]) {
                if (blank_idx != j) {
                    row[blank_idx] = row[j];
                    row[j] = 0;
                    changed = true;
                }
                blank_idx++;
            }
        }

        for (int j = 0; j < m - 1; j++) {
            if (row[j] && row[j + 1] == row[j]) {
                row[j] <<= 1;
                row[j + 1] = 0;
                changed = true;
            }
        }

        blank_idx = 0;
        for (int j = 0; j < m; j++) {
            if (row[j]) {
                if (blank_idx != j) {
                    row[blank_idx] = row[j];
                    row[j] = 0;
                    changed = true;
                }
                blank_idx++;
            }
        }
    }
    return changed;
}

bool right(Board& board) {
    reverseRow(board);
    bool changed = left(board);
    reverseRow(board);
    return changed;
}

bool up(Board& board) {
    transpose(board);
    bool changed = left(board);
    transpose(board);
    return changed;
}

bool down(Board& board) {
    transpose(board);
    bool changed = right(board);
    transpose(board);
    return changed;
}

enum class Direction {
    LEFT,
    RIGHT,
    UP,
    DOWN
};

// 统一的滑动接口
bool slide(Board& board, Direction dir) {
    switch (dir) {
        case Direction::LEFT:
            return left(board);
        case Direction::RIGHT:
            return right(board);
        case Direction::UP:
            return up(board);
        case Direction::DOWN:
            return down(board);
        default:
            return false;
    }
}   

int const max_num(const Board& board) {
    int res = 0;
    for (const auto& row : board) {
        for (int num : row) {
            res = max(res, num);
        }
    }
    return res;
}

int global_max = 0;
// 深度优先搜索枚举所有可能的操作序列,并记录最大值
void dfs(Board& board, int p, int cur_step) {
    if (cur_step == p) {
        global_max = max(global_max, max_num(board));
        return;
    }

    Direction dirs[] = {Direction::LEFT, Direction::RIGHT, Direction::UP, Direction::DOWN};
    for (Direction dir : dirs) {
        Board tmp = board;
        if (slide(tmp, dir)) {
            dfs(tmp, p, cur_step + 1);
        } else {
            global_max = max(global_max, max_num(tmp));
        }
    }
}

int main() {
    int n, m, p;
    cin >> n >> m >> p;
    Board board(n, vector<int>(m));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cin >> board[i][j];
        }
    }

    dfs(board, p, 0);
    cout << global_max << endl;
    return 0;
}
```

> 用时60min



## T20576: printExp

http://cs101.openjudge.cn/practice/20576/



下面是 **< 60 行的超精简 C++ 实现**（不建 AST，完全复刻 Python 逻辑）

```cpp
#include <bits/stdc++.h>
using namespace std;

int pri(const string &op){return op=="not"?3:op=="and"?2:op=="or"?1:0;}
bool isop(const string&s){return s=="not"||s=="and"||s=="or";}

void apply(vector<pair<string,int>>&v, vector<string>&o){
    string op=o.back();o.pop_back();
    if(op=="not"){
        auto[a,pa]=v.back();v.pop_back();
        if(pa<pri(op)) a="( "+a+" )";
        v.push_back({"not "+a,pri(op)});return;
    }
    auto[b,pb]=v.back();v.pop_back();
    auto[a,pa]=v.back();v.pop_back();
    int p=pri(op);
    if(pa<p) a="( "+a+" )";
    if(pb<=p) b="( "+b+" )";
    v.push_back({a+" "+op+" "+b,p});
}

int main(){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    string s;getline(cin,s);
    vector<string> t;string cur;
    for(char c:s){
        if(isspace(c)){if(!cur.empty())t.push_back(cur),cur.clear();}
        else if(c=='('||c==')'){ if(!cur.empty())t.push_back(cur),cur.clear(); t.push_back(string(1,c)); }
        else cur+=c;
    }
    if(!cur.empty()) t.push_back(cur);

    vector<pair<string,int>> v; vector<string> o;
    for(auto&x:t){
        if(x=="(") o.push_back(x);
        else if(x==")"){
            while(o.back()!="(") apply(v,o);
            o.pop_back();
        }else if(isop(x)){
            while(!o.empty()&&isop(o.back())){
                string top=o.back();
                bool cond = (x!="not"? pri(top)>=pri(x): pri(top)>pri(x));
                if(!cond) break;
                apply(v,o);
            }
            o.push_back(x);
        }else v.push_back({x,4});
    }
    while(!o.empty()) apply(v,o);
    cout<<v.back().first<<"\n";
}
```



下面是 **加入详细注释、结构清晰、易读但仍保持简洁的 C++ 版本**。
逻辑与 Python Shunting Yard 版本完全一致，可直接 AC T20576。

> 注释非常详细，适合理解与维护。代码约 90 行（仍然不长）。

------

✅ **注释版（易读清晰版）**

```cpp
#include <bits/stdc++.h>
using namespace std;

/*
    运算符优先级：
        not > and > or
*/
int pri(const string &op) {
    if (op == "not") return 3;
    if (op == "and") return 2;
    if (op == "or")  return 1;
    return 0;
}

bool isop(const string &s) {
    return s == "not" || s == "and" || s == "or";
}

/*
    apply(): 弹出一个操作符，构造新的表达式字符串
    - vals:  存 (表达式字符串, 该表达式整体的优先级)
    - ops:   存操作符
    - 逻辑完全复刻 Python 版本
*/
void apply(vector<pair<string,int>> &vals, vector<string> &ops) {
    string op = ops.back();
    ops.pop_back();

    // ----- 单目操作符 not -----
    if (op == "not") {
        auto [a, pa] = vals.back();   // 右操作数
        vals.pop_back();

        // 若子表达式优先级 < not，则需要加括号
        if (pa < pri(op))
            a = "( " + a + " )";

        vals.push_back({"not " + a, pri(op)});
        return;
    }

    // ----- 二元操作符 and / or -----
    // 注意弹栈顺序：先右后左
    auto [b, pb] = vals.back(); vals.pop_back();
    auto [a, pa] = vals.back(); vals.pop_back();

    int p = pri(op);

    // 左侧优先级低 → 必须加括号
    if (pa < p)
        a = "( " + a + " )";

    // 右侧优先级 <= 当前 → 必须加括号
    if (pb <= p)
        b = "( " + b + " )";

    vals.push_back({a + " " + op + " " + b, p});
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    // ---- 读取整行表达式 ----
    string input;
    getline(cin, input);

    // ---- 分词 ----
    vector<string> tokens;
    string cur;

    for (char c : input) {
        if (isspace(c)) {
            if (!cur.empty()) tokens.push_back(cur), cur.clear();
        }
        else if (c == '(' || c == ')') {
            if (!cur.empty()) tokens.push_back(cur), cur.clear();
            tokens.push_back(string(1, c));
        }
        else {
            cur += c;
        }
    }
    if (!cur.empty()) tokens.push_back(cur);

    // 两个栈：
    // vals: (字符串, 优先级)
    // ops:  操作符
    vector<pair<string,int>> vals;
    vector<string> ops;

    // ---- 主循环：Shunting Yard ----
    for (auto &tk : tokens) {

        // 左括号直接入栈
        if (tk == "(") {
            ops.push_back(tk);
        }

        // 右括号：不断 apply 直到遇到 '('
        else if (tk == ")") {
            while (!ops.empty() && ops.back() != "(")
                apply(vals, ops);
            ops.pop_back(); // 弹掉 "("
        }

        // ------ 操作符 ------
        else if (isop(tk)) {

            // 根据优先级决定是否先 apply 栈顶操作符
            // 重点：not 是右结合 → 规则不同
            while (!ops.empty() && isop(ops.back())) {
                string top = ops.back();

                bool should_apply =
                    (tk != "not")
                        ? (pri(top) >= pri(tk))   // and/or：左结合
                        : (pri(top) >  pri(tk));  // not：右结合

                if (!should_apply) break;
                apply(vals, ops);
            }

            ops.push_back(tk);
        }

        // ------ 操作数：True / False ------
        else {
            // 常量优先级设为最高 4
            vals.push_back({tk, 4});
        }
    }

    // ---- 清空剩余操作符 ----
    while (!ops.empty())
        apply(vals, ops);

    // 最终表达式在 vals 栈顶
    cout << vals.back().first << "\n";
    return 0;
}
```

------

✅ 这个版本的优点

| 优点                     | 说明                          |
| ------------------------ | ----------------------------- |
| **非常清晰**             | 每一步都注释，容易理解        |
| **完全对应 Python 逻辑** | 左右 child 的括号规则完全一致 |
| **能 AC T20576**         | 处理所有情况                  |
| **处理 not 的右结合性**  | 完全正确                      |
| **没有 AST、只用两个栈** | 简单可靠                      |



## T22508: 最小奖金方案

topologic sort, http://cs101.openjudge.cn/practice/22508/

【姚博骞 25物院】思路：构建图，记录出度和入度的来源数组，这个学期也可以学习一下基本图论，以前没怎么搞过数学竞赛。
关键的转移方程：
`prize[beatenby[i][j]]=max(prize[beatenby[i][j]],prize[i]+1);`

```cpp
#include<iostream>
#include<queue>
#include<vector>
#include<unordered_map>
using namespace std;
int max(int a,int b)
{
    return (a>b)?a:b;
}
int main()
{
    //记录每个队伍打败的队伍数量，以及被打败的队伍的集合
    //考虑拓扑排序，肯定要一个也没打败的，直接把打败他的队伍奖金都变成max（now，ta+1），然后踢出去。
    int n,m;
    cin>>n>>m;
    vector<pair<int,int>>pk;
    vector<int> prize(n,100);
    for(int i=0;i<m;i++)
    {
        int a,b;
        cin>>a>>b;
        pk.push_back({a,b});
    }
    //构建图
    vector<int>num_beat(n,0);
    vector<vector<int>>beatenby(n,vector<int>(0));
    for(int i=0;i<m;i++)
    {
        num_beat[pk[i].first]++;
        beatenby[pk[i].second].push_back(pk[i].first);
    }
    queue<int>q;
    for(int i=0;i<n;i++)
    {
        if(!num_beat[i]) q.push(i);
    }
    while(!q.empty())
    {
        int i=q.front();
        q.pop();
        for(int j=0;j<beatenby[i].size();j++)
        {
            num_beat[beatenby[i][j]]--;
            prize[beatenby[i][j]]=max(prize[beatenby[i][j]],prize[i]+1);
            if(num_beat[beatenby[i][j]]==0) q.push(beatenby[i][j]);
        }
    }
    int ans=0;
    for(int i=0;i<n;i++)
    {
        ans+=prize[i];
    }
    cout<<ans;
    return 0;
}


```





## T25353: 排队

greedy, http://cs101.openjudge.cn/practice/25353



思路：

- 一个自然的想法是从前到后逐个确定当前位置可以填入的身高最小的同学。
- 如果现在一个同学 $i$ 想要前移到当前位置，则 $\not\exists j < i, \text{s.t. } |h_i - h_j| > D$。
- 因此可以发现：当且仅当 $i$ 前面“卡住它”的 $j$ 都已经被移到最前面的一些位置并固定下来，$i$ 才能前移到当前位置。
- 算法一：确定每一个位置时，暴力枚举待确定位置的同学，找到能前移且身高最小者即可。时间复杂度为 $O(n^2)$。
- 算法二：注意到这是一个图论模型，考虑一个 $n$ 个点的图，对初始序列中满足 $j < i \land |h_i - h_j| > D$ 的 $(i, j)$，连**有向边** $j \to i$，维护**优先队列**拓扑排序即可。时间复杂度为 $O(n^2)$。
- 算法三：注意到每个连向 $i$ 的 $j$ 满足 $j < i, h_j < h_i - D$ 或 $j < i, h_j > h_i + D$，AI 说这个可以“线段树优化建图”，点数和边数都将变为 $O(n \log n)$。对原图上的点用优先队列维护、对“优化建图”中新建的点用普通队列维护即可。时间复杂度为 $O(n \log n)$。
- 算法四：考虑不要把“图”建出来。注意到这张图是“分层”的，即我们可以把所有同学分成若干层，使得将层内排序结果拼起来就能得到答案。
- 这个结论看上去似乎比较“直观”，比如样例中 $1, 2, 4$ 和 $3, 5$ 就是两层，层内可以任意交换；但总让人有点不安，下面我们来证明一下。
- 在某一时刻，设待确定者中没有“被卡住”的同学编号为 $x_1 < x_2 < \cdots < x_k$，则 $(x_1, x_2), \cdots, (x_{k - 1}, x_k), (x_k, n]$ 这些区间中每个同学都至少被前面的一个同学卡住。
- (1) 对 $(x_k, n]$ 中的同学，它们显然不能在这些没有“被卡住”的同学都前移之前前移。
- (2) 而对于 $(x_1, x_k)$ 中的同学，考虑反证法，即对目前被卡住的同学 $t \in (x_i, x_{i + 1})$，当某些没有“被卡住”的同学 $x_j \ (j \leq i)$ 移到最前面并固定下来时，假设 $t$ 不再“被剩下的项卡住”，则可知 $|h_t - h_{x_j}| > d$，又由于 $|h_{x_{i + 1}} - h_{x_j}| \leq d, |h_{x_{i + 1}} - h_t| \leq d$，可得 $h_t > h_{x_{i + 1}} > h_{x_j}$ 或 $h_{x_j} > h_{x_{i + 1}} > h_t$。若为前者，则此时取 $t$ 不优；若为后者，则矛盾，因为取 $h_{x_j}$ 不优于 $h_{x_{i + 1}}$，即我们前移 $x_j$ 的操作不优。
- 故 (1)(2) 均不成立，可知上面的结论正确。
- 通过支持单点修改、前 / 后缀最大值的树状数组，即可从前到后依次求出每个同学所处的层。时间复杂度为 $O(n \log n)$。

代码（算法三）：

```cpp
#include <algorithm>
#include <queue>
#include <cstdio>

using namespace std;

struct Node {
	int ls;
	int rs;
};

struct Edge {
	int nxt;
	int end;
};

struct Candidate {
	int pos;

	Candidate(int _pos) : pos(_pos) {}
};

int n, id, root = 0, cnt = 0;
int h[1900001], lsh[100001], head[1900001], deg[1900001];
Node tree[1900001];
Edge edge[7100001];
queue<int> q;
priority_queue<Candidate> pq;

bool operator <(const Candidate a, const Candidate b){
	return h[a.pos] > h[b.pos];
}

void add_edge(int start, int end){
	cnt++;
	edge[cnt].nxt = head[start];
	head[start] = cnt;
	edge[cnt].end = end;
	deg[end]++;
}

int insert(int x, int l, int r, int val, int pos){
	int ans = ++id;
	tree[ans] = tree[x];
	if (x != 0) add_edge(x, ans);
	add_edge(pos, ans);
	if (l == r) return ans;
	int mid = (l + r) >> 1, &ls = tree[ans].ls, &rs = tree[ans].rs;
	if (val <= mid){
		ls = insert(ls, l, mid, val, pos);
	} else {
		rs = insert(rs, mid + 1, r, val, pos);
	}
	return ans;
}

void add_edges(int x, int L, int R, int l, int r, int pos){
	if (x == 0) return;
	if (l <= L && R <= r){
		add_edge(x, pos);
		return;
	}
	int mid = (L + R) >> 1;
	if (l <= mid) add_edges(tree[x].ls, L, mid, l, r, pos);
	if (r > mid) add_edges(tree[x].rs, mid + 1, R, l, r, pos);
}

void push(int x){
	if (x <= n){
		pq.push(Candidate(x));
	} else {
		q.push(x);
	}
}

bool empty(){
	return q.empty() && pq.empty();
}

int pop(){
	int ans;
	if (!q.empty()){
		ans = q.front();
		q.pop();
	} else {
		ans = pq.top().pos;
		pq.pop();
	}
	return ans;
}

int main(){
	int d, m;
	scanf("%d %d", &n, &d);
	for (int i = 1; i <= n; i++){
		scanf("%d", &h[i]);
		lsh[i] = h[i];
	}
	sort(lsh + 1, lsh + n + 1);
	m = unique(lsh + 1, lsh + n + 1) - lsh - 1;
	id = n;
	for (int i = 1; i <= n; i++){
		int r = upper_bound(lsh + 1, lsh + m + 1, h[i] - d - 1) - lsh - 1, l = lower_bound(lsh + 1, lsh + m + 1, h[i] + d + 1) - lsh;
		if (r >= 1) add_edges(root, 1, m, 1, r, i);
		if (l <= m) add_edges(root, 1, m, l, m, i);
		root = insert(root, 1, m, lower_bound(lsh + 1, lsh + m + 1, h[i]) - lsh, i);
	}
	for (int i = 1; i <= id; i++){
		if (deg[i] == 0) push(i);
	}
	while (!empty()){
		int cur = pop();
		if (cur <= n) printf("%d\n", h[cur]);
		for (int i = head[cur]; i != 0; i = edge[i].nxt){
			int x = edge[i].end;
			if (--deg[x] == 0) push(x);
		}
	}
	return 0;
}
```





思路：两个月前就尝试过一直不会做，现在还是不会做，学习了树状数组后靠ai写了一个出来。。。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <unordered_map>
#include <map>
using namespace std;

int lowbit(int x){
    return x&(-x);
}
class BIT {
private:
    vector<int> depth;
    int length;
public:
    BIT(int len) : length(len){
        depth.resize(len,-1);
    }
    void update(int id,int newvalue){
        while(id<=length){
            depth[id-1]=max(depth[id-1],newvalue);
            id+=lowbit(id);
        }
    }
    int findmax(int id){
        int f=-1;
        while(id>0){
            f=max(f,depth[id-1]);
            id-=lowbit(id);
        }
        return f;
    }
};
int main(){
    int n,d;
    cin>>n>>d;
    vector<int> heights(n,0);
    for(int i=0;i<n;i++){
        cin>>heights[i];
    }
    vector<int> sortheights=heights;
    sort(sortheights.begin(),sortheights.end());
    sortheights.erase(unique(sortheights.begin(),sortheights.end()),sortheights.end());
    int t=sortheights.size();
    unordered_map<int,int> mp;
    for(int i=0;i<t;i++){
        mp[sortheights[i]]=i;
    }
    BIT stree(t);
    BIT rtree(t);
    map<int,vector<int>> depclass;
    for(int height : heights){
        int sortid=upper_bound(sortheights.begin(),sortheights.end(),height-d-1)-sortheights.begin();
        int rsortid=t-(lower_bound(sortheights.begin(),sortheights.end(),height+d+1)-sortheights.begin());
        int max1=stree.findmax(sortid);
        int max2=rtree.findmax(rsortid);
        int de=max(max1,max2)+1;

        stree.update(mp[height]+1,de);
        rtree.update(t-mp[height],de);
        depclass[de].push_back(height);
    }
    for(auto &p:depclass){
        sort(p.second.begin(),p.second.end());
        for(int height : p.second){
            cout<<height<<'\n';
        }
    }
    return 0;
}
```



思路：用链表实现元素删除的O(1)实现就过了，本来用vector元素删除O(N)就过不了

```cpp
#include <bits/stdc++.h>

using namespace std;

struct lineup

{

    long long height;

    lineup *next;
};

int main()
{

    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int N, D;

    cin >> N >> D;

    vector<lineup> stu(N);

    for (int i = 0; i < N - 1; i++)
    {

        long long h;

        cin >> h;

        stu[i] = {h, &stu[i + 1]};
    }

    cin >> stu[N - 1].height;

    stu[N - 1].next = NULL;

    lineup *head = &stu[0];

    multiset<long long> part;

    vector<long long> ans;

    while (head->next != NULL)
    {

        lineup *it = head;

        lineup *previous = head;

        bool flag = 1;

        long long mmin = it->height, mmax = it->height;

        while (it != NULL)
        {

            mmin = min(mmin, it->height);

            mmax = max(mmax, it->height);

            if (abs(it->height - mmin) <= D && abs(it->height - mmax) <= D)
            {

                part.insert(it->height);

                previous->next = it->next;
            }

            else
            {

                if (flag)
                {
                    head = it;
                    flag = 0;
                }

                previous = it;
            }

            it = it->next;
        }

        while (!part.empty())
        {
            ans.push_back(*part.begin());
            part.erase(part.begin());
        }


    }

    //ans.push_back(head->height);

    for (int i = 0; i < N; i++) cout << ans[i] << '\n';
}

```





对于这道题目，线段树（或类似的二分查找树）思路实际上是解决这个问题的正解方向之一。这个问题的本质是求一个字典序最小的拓扑排序，而由于约束条件的特殊性（$|h_i - h_j| > D$ 时不能交换），这可以转化为一个分层问题：每一个数 $h_i$ 必须排在所有在该数之前出现、且与该数差值超过 $D$ 的数之后。

代码使用了动态开点的线段树思想（尽管是一次性建树），维护的是“值域”上的最大层数。

如果得到 WA（Wrong Answer）的主要原因很可能是 **整数溢出** 以及 **I/O 速度** 问题，还有 `getf` 函数中对于“完全包含在安全区”的节点处理不够显式（虽然逻辑上勉强通过，但为了稳健性最好加上）。

**1. 整数溢出问题 (Critical)**

题目中 $h_i$ 和 $D$ 均可达 $10^9$。
在代码中调用 `getf(h[i] - d, h[i] + d, root)` 时：
`h[i] + d` 的计算结果最大可达 $2 \times 10^9$。虽然 $2 \times 10^9$ 刚好在 `int` (约为 $2.147 \times 10^9$) 的范围内，但非常接近边界。如果测试数据稍微触碰边界，或者编译器对有符号整数溢出的处理，这都是极其危险的。
更重要的是，你的 `getf` 函数参数定义为 `const int&`。如果计算结果发生了溢出（变成负数），或者单纯因为类型转换问题，会导致 `ub` 变成一个很小的数，从而导致 `cur->l > ub` 误判为真，返回错误的层数。

**修改建议：** 将 `getf` 的参数改为 `long long`，并在调用时强制转换计算类型。

**2. 递归查询的逻辑隐患**

在 `getf` 函数中，你通过 `cur->r < lb` 和 `cur->l > ub` 来判断是否落在“阻挡区”。
如果一个节点的区间 `[l, r]` 完全落在 `[lb, ub]`（安全区，即可以交换的区域）内，你的代码通过不进入 `if` 分支最终返回 `ans = -1`。
这个逻辑是对的，但是为了清晰和防止边界错误，最好显式处理“无交集”或“被包含”的情况。

**3. I/O 性能**

$N=10^5$，且输出量大，使用 `cin/cout` 而不加 `ios::sync_with_stdio(0)` 极易导致 TLE（虽然你报的是 WA，但有时候评测机反馈不准确，或者因为超时截断导致 WA）。

 `long long` 的使用，增加了 Fast I/O。

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

struct Node {
    int f;          // 当前区间的最大批次
    int l, r;       // 当前结点覆盖的值域 [l, r]
    Node* l_ch;
    Node* r_ch;
    
    Node(int a, int b, int x = -1) : f(x), l(a), r(b), l_ch(nullptr), r_ch(nullptr) {}
};

// 建树逻辑不变，注意这里是对排序后的值建树
Node* buildTree(const vector<int>& v, int l, int r) {
    if (v[l] == v[r]) return new Node(v[l], v[r]); // 这里的区间是值域
    int m = l + (r - l) / 2;
    Node* cur = new Node(v[l], v[r]);
    cur->l_ch = buildTree(v, l, m);
    cur->r_ch = buildTree(v, m + 1, r);
    return cur;
}

// 查询范围 [lb, ub] 之外（即 (-inf, lb) U (ub, inf)）的最大 f 值
// 使用 long long 避免 lb/ub 溢出问题
int getf(long long lb, long long ub, Node* cur) {
    // 如果当前节点完全在安全区 [lb, ub] 内，它不产生阻挡，忽略
    if (cur->l >= lb && cur->r <= ub) return -1;
    
    // 如果当前节点完全在左侧阻挡区 (-inf, lb)
    if (cur->r < lb) return cur->f;
    // 如果当前节点完全在右侧阻挡区 (ub, inf)
    if (cur->l > ub) return cur->f;

    // 否则区间有重叠，需要递归查询
    int ans = -1;
    if (cur->l_ch) ans = max(ans, getf(lb, ub, cur->l_ch));
    if (cur->r_ch) ans = max(ans, getf(lb, ub, cur->r_ch));
    
    return ans;
}

// 更新值为 k 的节点的层数为 nf
void updatef(int k, int nf, Node* cur) {
    // 找到覆盖 k 的叶子节点（或者值域缩成一点的节点）
    if (cur->l == k && cur->r == k) {
        cur->f = max(cur->f, nf);
        return;
    }
    
    // 递归更新子节点
    // 由于可能有重复值，且树的划分是基于排序后的索引，相同的值可能跨越左右子树
    // 因此需要分别检查
    if (cur->l_ch && k <= cur->l_ch->r) updatef(k, nf, cur->l_ch);
    if (cur->r_ch && k >= cur->r_ch->l) updatef(k, nf, cur->r_ch);
    
    // 回溯更新当前节点
    int val = -1;
    if (cur->l_ch) val = max(val, cur->l_ch->f);
    if (cur->r_ch) val = max(val, cur->r_ch->f);
    cur->f = val;
}

int main() {
    // 开启 Fast I/O
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    long long d; // D 可能很大，配合加法运算使用 long long
    if (!(cin >> n >> d)) return 0;

    vector<int> h(n);
    for(int i = 0; i < n; i++) cin >> h[i];

    // 排序并建树
    vector<int> sorted_h(h);
    sort(sorted_h.begin(), sorted_h.end());
    
    // 构建线段树
    Node* root = buildTree(sorted_h, 0, n - 1);

    // 存储分层结果
    // fs[layer] 存储该层所有的身高
    vector<vector<int>> fs; 

    for(int i = 0; i < n; i++) {
        // 查询阻挡区：(-inf, h[i]-d) U (h[i]+d, inf)
        // 计算 h[i]-d 和 h[i]+d 时强制使用 long long
        long long lb = (long long)h[i] - d;
        long long ub = (long long)h[i] + d;
        
        int nf = getf(lb, ub, root) + 1;
        
        updatef(h[i], nf, root);

        if (fs.size() <= nf) {
            fs.resize(nf + 1);
        }
        fs[nf].push_back(h[i]);
    }

    // 输出
    for(auto& group : fs) {
        sort(group.begin(), group.end()); // 同一层内按身高从小到大排序（字典序最小）
        for(int val : group) {
            cout << val << "\n";
        }
    }

    return 0;
}
```



【潘彦璋 物理学院】思路：终于写到这里……我在这题上花了超久，首先是用的我在课后与同学初步讨论得到的拓扑排序解法，直接显式建图，记录每个点的所有儿子，入度，值，然后把所有入度为0的点丢到一个最小堆（我还为此学了一下堆如何自定义比较规则）blablabla……结果不出意料的爆了，而且还是先爆的内存，因为我把所有子结点指针直接存在结点里，但是其实只要存子结点的编号就够了
然后就是喜闻乐见的优化环节，首先这个拓扑排序的思路优化空间不说前途光明也是一点没有，于是只能求教AI和同学，于是收获了一个新思路：分层。
分层的主要思路是多次扫描数列h_i，每次找出所有入度为0的点，然后将他们一并删去，随后循环直到处理完所有数据。这个做法与每次只删去一个点相比利用了一个好的性质，那就是在任意时刻所有入度为0的点在最后的输出中必定是连续的。证明如下：
首先找出某一时刻数列中所有入度为0的点（编号为{a_1~a_n}，满足h_a_i单调递增），如果他们在最后的结果中不连续，那只能是在从小到大依次删除他们的过程中会产生新的入度为0的点，且其值小于h_a_n。假设这样的点a_k在删除a_i时产生，则有h_a_k大于h_a_i + D或h_a_k小于h_a_i - D。
1 若h_a_k大于h_a_i + D：由于h_a_n和h_a_k可以交换，故h_a_n不大于h_a_i + D，所以h_a_k不可能小于h_a_n，矛盾
2 若h_a_k小于h_a_i - D：则h_a_n和h_a_k的差必然大于D，因此a_n与a_k之间存在边，要么a_n入度不为零要么a_k入度不为零，总之矛盾
因此，问题就变成了将所有数据分批，而且一个点的输出批次只与其前面的输入数据有关，只要知道了输出的批次就可以得到结果。
又注意到某个点的输出批次等于它前面的与其值相差大于D的所有点的批次中的最大值+1（没有找到就是0），于是我们可以使用线段树维护每个区间点的批次最大值。
于是本人去学习了线段树的写法，然后又是指针显式建树（用数组应该也可以，但是我不太会，用指针更明了），最后终于是搞出来了，但是还是败在细节上了，递归访问的逻辑写错了……
总之，现在基本是会写线段树了，但是还得练习。
另外最后为了调试debug把注释基本全写上了，可以给同学参考了（

```cpp
#include<iostream>
#include<algorithm>
#include<vector>

using namespace std;

struct Node {
    int f, l, r; //f储存当前区间的最大批次，l和r则是当前区间的值域左右端
    Node* l_ch;
    Node* r_ch;
    Node(int a, int b, int x = -1) : f(x), l(a), r(b), l_ch(nullptr), r_ch(nullptr) {} //未处理的结点默认批次为-1，方便后续处理
};

Node* buildTree(vector<int>& v, int l, int r) {
    if(v[l] == v[r]) return (new Node(v[l], v[r])); //值相同的点可以合并储存
    int m = l + (r - l) / 2; //简单二分
    Node* cur = (new Node(v[l], v[r]));
    cur->l_ch = buildTree(v, l ,m);
    cur->r_ch = buildTree(v, m + 1, r); //树的建立过程保证了所有非叶子结点都有左右孩子
    return cur;
}

int getf(const int& lb, const int& ub, Node* cur) {
    if (cur->l >= lb && cur->r <= ub) return -1; //当前节点区间完全在[lb, ub]内
    if(cur->r < lb) return cur->f; //当前结点的区间完全在(-无穷, lb)内
    if(cur->l > ub) return cur->f; //当前结点的区间完全在(ub, +无穷)内
    //否则有重叠，需要进一步递归
    int ans = -1;
    if(cur->l_ch) ans = max(ans, getf(lb, ub, cur->l_ch)); //执行该语句时必定有cur->r >= lb，因此不是叶子结点
    if(cur->r_ch) ans = max(ans, getf(lb, ub, cur->r_ch)); //同上
    return ans;
}

void updatef(const int& k, const int& nf, Node* cur) {
    if(cur->l == k && cur->r == k) {
        cur->f = max(cur->f, nf); //找到，更新
        return;
    }
    if(k <= cur->l_ch->r) updatef(k, nf, cur->l_ch);
    if(k >= cur->r_ch->l) updatef(k, nf, cur->r_ch);
    cur->f = max(cur->l_ch->f, cur->r_ch->f);
    return;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n, d;
    cin >> n >> d;
    vector<int> h(n);
    for(int i = 0; i < n; i ++) cin >> h[i];
    vector<int> sorted_h(h.begin(), h.end());
    sort(sorted_h.begin(), sorted_h.end());
    Node* root = buildTree(sorted_h, 0, n - 1); //在排序后的h[i]上建树，减少内存需求
    vector<vector<int>> fs; //分批存储输出值
    for(int i = 0; i < n; i ++) {
        int nf = getf(h[i] - d, h[i] + d, root) + 1; //这就是方便的地方：-1对应的是要么前面的点都可以换要么是不能换的还在后面，批次显然都为0
        updatef(h[i], nf, root);
        if(fs.size() < nf + 1) fs.push_back({h[i]});
        else fs[nf].push_back(h[i]);
    }
    for(auto& p : fs){
        sort(p.begin(), p.end()); //同批次可自由交换
        for(auto& t : p) cout << t << endl;
    }
    return 0;
}
```



## T27351: 01最小生成树 

mst, http://cs101.openjudge.cn/practice/27351/

思路：优先选权值为 0 的边，再用权值为 1 的边补全连通性

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
#include <queue>
using namespace std;

const int MAX_N = 200005;
unordered_set<int> adj[MAX_N];  
unordered_set<int> unvisited; 
queue<int> q;             

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; ++i) {
        unvisited.insert(i);
    }
    for (int i = 0; i < m; ++i) {
        int a, b;
        cin >> a >> b;
        adj[a].insert(b);
        adj[b].insert(a);
    }
    int component_count = 0;
    for (int i = 1; i <= n; ++i) {
        if (unvisited.count(i)) { 
            component_count++;
            q.push(i);
            unvisited.erase(i); 
            while (!q.empty()) {
                int u = q.front();
                q.pop();
                vector<int> neighbors;
                for (auto it = unvisited.begin(); it != unvisited.end();) {
                    int v = *it;
                    if (adj[u].count(v) == 0) {
                        neighbors.push_back(v);
                        it = unvisited.erase(it);  
                    } else {
                        it++;
                    }
                }
                for (int v : neighbors) {
                    q.push(v);
                }
            }
        }
    }
    cout << component_count - 1 << endl;

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



## T27384: 候选人追踪

heap,lazy delete, http://cs101.openjudge.cn/practice/27384/

【姚博骞 25物院】思路：将在k个人里面和不在k个人里的人的投票数据分别加入两个堆，比较第一个堆最小和第一个堆最大。思路还行但执行起来非常难办对我而言，起码提交了20次没过。要注意的是投票时间间隔中票数都不变，故应当找开始满足的时刻和结束满足的时刻做差。
最后的bug出现在对最末尾的处理，要同时判断存在一个之前满足的时刻并且在这之后没有不满足的时刻才最后要用tmax-tlast。

懒删除的意思就是我不做队列中的删除但是做用数组记录，同时把正确的入队，如果出队的时候发现匹配不上就不管他。

```cpp
#include<iostream>
#include<vector>
#include<queue>
#include<set>
#include<algorithm>
#include<unordered_map>
using namespace std;
struct Compareda//return true 时a的优先级小于b
{
    bool operator()(pair<int,int> &a,pair<int,int> &b)
    {
        return a.second<b.second;
    }
};
struct Comparexiao//return true 时a的优先级小于b
{
    bool operator()(pair<int,int> &a,pair<int,int> &b)
    {
        return a.second>b.second;
    }
};
int main()
{
    int n,k;
    vector<pair<int,int>> vote;
    cin>>n>>k;
    for(int i=0;i<n;i++)
    {
        int t,c;
        cin>>t>>c;
        vote.push_back({t,c});
    }
    set<int> s;
    for(int i=0;i<k;i++)
    {
        int p;
        cin>>p;
        s.insert(p);
    }
    sort(vote.begin(),vote.end(),[&s](pair<int,int>&a,pair<int,int>&b)
    {
            return a.first<b.first;
    });
    vector<int> sum(314160,0);
    priority_queue<pair<int,int>,vector<pair<int,int>>,Comparexiao> kgeren;//第一个是序号，第二个是票数
    priority_queue<pair<int,int>,vector<pair<int,int>>,Compareda> qita;
    int ans=0;
    for(int i=1;i<314160;i++)
    {
        if(s.find(i)!=s.end())
            {
                kgeren.push({i,0});
            }
            else
            {
                qita.push({i,0});
            }
    }
    //只要我让k个的最小值比其它的最大值大就行。
    int i=0;
    int flag=0;
    int t_last=-1;
    while(i<n)
    {
        if(k==314159) break;
        while(i<n)
        {
            sum[vote[i].second]++;
            if(s.find(vote[i].second)!=s.end())
            {
                kgeren.push({vote[i].second,sum[vote[i].second]});
            }
            else
            {
                qita.push({vote[i].second,sum[vote[i].second]});
            }
            i++;
            if(i==n||vote[i].first!=vote[i-1].first)
            {
                break;
            }
        }
        while(kgeren.top().second!=sum[kgeren.top().first]||qita.top().second!=sum[qita.top().first])
        {
            if(!kgeren.empty()&&kgeren.top().second!=sum[kgeren.top().first])
            {
                kgeren.pop();
            }
            if(!qita.empty()&&qita.top().second!=sum[qita.top().first])
            {
                qita.pop();
            }
        }
        if(qita.top().second<kgeren.top().second)
        {
            if(flag==0) {t_last=vote[i-1].first;}
            flag=1;
        }   
        else if(flag==1)
        {
            flag=0;
            ans+=vote[i-1].first-t_last;
        }
    }
    if(flag==1&&t_last!=-1)
    {
        ans+=vote[i-1].first-t_last;
    }
    if(k==314159) 
    {cout<<vote[n-1].first;}
    else 
    {cout<<ans;}
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



## T30102: 完美交易窗口

monotonic stack, http://cs101.openjudge.cn/practice/T30102/

【江昊中 数学科学学院】思路：对于每个元素, 最大的左边界 `l` 是上一个大于等于它的元素的下一位, 所以维护一个递减的单调栈 `st` , 购入点是左边界 `l` 到当前元素的最右侧的最小值, 因此我还需维护一个严格单调递减的单调栈 `purchase` , 它保存的是从右往左看的第一个严格最小值. 为了让区间长度最大, 我们每次找购入点都只要找 `purchase` 里第一个大于等于左边界 `l` 的位置

```c++
#include<bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> h(n);
    for (int i = 0; i < n; i++) {
        cin >> h[i];
    }

    int max_len = 0;
    stack<int> st;
    vector<int> purchase;
    for (int i = 0; i < n; i++) {
        while (!st.empty() && h[i] > h[st.top()]) {
            st.pop();
        }
        
        int l = (st.empty()) ? 0 : st.top() + 1;
        for (int j = 0; j < purchase.size(); j++) {
            if (purchase[j] >= l) {
                max_len = max(max_len, i - purchase[j] + 1);
            }
        }
        
        while (!purchase.empty() && h[i] <= h[purchase.back()]) {
            purchase.pop_back();
        }
        purchase.push_back(i);

        st.push(i);
    }
    cout << max_len << endl;
    return 0;
}
```





【黄宇曦 地球与空间科学学院】思路：叽里咕噜说什么呢，线段树秒了。

首先考察到连续的一段肯定去思考用单调栈。假定我们通过单调栈得知了 $a_p$ 右侧第一个**小于等于** $a_p$ 的位置 $p'$，那么我们在这一段里面，以 $p$ 为左端点的最长区间肯定就是 $[p,p')$ 里面的所有最大值（若有多个）第一个出现的地方。考场上我想到这里就没想了于是首先敲了个 ST 表没过去。转念一想，$O(n\log n)$ 的内存确实会爆掉。所以转而敲一个线段树只用 $O(n)$ 的空间复杂度就过了。 

整个过程的时间复杂度是 $O(n\log n)$，瓶颈在于线段树的询问处理。

```cpp
#include <bits/stdc++.h>

using namespace std;

#define all(x) begin(x), end(x)
#define sz(x) (int) (x).size()

using i64 = long long;
using u64 = unsigned long long;
using i128 = __int128_t;
using u128 = __uint128_t;
using pii = pair<int, int>;
using vi = vector<int>;
using usi = unordered_set<int>;

const int MAXN = 1e6 + 5;

int n;

class SegTree {
    int n;
    vector<i64> s;
    vector<i64> pos;

    inline int lson(int x) { return x << 1; }
    inline int rson(int x) { return x << 1 | 1; }

    void push_up(int p) {
        s[p] = max(s[lson(p)], s[rson(p)]);
        pos[p] = s[lson(p)] >= s[rson(p)] ? pos[lson(p)] : pos[rson(p)];
    }
    void build(int l, int r, int p, const vector<i64> &a) {
        if (l == r) {
            s[p] = a[l];
            pos[p] = l;
            return;
        }
        int mid = l + r >> 1;
        build(l, mid, lson(p), a);
        build(mid + 1, r, rson(p), a);
        push_up(p);
    }
    pii query(int ql, int qr, int l, int r, int p) {
        if (ql <= l && r <= qr) {
            return {pos[p], s[p]};
        }
        int mid = l + r >> 1, ret = 0, val = 0;
        if (ql <= mid)
            tie(ret, val) = query(ql, qr, l, mid, lson(p));
        if (mid < qr) {
            auto [rr, vv] = query(ql, qr, mid + 1, r, rson(p));
            if (vv > val) {
                val = vv;
                ret = rr;
            }
        }
        return {ret, val};
    }

  public:
    SegTree(int n, const vector<i64> &a)
        : n(n), s(n + 2 << 2, 0), pos(n + 2 << 2, 0) {
        build(1, n, 1, a);
    }
    int query(int ql, int qr) { return query(ql, qr, 1, n, 1).first; }
};

int main() {
    cin >> n;
    vector<i64> a(n + 1);
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    SegTree st(n, a);
    stack<int> stk;
    int ans = 0;
    for (int i = 1; i <= n + 1; i++) {
        while (!stk.empty() && a[stk.top()] >= a[i]) {
            int l = stk.top();
            stk.pop();
            int r = st.query(l, i - 1);
            if (a[r] > a[l]) {
                ans = max(ans, r - l + 1);
            }
        }
        stk.push(i);
    }
    cout << ans << '\n';
}
```



【竺景琦、工学院】思路：单调栈。具体优化过程写在后面了。

```python
#include<bits/stdc++.h>
using namespace std;
#define ll long long
#define For(i,l,r) for(ll i=(l),i##_=(r);i<=i##_;++i)
#define Rep(i,l,r) for(ll i=(l),i##_=(r);i<i##_;++i)
#define FOR(i,l,r) for(ll i=(l),i##_=(r);i>=i##_;--i)

const ll N = 1e6+10;
ll a[N],d[N],m[N];
const ll inf = 2e18;
ll read(){
	char c=getchar();ll v=0;bool f=1;
	for(;'0'>c||c>'9';c=getchar())
	    if(c=='-') f = 0;
	for(;'0'<=c&&c<='9';c=getchar())
	    v = (v<<1)+(v<<3)+(c^48);
	return f?v:-v;
}
int main(){
	
	ll n=read();
	For(i,1,n) a[i]=read();
	
	ll dn = 0,now = 0,ans = 0;
	a[0] = inf;
	For(i,1,n){
		while(dn!=0&&a[d[dn]]<a[i]){
		    if(a[now]>a[m[dn]]) now = m[dn];
			--dn;
		}
		if(now!=0) ans = max(ans,i-now+1);
		if(a[now]>=a[i]) now = i;
		d[++dn] = i;m[dn] = now;
		now = 0;
	}
	
	printf("%lld",ans);
	return 0;
}
```



```cpp
#include <iostream>
#include <vector>
#include <algorithm>

auto main() -> int {
  std::cin.tie(nullptr)->sync_with_stdio(false);

  int n;
  std::cin >> n;
  std::vector<int> h(n);
  for (auto &v : h)
    std::cin >> v;

  std::vector<int> st_max;
  std::vector<int> st_min;

  int ans = 0;
  for (int j = 0; j < n; ++j) {
    while (!st_max.empty() && h[st_max.back()] < h[j])
      st_max.pop_back();

    int left_border = st_max.empty() ? -1 : st_max.back();

    while (!st_min.empty() && h[st_min.back()] >= h[j])
      st_min.pop_back();

    if (!st_min.empty()) {
      auto it = std::upper_bound(st_min.begin(), st_min.end(), left_border);
      if (it != st_min.end()) {
        int min_l = *it;
        ans = std::max(ans, j - min_l + 1);
      }
    }

    st_max.emplace_back(j);
    st_min.emplace_back(j);
  }

  std::cout << ans << '\n';
}
```





## T30201: 旅行售货商问题

bitmask dp, http://cs101.openjudge.cn/practice/30201/



思路：以前没接触过状压DP, 看懂课件上的做法后, 自己码了一遍, 嵌套层数有点多, 难点是理清思路 (下次记得还是不要随便命名变量了, 不然自己都看不懂)

```c++
#include <bits/stdc++.h>
using namespace std;

// Bitmask DP solution for the Traveling Salesman Problem (TSP)
int main() {
    int n;
    cin >> n;
    vector<vector<int>> grid(n, vector<int>(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid[i][j];
        }
    }

    int total = 1 << n;
    const int INF = 1e9;
    vector<vector<int>> dp(total, vector<int>(n, INF));
    dp[1][0] = 0;
    for (int mask = 1; mask < total; mask += 2) {
        for (int j = 0; j < n; j++) {
            if (dp[mask][j] != INF) {
                for (int u = 1; u < n; u++) {
                    if (((mask >> u) & 1) == 0) {
                        int nxt = mask | (1 << u);
                        dp[nxt][u] = min(dp[nxt][u], dp[mask][j] + grid[j][u]);
                    }
                }
            }
        }
    }

    int ans = INF;
    for (int i = 1; i < n; i++) {
        ans = min(ans, dp[total - 1][i] + grid[i][0]);
    }
    cout << ans << endl;
    return 0;
}
```

> 用时50min





```cpp
#include <iostream>
#include <vector>
using namespace std;

constexpr static int INF = 1e9;

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    int n;
    cin >> n;
    vector<vector<int>> G(n, vector<int>(n));
    for (auto &g : G)
        for (auto &x : g)
            cin >> x;

    int N = 1 << n;
    vector<vector<int>> dp(N, vector<int>(n + 1, INF));
    dp[1][0] = 0;

    for (int mask = 1; mask < N; ++mask)
        for (int u = 0; u < n; ++u)
        {
            if (!(mask & (1 << u)))
                continue;
            if (dp[mask][u] == INF)
                continue;
            for (int v = 0; v < n; ++v)
            {
                if ((mask & (1 << v)))
                    continue;
                dp[mask | (1 << v)][v] = min(dp[mask | (1 << v)][v], dp[mask][u] + G[u][v]);
            }
        }

    int ans = INF;
    for (int i = 1; i < n; ++i)
        ans = min(ans, dp[N - 1][i] + G[i][0]);
    cout << ans << '\n';
    return 0;
}
```

>共用时1h



思路：状压dp,自底向上写动态规划，动态规划的难点在于知道dp数组记录的是什么，这里记录在到达不同点的状态下（用二进制记录，即为状压），到达最后一个城市所用的最大值，直到把所有城市都遍历过，1<<k-1状态，再加上所有结束点回到起点，计算最大值。

ps：如果不用回到原点，可以这么写,dp数组的含义仍然不变，最后只要找dp[1<<k-1]中的最小值。

```cpp
for(int i = 0; i < n; i++)
    dp[1<<i][i] = 0;
```


代码：

```cpp
#include<iostream>
#include<vector>
using namespace std;
int min(int a,int b){
    return (a<b)?a:b;
}
int main()
{
    int n;
    cin>>n;
    vector<vector<int>> cost(n,vector<int>(n));
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            cin>>cost[i][j];
        }
    }
    int mask[1<<18];//状压dp：把每个城市去没去过的状态记录一下
    vector<vector<int>> dp(1<<18,vector<int>(n,1000000000));
    dp[1][0]=0;//一开始什么都不走的时候花费为0
    //由于最后的路线是一个圈，所以我们不妨假定就从下标为0的城市出发，上面的dp数组是（状态，最后在的城市）所花的最小值。
    for(int i=1;i<(1<<n);i+=2){
        for(int j=0;j<n;j++)//自底向上的dp写法。
        {
            int curr_dist=dp[i][j];
            if(dp[i][j]==1000000000){
                continue;
            }
            for(int k=0;k<n;k++){
                if((i>>k)&1){
                    continue;
                }
                int new_i=i|(1<<k);
                int new_cost=cost[j][k];
                dp[new_i][k]=min(dp[new_i][k],new_cost+dp[i][j]);
            }
        }   
    }
    int ans=1000000000;
    for(int i=1;i<n;i++){
        ans=min(ans,cost[0][i]+dp[(1<<n)-1][i]);
    }
    cout<<ans;
    return 0;
}

```



思路：即寻找有向图的最小哈密顿环．令 $f_{u,S}\ (u\in[n],\ S\in 2^{[n]\backslash\{ 1,u \}})$ 为自 $1$ 至 $u$、途径点集 $S$ 的最小路径长度，有 $f_{u,\varnothing}=w(1,u)$ 和 $f_{u,S}=\displaystyle\min_{v\in S}\{ f_{v,S\backslash\{ v \}} +w(v,u)\}\ (S\ne \varnothing)$，答案为 $f_{1,[n]\backslash\{ 1 \}}$．时间复杂度为 $O(2^{n}n^{2})$．

```cpp
#include <bits/stdc++.h>
using namespace std;

void tomin(auto& x, const auto& y) {
    if(x > y) x = y;
}
const int N = 18;
int G[N][N];
int f[1 << N][N];
int main() {
    int n;
    cin >> n;
    for(int i = 0; i < n; i++)
        for(int j = 0; j < n; j++) cin >> G[i][j];
    for(int u = 1; u < n; u++) f[0u][u] = G[0][u];
    for(unsigned S = 2u; S < (1u << n); S += 2u) {
        for(int u = 0; u < n; u++) {
            if(S & (1u << u)) continue;
            f[S][u] = numeric_limits<int>::max();
            for(int v = 0; v < n; v++)
                if(S & (1u << v))
                    tomin(f[S][u], f[S & ~(1u << v)][v] + G[v][u]);
        }
    }
    cout << f[(1u << n) - 2u][0];
    return 0;
}
```





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



```cpp
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

```cpp
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

```cpp
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

## E108.将有序数组转换为二叉搜索树

https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/

思路：二分查找，选中间元素为根节点，递归构建左右子树，25分钟

```cpp
class Solution {
private:
    TreeNode* buildBST(vector<int>& nums, int left, int right) {
        
        if (left > right) {
            return nullptr;
        }
        int mid = left + (right - left) / 2; 
        TreeNode* root = new TreeNode(nums[mid]);
        root->left = buildBST(nums, left, mid - 1);
        root->right = buildBST(nums, mid + 1, right);
        return root;
    }
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        if (nums.empty()) {
            return nullptr;
        }
        return buildBST(nums, 0, nums.size() - 1);
    }
};
```



## 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A

思路：遇到元音continue，其余情况变成小写然后输出.和该字母，用时较长（处理输出次数太多），但代码较短
，用时约15min（没注意到y也算元音）

```cpp
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

```cpp
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

```cpp
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



```cpp
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

```cpp
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



## 1520D. Same Differences

Data structures, hashing, math, 1200, https://codeforces.com/problemset/problem/1520/D

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;
    while (t--)
    {
        int n;
        cin >> n;
        unordered_map<int, long long> diff;
        for (int i = 1; i <= n; i++)
        {
            int a;
            cin >> a;
            diff[a - i]++;
        }

        long long ans = 0;
        for (auto i : diff)
            if (i.second >= 2)
                ans += (i.second * (i.second - 1) / 2);

        cout << ans << '\n';
    }
    return 0;
}
```





## 1868A. Fill in the Matrix

constructive algorithms, implementation, 1300, https://codeforces.com/problemset/problem/1868/A

```cpp
#include<bits/stdc++.h>
using namespace std;
int T,n,m,a;
int main(){
    scanf("%d",&T);
    while(T--){
        scanf("%d %d",&n,&m);
        if(m==1)
            printf("0\n");
        else
            printf("%d\n",min(n+1,m));
        for(int i=1;i<=n;i++){
            a=m-i;
            if(a<=0)
                a=m-1;
            for(int j=1;j<=m;j++){
                printf("%d ",a);
                a=(a+1)%m;
            }
            printf("\n");
        }
    }
    return 0;
}
```





## 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

```cpp
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





# 力扣简单



## E20.有效的括号

stack, https://leetcode.cn/problems/valid-parentheses/

思路：括号匹配问题 简单的一个栈数据结构即可

```cpp
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



思路：注意到括号的匹配与栈的后入先出是一样的，因此用栈的思路去解决，很顺利

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



## E94.二叉树的中序遍历

dfs, stack, https://leetcode.cn/problems/binary-tree-inorder-traversal/

思路：简单的 dfs

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        dfs(root, res);
        return res;
    }

    void dfs(TreeNode* root, vector<int>& res) {
        if (!root) return;
        dfs(root->left, res);
        res.push_back(root->val);
        dfs(root->right, res);
    }
};
```



## E108.将有序数组转换为二叉搜索树

https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/

思路：mid = (left + right) / 2 选中间元素作为根节点；

左子数组递归生成左子树；

右子数组递归生成右子树；

```cpp
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return build(nums, 0, nums.size() - 1);
    }

private:
    TreeNode* build(const vector<int>& nums, int left, int right) {
        if (left > right) return nullptr;  // 递归终止条件
        int mid = left + (right - left) / 2;  // 取中点
        TreeNode* root = new TreeNode(nums[mid]);
        root->left = build(nums, left, mid - 1);
        root->right = build(nums, mid + 1, right);
        return root;
    }
};
```



思路：将数组折半建树

```cpp
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return dfs(nums, 0, nums.size());
    }

    TreeNode* dfs(vector<int>& nums, int l, int r) {
        if (l >= r) return nullptr;
        int mid = (r - l) / 2 + l;
        TreeNode* left = dfs(nums, l, mid);
        TreeNode* right = dfs(nums, mid + 1, r);
        TreeNode* root = new TreeNode(nums[mid], left, right);
        return root;
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



## E160.相交链表

hash table, linked list, two pinters, https://leetcode.cn/problems/intersection-of-two-linked-lists/

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



```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode *> visited;
        ListNode *temp = headA;
        while (temp != nullptr) {
            visited.insert(temp);
            temp = temp->next;
        }
        temp = headB;
        while (temp != nullptr) {
            if (visited.count(temp)) {
                return temp;
            }
            temp = temp->next;
        }
        return nullptr;
    }
};
```





## E190.颠倒二进制位

  bit manipulation, https://leetcode.cn/problems/reverse-bits/

```cpp
class Solution {
public:
    int reverseBits(int n) {
        unsigned int ori = n, ans = 0;
        for (int i = 0; i < 32; i++) {
            ans = (ans << 1) | (ori & 1);
            ori >>= 1;
        }
        return static_cast<int>(ans);
    }
};
```



思路：简单的位运算

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int reverseBits(int n) {
        int ans = 0;
        for (int i = 0; i < 32; i++) {
            ans <<= 1;
            ans |= (n & 1);
            n >>= 1;
        }
        return ans;
    }
};
```

> 用时5min



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

思路：双指针处理即可,主要是考虑到各自的位置进行swap

```cpp
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



## E303.区域和检索 - 数组不可变

https://leetcode.cn/problems/range-sum-query-immutable/

```cpp
#include <iostream>
#include <ranges>
#include <vector>
using namespace std;

class NumArray
{
private:
    vector<int> prefixSum;

public:
    NumArray(vector<int> &nums) : prefixSum(nums.size() + 1)
    {
        for (auto [i, v] : nums | views::enumerate)
            prefixSum[i + 1] = prefixSum[i] + v;
    }

    int sumRange(int left, int right)
    {
        return prefixSum[right + 1] - prefixSum[left];
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    vector<int> nums = {-2, 0, 3, -5, 2, -1};
    int left = 2, right = 5;
    NumArray *obj = new NumArray(nums);
    int param_1 = obj->sumRange(left, right);
    cout << param_1 << '\n';
    return 0;
}

```





## E868.二进制间距

bit manipulation, https://leetcode.cn/problems/binary-gap/

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution
{
public:
    int binaryGap(int n)
    {
        int last = -1, ans = 0;
        for (int i = 0; n; ++i)
        {
            if (n & 1)
            {
                if (last != -1)
                    ans = max(ans, i - last);
                last = i;
            }
            n >>= 1;
        }

        return ans;
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    Solution sol;
    cout << sol.binaryGap(22) << '\n';
    return 0;
}
```

>共用时5min



简单的位运算

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int binaryGap(int n) {
        int ans = 0, prev = -1, pos = 0;
        while (n) {
            if (n & 1) {
                if (prev != -1) ans = max(ans, pos - prev);
                prev = pos;
            }
            n >>= 1;
            pos++;
        }
        return ans;
    }
};

```

> 用时5min



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

```cpp
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



## E1356.根据数字二进制下 1 的数目排序

bit manipulation, https://leetcode.cn/problems/sort-integers-by-the-number-of-1-bits/

思路：学会了内置的 `__builtin_popcount` 用于计算二进制中 1 的个数

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<int> sortByBits(vector<int>& arr) {
        sort(arr.begin(), arr.end(), [](int a, int b) {
            // __builtin_popcount 用于计算一个整数的二进制表示中 1 的个数
            // 可用 while(n) { if (n & 1) count++; n >>= 1; } 实现
            int count_a = __builtin_popcount(a);
            int count_b = __builtin_popcount(b);
            if (count_a == count_b) {
                return a < b;
            }
            return count_a < count_b;
        });
        return arr;
    }
};
```

> 用时5min



# 力扣中等&挑战

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

```cpp
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

```cpp
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

```cpp
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

```cpp
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



思路：bfs 遍历即可

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (!root) return res;
        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int sz = q.size();
            vector<int> cur_level(sz);
            for (int i = 0; i < sz; i++) {
                TreeNode* node = q.front();
                q.pop();
                cur_level[i] = node->val;
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            res.push_back(cur_level);
        }

        return res;
    }
};
```





## M129.求根节点到叶节点数字之和

dfs, https://leetcode.cn/problems/sum-root-to-leaf-numbers/

思路：在遍历时，把当前路径代表的数字累计下去（上一层的值 × 10 + 当前节点值），到叶子节点时就把这条路径的数字加入总和。

```cpp
class Solution {
public:
    int sumNumbers(TreeNode* root) {
        return dfs(root, 0);
    }

private:
    int dfs(TreeNode* node, int current) {
        if (!node) return 0;
        int val = current * 10 + node->val;
        if (!node->left && !node->right)  // 到达叶子
            return val;
        return dfs(node->left, val) + dfs(node->right, val);
    }
};
```



## M131.分割回文串

dp, backtracking, https://leetcode.cn/problems/palindrome-partitioning/

思路：dp预先计算字符串所有子串的回文信息并存储在DP表中，然后通过回溯算法进行深度优先搜索，在每一步利用DP表快速判断子串是否回文来指导分割决策，当搜索到字符串末尾时将当前分割方案加入结果集，用时一个小时（还是不熟练，小错误不断，太菜了）

```cpp
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





```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

class Solution
{
public:
    vector<vector<string>> partition(string s)
    {
        int n = s.length();
        vector<vector<string>> ans;
        vector<string> a;

        auto dfs = [&](this auto &&dfs, int i)
        {
            if (i == n)
            {
                ans.emplace_back(a);
                return;
            }

            for (int j = i; j < n; ++j)
            {
                string sub = s.substr(i, j - i + 1);
                if (isPanlindromic(sub))
                {
                    a.emplace_back(sub);
                    dfs(j + 1);
                    a.pop_back();
                }
            }
        };

        dfs(0);
        return ans;
    }

private:
    inline bool isPanlindromic(const string &s)
    {
        int l = 0, r = s.length() - 1;
        while (l < r)
            if (s[l++] != s[r--])
                return false;
        return true;
    }
};

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    Solution sol;
    string s = "aab";
    for (auto i : sol.partition(s))
    {
        for (auto j : i)
            cout << j << ' ';
        cout << '\n';
    }
    return 0;
}
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





```cpp
class LRUCache {
public:
    int cap,sz=0;
    list<int> l;
    int mp[100005], pos[100005], cnt[100005];
    LRUCache(int capacity) {
        cap=capacity;
        memset(mp,-1,sizeof(mp));
    }
    
    int get(int key) {
        if(mp[key]!=-1) {
            l.push_back(key);
            cnt[key]++;
        }
        return mp[key];
    }
    
    void put(int key, int value) {
        if(mp[key]!=-1) {
            mp[key]=value;
            cnt[key]++;
            l.push_back(key);
        }else {
            sz++;
            mp[key]=value;
            cnt[key]++;
            l.push_back(key);
            while(sz>cap) {
                if(--cnt[l.front()]==0) {
                    mp[l.front()]=-1;
                    sz--;
                }
                l.pop_front();
            }
        }
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```





## M200.岛屿数量

dfs, bfs, https://leetcode.cn/problems/number-of-islands/ 

思路：通过dfs，bfs遍历算法，在遇到陆地('1')时进行连通分量标记并计数，利用搜索过程将相邻陆地沉没为水域从而避免重复统计。

```cpp
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



## M234.回文链表

linked list, two pointers, https://leetcode.cn/problems/palindrome-linked-list/

<mark>请用快慢指针实现</mark> `O(1)` 空间复杂度。



```cpp
class Solution {
    ListNode* middleNode(ListNode* head) {
        ListNode* slow = head, *fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }

    ListNode* reverseList(ListNode* head) {
        ListNode* pre = nullptr, *cur = head;
        while (cur) {
            ListNode* nxt = cur->next;
            cur->next = pre;
            pre = cur;
            cur = nxt;
        }
        return pre;
    }

public:
    bool isPalindrome(ListNode* head) {
        ListNode* mid = middleNode(head);
        ListNode* head2 = reverseList(mid);
        while (head2) {
            if (head->val != head2->val) {
                return false;
            }
            head = head->next;
            head2 = head2->next;
        }
        return true;
    }
};
```





## M304.二维区域和检索 - 矩阵不可变

prefix sum, https://leetcode.cn/problems/range-sum-query-2d-immutable/

二维前缀和

```cpp
#include <iostream>
#include <vector>
using namespace std;

class NumMatrix
{
    vector<vector<int>> sum;

public:
    NumMatrix(vector<vector<int>> &matrix)
    {
        int n = matrix.size(), m = matrix[0].size();
        sum.resize(n + 1, vector<int>(m + 1));
        for (int i = 0; i < n; ++i)
            for (int j = 0; j < m; ++j)
                sum[i + 1][j + 1] = sum[i + 1][j] + sum[i][j + 1] - sum[i][j] + matrix[i][j];
    }

    int sumRegion(int row1, int col1, int row2, int col2)
    {
        return sum[row2 + 1][col2 + 1] - sum[row2 + 1][col1] - sum[row1][col2 + 1] + sum[row1][col1];
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    vector<vector<int>> matrix = {{3, 0, 1, 4, 2}, {5, 6, 3, 2, 1}, {1, 2, 0, 1, 5}, {4, 1, 0, 1, 7}, {1, 0, 3, 0, 5}};
    NumMatrix *numMatrix = new NumMatrix(matrix);
    cout << numMatrix->sumRegion(2, 1, 4, 3) << '\n'; // return 8 (红色矩形框的元素总和)
    cout << numMatrix->sumRegion(1, 1, 2, 2) << '\n'; // return 11 (绿色矩形框的元素总和)
    cout << numMatrix->sumRegion(1, 2, 2, 4) << '\n'; // return 12 (蓝色矩形框的元素总和)
    return 0;
}
```

>共用时10min



思路：预处理二维前缀和．时间复杂度：构造 $O(mn)$，单次查询 $O(1)$．

```cpp
class NumMatrix {
   public:
    vector<vector<int>> A;
    NumMatrix(vector<vector<int>>& matrix) {
        const int n = matrix.size(), m = matrix.front().size();
        A.resize(n + 1);
        A[0].resize(m + 1);
        for(int i = 0; i < n; i++) {
            A[i + 1].resize(m + 1);
            partial_sum(matrix[i].begin(), matrix[i].end(),
                        A[i + 1].begin() + 1);
        }
        for(int j = 1; j <= m; j++)
            for(int i = 1; i <= n; i++) A[i][j] += A[i - 1][j];
    }

    int sumRegion(int row1, int col1, int row2, int col2) {
        return A[row2 + 1][col2 + 1] - A[row2 + 1][col1] - A[row1][col2 + 1] +
               A[row1][col1];
    }
};
```







## M647.回文子串

https://leetcode.cn/problems/palindromic-substrings/

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution
{
public:
    int countSubstrings(string s)
    {
        string t = "^#";
        for (char c : s)
        {
            t += c;
            t += "#";
        }
        t += "$";

        int n = t.size();
        int ans = 0;
        vector<int> p(n);
        int r = 0, c = 0;
        for (int i = 1; i < n - 1; ++i)
        {
            if (i < r)
                p[i] = min(p[(c << 1) - i], r - i);
            else
                p[i] = 1;
            while (t[i - p[i]] == t[i + p[i]])
                ++p[i];
            if (i + p[i] > r)
                r = i + p[i], c = i;
            ans += p[i] / 2;
        }

        return ans;
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    Solution sol;
    string s = "aaa";
    cout << sol.countSubstrings(s) << '\n';
    return 0;
}
```





## M1123.最深叶节点的最近公共祖先

dfs, https://leetcode.cn/problems/lowest-common-ancestor-of-deepest-leaves/

思路：如果直接想还挺难,但是如果考虑到二叉树的通用递归思路,那么就可以有很好的解决方法,即利用递归的思路

如果左子树更深，最深叶节点在左子树中，我们返回 {左子树深度 + 1，左子树的 lca 节点}
如果右子树更深，最深叶节点在右子树中，我们返回 {右子树深度 + 1，右子树的 lca 节点}
如果左右子树一样深，左右子树都有最深叶节点，我们返回 {左子树深度 + 1，当前节点}

```cpp
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



思路：dfs 返回左右子树的最大深度和 lca , 选取深度最大的子树及其 lca, 如果深度相等, 则说明当前节点是 lca

```cpp
class Solution {
public:
    TreeNode* lcaDeepestLeaves(TreeNode* root) {
        return dfs(root).first;
    }

    pair<TreeNode*, int> dfs(TreeNode* root) {
        if (!root) return {nullptr, 0};

        auto [left_lca, left_depth] = dfs(root->left);
        auto [right_lca, right_depth] = dfs(root->right);
        if (left_depth < right_depth) {
            return {right_lca, right_depth + 1};
        } else if (left_depth > right_depth) {
            return {left_lca, left_depth + 1};
        } else {
            return {root, left_depth + 1};
        }
    }
};
```





## M1680.连接连续二进制数字

bit manipulation, https://leetcode.cn/problems/concatenation-of-consecutive-binary-numbers/



思路：记录当前数字的二进制长度即可, 用 `(i & (i - 1)) == 0` 判断 `i` 是否为二的幂次

```c++
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int concatenatedBinary(int n) {
        int len = 0, ans = 0, mod = 1e9 + 7;
        for (int i = 1; i <= n; i++) {
            if ((i & (i - 1)) == 0) {
                len++;
            }
            ans = ((long long)ans << len | i) % mod;
        }
        return ans;
    }
};
```

> 用时10min



## M1461.检查一个字符串是否包含所有长度为 K 的二进制子串

bit manipulation, https://leetcode.cn/problems/check-if-a-string-contains-all-binary-codes-of-size-k/



思路：滑动窗口, 学会了 `stoi` (string to int) 的用法, `int stoi( const std::string& str, std::size_t* pos = nullptr, int base = 10 )`

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    bool hasAllCodes(string s, int k) {
        int num = stoi(s.substr(0, k), nullptr, 2);
        unordered_set<int> a;
        a.insert(num);
        for (int i = k; i < s.length(); i++) {
            num <<= 1;
            if (num >= (1 << k)) {
                num -= (1 << k);
            }
            num += (s[i] - '0');
            a.insert(num);
        }

        return a.size() == (1 << k);
    }
};
```

> 用时10min



```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

class Solution
{
public:
    bool hasAllCodes(string s, int k)
    {
        int total_needed = 1 << k;
        if (s.size() < (size_t)total_needed + k - 1)
            return false;

        vector<bool> seen(total_needed, false);

        int x = 0;
        int cnt = 0;
        int MASK = total_needed - 1;

        for (int i = 0; i < k - 1; ++i)
        {
            x = (x << 1) | (s[i] & 1);
        }

        for (int i = k - 1; i < s.length(); ++i)
        {
            x = ((x << 1) & MASK) | (s[i] & 1);
            if (!seen[x])
            {
                seen[x] = true;
                if (++cnt == total_needed)
                    return true;
            }
        }

        return false;
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    Solution sol;
    string s = "0110";
    int k = 2;
    cout << sol.hasAllCodes(s, k) << '\n';
    return 0;
}
```

>共用时20min



思路：直接提取 $s$ 的所有长度为 $k$ 的子串．时间复杂度为 $O(|s|)$．

```cpp
class Solution {
   public:
    bool hasAllCodes(string s, int k) {
        const int n = s.length();
        if(n - k + 1 < (1 << k)) return false;
        vector<bool> buc;
        buc.resize(1 << k);
        int x = 0;
        for(int i = 0; i < n; i++) {
            x <<= 1;
            x |= s[i] - '0';
            x &= (1 << k) - 1;
            if(i >= k - 1) buc[x] = true;
        }
        return ranges::count(buc, false) == 0;
    }
};
```





## M1536.排布二进制网格的最少交换次数

greedy, matrix, https://leetcode.cn/problems/minimum-swaps-to-arrange-a-binary-grid/

思路：统计后缀零后第一个1的位置再按行冒泡检查能否满足  

```cpp
class Solution {
public:
    int minSwaps(vector<vector<int>>& grid) {
        int n = grid.size();
        vector<int>col(n,-1);
        for (int i = 0; i < n; i++) {
            for (int j = n - 1; j >= 0; j--) {
                if (grid[i][j] == 1) {
                    col[i] = j;
                    break;
                }
            }
        }
        int ans = 0, check = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                if (col[j] <= i) {
                    ans += (j - i);
                    for (int k = j; k > i; k--)
                        col[k] = col[k - 1];
                    goto nxt;
                }
            }
            return -1;
        nxt:
            ;
        }
        return ans;
    }
};
```

 

思路：简单的贪心, 统计每行的末尾0的个数即可

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int minSwaps(vector<vector<int>>& grid) {
        int n = grid.size();
        vector<int> count_zeros(n, 0);
        for (int i = 0; i < n; i++) {
            for (int j = n - 1; j >= 0; j--) {
                if (grid[i][j] == 0) {
                    count_zeros[i]++;
                } else {
                    break;
                }
            }
        }

        int ans = 0;
        for (int i = 0; i < n; i++) {
            int col = -1;
            for (int j = i; j < n; j++) {
                if (count_zeros[j] >= n - 1 - i) {
                    col = j;
                    ans += col - i;
                    for (int k = col; k > i; k--) {
                        swap(count_zeros[k], count_zeros[k - 1]);
                    }
                    break;
                }
            }
            if (col == -1) {
                return -1;
            }
        }
        return ans;
    }
};
```

> 用时15min



## M1545. 找出第 N 个二进制字符串中的第 K 位

https://leetcode.cn/problems/find-kth-bit-in-nth-binary-string/

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution
{
public:
    char findKthBit(int n, int k)
    {
        if (n == 1)
            return '0';
        if (k == (1 << (n - 1)))
            return '1';
        if (k < (1 << (n - 1)))
            return findKthBit(n - 1, k);
        return findKthBit(n - 1, (1 << n) - k) ^ 1;
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    Solution sol;
    int n = 4, k = 11;
    cout << sol.findKthBit(n, k) << '\n';
    return 0;
}
```

被0神的方法震撼到了。。。数学，很神奇吧

```cpp
class Solution
{
public:
    char findKthBit(int n, int k)
    {
        if (k % 2)
            return '0' + k / 2 % 2;
        k /= k & -k;
        return '1' - k / 2 % 2;
    }
};
```



## M1680.连接连续二进制数字

bit manipulation, https://leetcode.cn/problems/concatenation-of-consecutive-binary-numbers/



思路：记录当前数字的二进制长度即可, 用 `(i & (i - 1)) == 0` 判断 `i` 是否为二的幂次

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int concatenatedBinary(int n) {
        int len = 0, ans = 0, mod = 1e9 + 7;
        for (int i = 1; i <= n; i++) {
            if ((i & (i - 1)) == 0) {
                len++;
            }
            ans = ((long long)ans << len | i) % mod;
        }
        return ans;
    }
};
```

> 用时10min



```cpp
#include <iostream>
#include <numeric>
using namespace std;

class Solution
{
public:
    int concatenatedBinary(int n)
    {
        constexpr int MOD = 1000000007;
        long long res = 0;
        for (int i = 1; i <= n; ++i)
        {
            int w = bit_width((uint32_t)i);
            res = (res << w | i) % MOD;
        }
        return res;
    }
};

int main()
{
    cin.tie(nullptr)->sync_with_stdio(false);

    Solution sol;
    int n = 12;
    cout << sol.concatenatedBinary(n) << '\n';
    return 0;
}
```


>共用时5min




## M1760.袋子里最少数目的球

binary search, https://leetcode.cn/problems/minimum-limit-of-balls-in-a-bag/




思路：一开始的想法是将最多的一个袋子拆成 m + n 暴力回溯，显然太暴力了，后来看了题解，反向设置最终目标加二分法才是最合适的，用时约30分钟

```cpp
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




二分答案

```cpp
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





## M3532.针对图的路径存在性查询 I

union find, binary search, https://leetcode.cn/problems/path-existence-queries-in-a-graph-i/

思路：

- 由于 `nums` 单调不降排序，若 $r - l > 1$，则 $l, r$ 间有边直接相连意味着 $\text{nums}_r - \text{nums}_l \leq \text{maxDiff} \Rightarrow \forall l \leq i < r, \text{nums}_{i + 1} - \text{nums}_i \leq \text{nums}_r - \text{nums}_l \leq \text{maxDiff}$，即边 $(i, i + 1)$ 存在，$(l, r)$ 这条边可以被“替代”。
- 故只需考虑所有形如 $(i, i + 1)$ 的边，进而可知对每个 $i$ 都有 $\text{maxr}_i$，表示从 $i$ 出发向右、能到达的最大节点编号。
- 回答询问时，不妨设 $u \leq v$，则存在路径当且仅当 $v \leq \text{maxr}_u$。

```cpp
class Solution {
public:
	vector<bool> pathExistenceQueries(int n, vector<int>& nums, int maxDiff, vector<vector<int>>& queries) {
		vector<int> maxr(n);
		vector<bool> answer;
		for (int i = 0; i < n; i++){
			int l = i;
			while (i + 1 < n && nums[i + 1] - nums[i] <= maxDiff) i++;
			for (int j = l; j <= i; j++){
				maxr[j] = i;
			}
		}
		for (vector<int> i : queries){
			if (i[0] > i[1]) swap(i[0], i[1]);
			answer.push_back(i[1] <= maxr[i[0]]);
		}
		return answer;
	}
};
```





## T51.N皇后

backtracking, [https://leetcode.cn/problems/n-queens/](https://leetcode.cn/problems/n-queens/)

 

```cpp
#include <iostream>  
 #include <vector>  
 using namespace std;  
 
 vector<int> row;  
 
 bool is_Valid(int x, int y)  
 {  
     for (int i = 0; i < x; i++)  
         if (row[i] == y || abs(x - i) == abs(y - row[i]))  
             return false;  
     return true;  
 }  
 
 void solve(int n, vector<vector<string>>& q, int x)  
 {  
     if (x == n)  
     {  
         vector<string> tmp(n, string(n, '.'));  
         for (int i = 0; i < row.size(); i++)  
             tmp[i][row[i]] = 'Q';  
         q.push_back(tmp);  
         return;  
     }  
     for (int i = 0; i < n; i++)  
         if (is_Valid(x, i))  
         {  
             row.push_back(i);  
             solve(n, q, x + 1);  
             row.pop_back();  
         }  
 }  

 vector<vector<string>> solveNQueens(int n)  
 {  
     vector<vector<string>> ans;  
     solve(n, ans, 0);  
     return ans;  
 }  

 int main()  
 {  
     ios::sync_with_stdio(false);  
     cin.tie(nullptr);  

     int n = 4;  
     for (auto i : solveNQueens(n))  
     {  
         for (auto j : i)  
             cout << j << ' ';  
         cout << '\n';  
     }  
     return 0;  
 }
```





## T3892 : 产生至少 K 个峰值的最少操作次数

【江昊中 数学科学学院】做了力扣周赛, 周赛第四题除了用 dp , 问了 ai 后还学习到了反悔贪心的算法

dp, greedy with regret, https://leetcode.cn/problems/minimum-operations-to-achieve-at-least-k-peaks/


```cpp
class Solution {
public:
    int minOperations(vector<int>& nums, int k) {
        const int n = nums.size();
        if (k > n / 2) return -1;

        // 使用两个数组 prev 和 next 来模拟双向链表
        vector<int> prev(n), next(n);
        for (int i = 0; i < n; i++) {
            prev[i] = (i + n - 1) % n;
            next[i] = (i + 1) % n;
        }

        vector<int> cost(n);
        for (int i = 0; i < n; i++) {
            int prev_val = nums[prev[i]];
            int next_val = nums[next[i]];
            cost[i] = max(0, max(prev_val, next_val) + 1 - nums[i]);
        }

        // 最小堆, 存放 {代价, idx}
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
        for (int i = 0; i < n; i++) {
            pq.push({cost[i], i});
        }

        vector<bool> visited(n, false);
        int ans = 0;

        // 贪心选取 k 次
        for (int i = 0; i < k; i++) {
            // 跳过已经被删除的节点
            while (!pq.empty() && visited[pq.top().second]) {
                pq.pop();
            }

            auto [val, idx] = pq.top();
            pq.pop();

            ans += val;
            int l = prev[idx], r = next[idx];
            visited[l] = visited[r] = true;

            // 将具有反悔代价的节点加入优先队列
            // 逻辑上等价于放弃当前节点 idx, 转而选取 l 和 r
            cost[idx] = cost[l] + cost[r] - val;
            pq.push({cost[idx], idx});

            // 在链表中删除 l 和 r
            prev[idx] = prev[l];
            next[idx] = next[r];
            next[prev[l]] = idx;
            prev[next[r]] = idx;
        }
        return ans;
    }
};
```





# Other

## sy132: 全排列I 中等

[https://sunnywhy.com/sfbj/4/3/132](https://sunnywhy.com/sfbj/4/3/132)

 

```cpp
 #include <iostream>  
 #include <vector>  
 using namespace std;  
 
 void permute(vector<bool>& valid, vector<int>& nums, int first, int n)  
 {  
     if (first == n + 1)  
     {  
         for (int i = 0; i < n; i++)  
             i < n - 1 ? cout << nums[i] << ' ' : cout << nums[i] << '\n';  
         return;  
     }  
     for (int i = 1; i <= n; i++)  
         if (valid[i])  
         {  
             valid[i] = false;  
             nums.push_back(i);  
             permute(valid, nums, first + 1, n);  
             valid[i] = true;  
             nums.pop_back();  
         }  
 }  
 
 int main()  
 {  
     ios::sync_with_stdio(false);  
     cin.tie(nullptr);  
 
     int n;  
     cin >> n;  
     vector<int> nums;  
     vector<bool> valid(n + 1, true);  
     permute(valid, nums, 1, n);  
     return 0;  
 }
```





## sy578

```cpp
#include <iostream>
using namespace std;

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, k;
    string s;
    cin >> n >> k >> s;

    int l = 0, r = -1, cnt = 0;
    int maxLen = 0;
    while (r < n)
    {
        if (cnt <= k)
        {
            maxLen = max(maxLen, r - l + 1);
            r++;
            if (r < n && s[r] == '0')
                cnt++;
        }
        else
        {
            if (s[l] == '0')
                cnt--;
            l++;
        }
    }

    cout << maxLen << '\n';
    return 0;
}
```





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

```cpp
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



## P1776 宝物筛选

bit manipulation,dp, https://www.luogu.com.cn/problem/P1776


【姚博骞 物院】思路：多重背包可以把物品总数拆成若干二进制个数的和，这样加和可以模拟所有可能的选择个数。

```cpp
//将每个物品数量拆成二进制个数的01背包
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;
int max(int a,int b){
    return (a>b)?a:b;
}
int min(int a,int b){
    return (a<b)?a:b;
}
int main(){
    int n,wmax;
    cin>>n>>wmax;//n还未输入时不能用n初始化数组
    vector<int> v(n);
    vector<int> w(n);
    vector<int> m(n);
    vector<int>dp(wmax+1,0);
    for(int i=0;i<n;i++){
        cin>>v[i]>>w[i]>>m[i];   
    }
    for(int i=0;i<n;i++)//考虑要不要选这个物品
    {
        int num=min(wmax/w[i],m[i]);
        for(int k=1;num>0;k<<=1){
            int cnt=min(k,num);
            int value=cnt*v[i];
            int weight=cnt*w[i];
            for(int j=wmax;j>=weight;j--){
                dp[j]=max(dp[j-weight]+value,dp[j]);
            }
            num-=cnt;
        }
    }
    cout<<dp[wmax];
}
```





## P2698 [USACO12MAR] Flowerpot S

monotonic queue, https://www.luogu.com.cn/problem/P2698



思路：双指针+单调队列

```cpp
#include <bits/stdc++.h>
using namespace std;
int n, D;
const int N = 1e5+20;
pair<int, int> r[N];
pair<int, int> ql[N], qr[N];
int qlh, qlt, qrh, qrt;
int main() {
    unsigned W = -1;
    cin >> n >> D;
    for (int i=0; i<n; i++)
        cin >> r[i].first >> r[i].second;
    sort(r, r+n);
    qlh = qlt = qrh = qrt = 0;
    for (int i=0, j=0; i<n; i++) {
        if (qlh != qlt and ql[qlh].first < i) qlh++;
        if (qrh != qrt and qr[qrh].first < i) qrh++;
        while (j<n and ql[qlh].second-qr[qrh].second < D) {
            int y = r[j].second; // j, y
            while (qlh != qlt and ql[qlt-1].second <= y) {
                qlt--;
            }
            ql[qlt] = make_pair(j, y); qlt++;
            while (qrh != qrt and qr[qrt-1].second >= y) {
                qrt--;
            }
            qr[qrt] = make_pair(j, y); qrt++;
            j++;
        }
        if (ql[qlh].second-qr[qrh].second >= D) {
            //cout << i << ' ' << j << endl;
            W = min(W, unsigned(r[j-1].first-r[i].first));
        }
    }
    cout << int(W) << endl;
    return 0;
}
```



思路：一眼顶针鉴定为二分答案。然后用 rust 写了下试试

```rust
// use std::collections::VecDeque;
// use std::fs::read;
use std::{
    collections::VecDeque,
    io::{self, BufWriter, Read, Write},
};

struct FastReader<R: Read> {
    reader: R,
    buffer: [u8; 65536],
    pos: usize,
    cap: usize,
}

impl<R: Read> FastReader<R> {
    fn new(reader: R) -> Self {
        Self {
            reader,
            buffer: [0; 65536],
            pos: 0,
            cap: 0,
        }
    }

    fn read_byte(&mut self) -> Option<u8> {
        if self.pos >= self.cap {
            self.cap = self.reader.read(&mut self.buffer).ok()?;
            self.pos = 0;
            if self.cap == 0 {
                return None;
            }
        }
        let b = self.buffer[self.pos];
        self.pos += 1;
        Some(b)
    }

    fn next_int<T: FromIntegral>(&mut self) -> T {
        let mut b = self.read_byte().unwrap();
        while b <= b' ' {
            b = self.read_byte().unwrap();
        }

        let mut neg = false;
        if b == b'-' {
            neg = true;
            b = self.read_byte().unwrap();
        }

        let mut res = T::from_u8(b - b'0');
        while let Some(c) = self.read_byte() {
            if c <= b' ' {
                break;
            }
            res = res * T::from_u8(10) + T::from_u8(c - b'0');
        }

        if neg { T::zero() - res } else { res }
    }

    fn next_string(&mut self) -> String {
        let mut b = self.read_byte().unwrap();
        while b <= b' ' {
            b = self.read_byte().unwrap();
        }

        let mut res = String::new();
        res.push(b as char);
        while let Some(c) = self.read_byte() {
            if c <= b' ' {
                break;
            }
            res.push(c as char);
        }
        res
    }
}

trait FromIntegral:
    std::ops::Mul<Output = Self> + std::ops::Add<Output = Self> + std::ops::Sub<Output = Self> + Copy
{
    fn from_u8(v: u8) -> Self;
    fn zero() -> Self;
}

macro_rules! impl_integral {
    ($($t:ty)*) => { $( impl FromIntegral for $t {
        fn from_u8(v: u8) -> Self { v as $t }
        fn zero() -> Self { 0 }
    } )* };
}
impl_integral!(i32 i64 isize usize i128 u8 u16 u32 u64 u128);

type Point = (i32, i32);

fn check(x: i32, a: &[Point], d: i32, q_min: &mut [usize], q_max: &mut [usize]) -> bool {
    let mut head_min = 0;
    let mut tail_min = 0;
    let mut head_max = 0;
    let mut tail_max = 0;
    let mut l = 0;

    for r in 0..a.len() {
        while tail_min > head_min && a[q_min[tail_min - 1]].1 >= a[r].1 {
            tail_min -= 1;
        }
        q_min[tail_min] = r;
        tail_min += 1;
        while tail_max > head_max && a[q_max[tail_max - 1]].1 <= a[r].1 {
            tail_max -= 1;
        }
        q_max[tail_max] = r;
        tail_max += 1;
        while a[r].0 - a[l].0 > x {
            l += 1;
            if q_min[head_min] < l {
                head_min += 1;
            }
            if q_max[head_max] < l {
                head_max += 1;
            }
        }
        if a[q_max[head_max]].1 - a[q_min[head_min]].1 >= d {
            return true;
        }
    }
    false
}

fn main() {
    let mut reader = FastReader::new(io::stdin().lock());
    let mut writer = BufWriter::new(io::stdout().lock());

    let n: usize = reader.next_int();
    let d: i32 = reader.next_int();

    let mut a: Vec<Point> = Vec::with_capacity(n);
    for _ in 0..n {
        a.push((reader.next_int(), reader.next_int()));
    }

    a.sort_unstable_by_key(|p| p.0);

    let mut q_min = vec![0; n];
    let mut q_max = vec![0; n];

    let mut l = 0;
    let mut r = 1000001;
    let mut ans = -1;

    while l <= r {
        let mid = (l + r) >> 1;
        if check(mid, &a, d, &mut q_min, &mut q_max) {
            ans = mid;
            r = mid - 1;
        } else {
            l = mid + 1;
        }
    }
    writeln!(writer, "{}", ans).unwrap();
}
```



思路：按 x 排序，对于每个 (x,y) 为左端点，找到最靠左的右端点满足 y 坐标之差大于等于 d，单调队列实现。

方法二：按 y 排序，找到符合要求的点钟与当前 (x,y) 横坐标差的绝对值最小的，平衡树实现（实则用 STL::set逃课）

代码

```python
n,d = map(int,input().split())
a = []
for i in range(n):
    a.append(tuple(map(int,input().split())))
b = sorted(a,key = lambda x: x[0])

d1,d2 = [0]*n,[0]*n
h1,h2,t1,t2 = 0,0,-1,-1
inf = 2e9
ans = inf
r = -1
for l in range(n):
    while(h1<=t1 and d1[h1]<l): h1 += 1
    while(h2<=t2 and d2[h2]<l): h2 += 1
    while(r<n-1 and b[d1[h1]][1]-b[d2[h2]][1]<d):
        r += 1
        while(h1<=t1 and b[d1[t1]][1]<=b[r][1]): t1 -= 1
        while(h2<=t2 and b[d2[t2]][1]>=b[r][1]): t2 -= 1
        t1 += 1
        t2 += 1
        d1[t1] = r
        d2[t2] = r
#    print(l,r)
    if(r!=n-1):
        ans = min(ans,b[r][0]-b[l][0])
if(ans>=inf):
    print(-1)
else:
    print(ans)

```





方法二：

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define ll long long
#define For(i,l,r) for(ll i=(l),i##_=(r);i<=i##_;++i)
#define FOR(i,l,r) for(ll i=(l),i##_=(r);i>=i##_;--i)
#define Rep(i,l,r) for(ll i=(l),i##_=(r);i<i##_;++i)

#define pr pair<ll,ll>
pr a[100010];
const ll inf = 1e9;
set<ll> s;
int main(){
	
	ll n,d;cin>>n>>d; 
	For(i,1,n){
		ll x,y;cin>>x>>y;
		a[i] = make_pair(x,y);
	}
	
	sort(a+1,a+n+1,[](pr a,pr b){return a.second<b.second;});
	ll r = n,ans = inf;
	FOR(l,n,1){
//		if(a[r].second-a[l].second<d) continue;
		while(a[r].second-a[l].second>=d)
		    s.insert(a[r].first),--r;
		auto it = s.lower_bound(a[l].first);
		ll x1=-inf*2,x2=inf*2;
		if(it!=s.end()) x2 = *it;
		if(it!=s.begin()) --it,x1 = *it;
		ans = min(ans,min(x2-a[l].first,a[l].first-x1));
	}
	cout<<(ans>=inf?-1ll:ans);
	return 0;
}
~~~

