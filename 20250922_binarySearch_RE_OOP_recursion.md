# 2025/09/22 二分、OOP、正则 & 递归

*Updated 2025-09-29 11:48 GMT+8*  
 *Compiled by Hongfei Yan (2025 Fall)*  



# 1 二分查找（Binary Search）

二分查找的难点在于边界条件。推荐参考 Python 标准库 **bisect** 的源码实现（采用左闭右开区间）：
https://github.com/python/cpython/blob/main/Lib/bisect.py



核心思想：当问题求”最小化最大值“或”最大化最小值“时，二分枚举答案。

- 模版：验证函数 + 二分搜索
- 关键：讲优化问题转化为判定问题（“能否达到？”）
- 应用：袋子分球、预算分配、资源分配类问题



## 相关题目：

- **1760. 袋子里最少数目的球**（binary search）
  https://leetcode.cn/problems/minimum-limit-of-balls-in-a-bag/
- **M08210: 河中跳房子/石头**（binary search）
  http://cs101.openjudge.cn/practice/08210
- **M04135: 月度开销**（binary search）
  http://cs101.openjudge.cn/practice/04135
- **M02456: Aggressive cows**（binary search）
  http://cs101.openjudge.cn/practice/02456







> **提示**：OpenJudge 使用 Python 3.8
>
> https://stackoverflow.com/questions/43233535/explicitly-define-datatype-in-python-function 
>
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/image-20231017141419717.png" alt="image-20231017141419717" style="zoom: 50%;" />
>
> 
>
> **OpenJudge 是 Python 3.8**, ，一些新版本 Python 的类型标注可能会触发 RE。
>
> 
>
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/f5805974d7220205945e7182e69058b2.png" alt="f5805974d7220205945e7182e69058b2" style="zoom:50%;" />
>
> 
>
> <img src="https://raw.githubusercontent.com/GMyhf/img/main/img/d617953bef96904658310485adbf3f5c.png" alt="d617953bef96904658310485adbf3f5c" style="zoom:50%;" />
>
> 
>
> OJ的pylint是静态检查，有时候报的compile error不对。解决方法有两种，如下：
> 1）第一行加# pylint: skip-file
> 2）方法二：如果函数内使用全局变量（变量类型是immutable，如int），则需要在程序最开始声明一下。如果是全局变量是list类型，则不受影响。





# 2 正则表达式（Regular Expression）



正则表达式是字符串匹配的“规则语言”，由普通字符与元字符组合而成，可实现搜索、验证、替换等功能。

常用资源：

- Python 正则表达式教程：https://www.runoob.com/python/python-reg-expressions.html
- 在线调试工具：[https://regex101.com](https://regex101.com/)
- CSDN 详解文章：https://blog.csdn.net/weixin_43347550/article/details/105158003

常见元字符：

- `.` 任意单字符（除换行）
- `^` 匹配开头
- `$` 匹配结尾
- `*` 前一子表达式重复零次或多次
- `+` 前一子表达式重复一次或多次
- `?`和{0,1}一样，前一字表达式0次或1次
- `{n}` 重复 n 次
- `{n,m}`匹配在 {n,m} 前面的东西，比如：o{1,3} 将匹配“fooooood"中的前三
- `[abc]` 字符集
- `\d` 数字 `[0-9]`
- `\w` 字母/数字/下划线 `[A-Za-z0-9_]`

应用场景：

- **数据验证**（邮箱、手机号等格式检查）
- **查找替换**（批量文本处理）
- **信息提取**（日志分析、网页解析）

------

## 示例题目



### 04015: 邮箱验证

strings, http://cs101.openjudge.cn/practice/04015

POJ 注册的时候需要用户输入邮箱，验证邮箱的规则包括：
1)有且仅有一个'@'符号
2)'@'和'.'不能出现在字符串的首和尾
3)'@'之后至少要有一个'.'，并且'@'不能和'.'直接相连
满足以上3条的字符串为合法邮箱，否则不合法，
编写程序验证输入是否合法

**输入**

输入包含若干行，每一行为一个代验证的邮箱地址，长度小于100

**输出**

每一行输入对应一行输出
如果验证合法，输出 YES
如果验证非法：输出 NO

样例输入

```
.a@b.com
pku@edu.cn
cs101@gmail.com
cs101@gmail
```

样例输出

```
NO
YES
YES
NO
```





这题目输入没有明确结束，需要套在try ...  except里面。测试时候，需要模拟输入结束，看你是window还是mac。If the user hits EOF (*nix: Ctrl-D, Windows: Ctrl-Z+Return), raise EOFError.



题目给的要求是\[\^@\.]，也就是说正常字段只需要不是“@”和“.”即可。以前遇到的要求是：正常字段只能是大小写字母或“-”，所以也试了试[\w-]。虽然regulation需要前后match，也就是说前面加一个“^”，后面加一个“$”， 但 是.match函数本身就是从头开始检索的，所以“^”可以删去。

```python
# https://www.tutorialspoint.com/python/python_reg_expressions.htm
# https://www.geeksforgeeks.org/python-regex/

import re
while True:
    try:
        s = input()
        reg = r'^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$'
        print('YES' if re.match(reg, s) else 'NO')
    except EOFError:
        break
```

> ^：匹配字符串的开始。
> [\w-]+：匹配用户名部分的第一个子部分，允许字母、数字、下划线和连字符，至少有一个字符。
> (\.[\w-]+)*：匹配用户名部分的其余子部分，每个子部分由点分隔，可以有零个或多个这样的子部分。
> @：匹配单个 @ 符号。
> [\w-]+：匹配域名的第一部分，允许字母、数字、下划线和连字符，至少有一个字符。
> (\.[\w-]+)+：匹配域名的后续部分，每个部分由点分隔，至少有一个这样的部分，并且每个部分都至少包含一个字符。
> $：匹配字符串的结尾，确保整个字符串都被匹配到结尾，不允许多余的字符。



```python
# https://www.tutorialspoint.com/python/python_reg_expressions.htm
# https://www.geeksforgeeks.org/python-regex/
import re  
while True: 
    try:
        s = input()
        reg   = r'^[^@\.]+(\.[^@\.]+)*@[^@\.]+(\.[^@\.]+)+$'
        print('YES' if re.match(reg, s) else 'NO')
    except EOFError:
        break
```

> 正则表达式遵循以下规则：
>
> ^：匹配字符串的开始。
>
> `[^@\.]+`：匹配不包含 @ 和 . 的字符序列，确保用户名部分不以 @ 或 . 开始。
> `(\.[^@\.]+)*`：允许用户名部分有多个子部分，每个子部分由点分隔。
> `@`：匹配单个 @ 符号。
> `[^@\.]+`：匹配域名的第一部分，确保其不包含 @ 和 .。
> `(\.[^@\.]+)+`：匹配域名的后续部分，每个部分必须至少包含一个非 @ 和 . 的字符，并且必须至少有一个这样的部分。
> `$`：确保整个字符串都被匹配到结尾，不允许多余的字符。

[\^xyz]，匹配未包含的任意字符。例如，“[\^abc]”可以匹配“plain”中的“plin”任一字符。

$匹配输入行尾。

(pattern)，匹配pattern并获取这一匹配。所获取的匹配可以从产生的Matches集合得到。



https://regex101.com

![image-20231017131949282](https://raw.githubusercontent.com/GMyhf/img/main/img/image-20231017131949282.png)



### 24834: 通配符匹配

http://cs101.openjudge.cn/practice/24834/

给定一个字符串s和一个字符模式p，请实现一个支持'?'和'*'的通配符匹配功能。

其中‘?’可以匹配任何单个字符，如‘a?c’可以成功匹配‘aac’,‘abc’等字符串，但不可匹配‘ac’,‘aaac’等字符串 。

‘\*’ 可以匹配任意长度字符串（包括空字符串）,如‘a*c’可以成功匹配‘ac’,‘abdc’,‘abc’,‘aaac’等字符串，但不可匹配‘acb’，‘cac’等字符串。

两个字符串完全匹配才算匹配成功。

**输入**

输入为一个数字n表示测试字符串与字符模式对数，换行。(n ≤ 30)
后续2n行为每组匹配的s与p，每行字符串后换行。
s 非空，只包含从 a-z 的小写字母。
p 非空，只包含从 a-z 的小写字母，以及字符 ? 和 *。
字符串s和p的长度均小于50

**输出**

每一组匹配串匹配成功输出‘yes’,否则输出‘no’。

样例输入

```
3
abc
abc
abc
a*c
abc
a??c
```

样例输出

```
yes
yes
no
```





```python
#23n2300017735(夏天明BrightSummer)
import re

for i in range(int(input())):
    s, p = input(), input().replace("?", ".{1}").replace("*", ".*") + "$"
    print("yes" if re.match(p, s) else "no")
```

.点，匹配除“\n”和"\r"之外的任何单个字符。要匹配包括“\n”和"\r"在内的任何字符，请使用像“[\s\S]”的模式。

\*，匹配前面的子表达式任意次。例如，z*能匹配“z”，也能匹配“zo”以及“zoo”。*等价于{0,}。



### 58A. Chat room

greedy/strings, 1000, http://codeforces.com/problemset/problem/58/A

Vasya has recently learned to type and log on to the Internet. He immediately entered a chat room and decided to say hello to everybody. Vasya typed the word *s*. It is considered that Vasya managed to say hello if several letters can be deleted from the typed word so that it resulted in the word "hello". For example, if Vasya types the word "ahhellllloou", it will be considered that he said hello, and if he types "hlelo", it will be considered that Vasya got misunderstood and he didn't manage to say hello. Determine whether Vasya managed to say hello by the given word *s*.

**Input**

The first and only line contains the word *s*, which Vasya typed. This word consisits of small Latin letters, its length is no less that 1 and no more than 100 letters.

**Output**

If Vasya managed to say hello, print "YES", otherwise print "NO".

Examples

input

```
ahhellllloou
```

output

```
YES
```

input

```
hlelo
```

output

```
NO
```





```python
import re
s = input()
r = re.search('h.*e.*l.*l.*o', s)
print(['YES', 'NO'][r==None])
```



### LeetCode 65. 有效数字

https://leetcode.cn/problems/valid-number/description/

https://leetcode.cn/problems/valid-number/solutions/564188/you-xiao-shu-zi-by-leetcode-solution-298l/

这个正则表达式 pattern 用于判断一个字符串是否是有效数字。下面我来详细解释一下其中的各个部分：

- `^` 表示匹配字符串的开始位置。
- `[-+]?` 表示一个可选的符号字符，可以是正号 `+` 或负号 `-`。
- `(\d+(\.\d*)?|\.\d+)` 表示有效数字的主要部分，可以分成三种情况：
  - `\d+(\.\d*)?` 表示至少一位数字，后面可选的小数部分，小数部分可以没有或有多个小数位。
  - `|` 表示或的关系。
  - `.\d+` 表示以点 `.` 开始，后面至少一位数字的小数形式。
- `([eE][-+]?\d+)?` 表示指数部分，也是一个可选项，可以是 `e` 或 `E` 开头，后面可选的符号字符，以及至少一位数字。
- `$` 表示匹配字符串的结束位置。

综合起来，整个正则表达式可以解释为：

- 首先可以匹配一个可选的符号字符。
- 接下来是有效数字的主要部分，可以是整数或小数形式。
- 最后是可选的指数部分。

因此，该正则表达式可以匹配符合有效数字要求的字符串。在 Python 中使用 `re.match` 方法进行匹配时，如果匹配成功，说明字符串是一个有效数字，返回 `True`；否则，返回 `None`，表示不是一个有效数字。



```python
class Solution:
    def isNumber(self, s: str) -> bool:
        import re 
        pattern = r'^[-+]?(\d+(\.\d*)?|\.\d+)([eE][-+]?\d+)?$'
        
        ans = re.match(pattern, s) 
        if ans is not None:
            return True
        else:
            return False
```



# 3 OOP

参考资料：
https://github.com/GMyhf/2025fall-cs201/blob/main/20250915_DA_week2_OOP.md
（见 `1.3 面向对象编程` 部分）



> 增加：1.3.2 矩阵乘法运算符
>
> 示例E18161: 矩阵运算(先乘再加)



# 4 递归

参考资料：
https://github.com/GMyhf/2024fall-cs101/blob/main/20241029_recursion.md