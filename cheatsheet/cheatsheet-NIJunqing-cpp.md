一、字符串操作函数
int len = strlen(str1);

// 复制
strcpy(str1, str2);      // 复制str2到str1
strncpy(str1, str2, 5);  // 安全复制，指定长度

// 连接
strcat(str1, str2);      // 将str2连接到str1末尾
strncat(str1, str2, 3);  // 安全连接，指定长度

// 比较
int result = strcmp(str1, str2);    // 比较字符串
stricmp(s1,s2);  // 不区分大小写
result = strncmp(str1, str2, 3);    // 比较前n个字符
strnicmp //不区分大小写
strupr(s);  //小写转大写
strlwr(s);  //大写转小写
strrev(s);  //倒置
strset(s,dest);  //s全部变成字符dest
#include <bits/stdc++.h>
using namespace std;
int main(){
  char str[] = "Hello World, Welcome to C++";
  char substr[] = "World";
  char* pos=strstr(str,substr);
  char s1[100],s2[100],s3[100];
  strcpy(s1,pos);//s1="World, Welcome to C++"
  s1[strlen(s1)]='\0';
  strcpy(s2,pos+strlen(substr));//s2=", Welcome to C++"
  s2[strlen(s2)]='\0';
  strncpy(s3,str,pos-str);//s3="Hello "
  s3[strlen(s3)]='\0';
  return 0;
}
// 查找
char* pos = strchr(str1, 'l');      // 查找字符第一次出现
pos = strrchr(str1, 'l');           // 查找字符最后一次出现
pos = strstr(str1, "llo");          // 查找子串
int num = atoi(numStr);      // 转整数
double d = atof("3.14");     // 转浮点数
long l = atol("100000");     // 转长整数

// 字符检测和转换
bool isDigit = isdigit(ch);  // 是否数字
bool isAlpha = isalpha(ch);  // 是否字母
bool isLower = islower(ch);  // 是否小写
char lowerCh = tolower(ch);  // 转小写
char upperCh = toupper(ch);  // 转大写

#include <cstring>

// 查找子串并返回剩余部分
char* findAndGetRemaining(const char* str, const char* substr) {
    char* pos = strstr(str, substr);
    if(pos != nullptr) {
        return pos + strlen(substr);  // 返回查找位置之后的字符串
    }
    return nullptr;
}

// 更安全的版本（复制到新数组）
bool findAndCopyRemaining(const char* str, const char* substr, char* result, int resultSize) {
    char* pos = strstr(str, substr);
    if(pos != nullptr) {
        char* remaining = pos + strlen(substr);
        strncpy(result, remaining, resultSize - 1);
        result[resultSize - 1] = '\0';  // 确保以null结尾
        return true;
    }
    return false;
}
二、二分模板
int binarySearchTemplate(vector<int>& nums, int target) {
    int left = 0, right = nums.size();  // 注意：右边界开区间
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        
        // 条件函数：根据具体问题修改
        if (checkCondition(nums, mid, target)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    
    return left;  // 返回满足条件的第一个位置
}
三、一个堆的实例
#include <iostream>
#include <algorithm>
#include <queue>
#include <vector>
using namespace std;

const int MAXM = 105;
const int MAXN = 2005;

int m, n;
int a[MAXM][MAXN];

// 或者更清晰的版本（使用tuple）
vector<int> mergeTwoClear(const vector<int>& A, const vector<int>& B) {
    using Element = tuple<int, int, int>; // (和, A索引, B索引)
    priority_queue<Element, vector<Element>, greater<Element>> pq;
    
    for (int i = 0; i < A.size(); i++) {
        pq.push({A[i] + B[0], i, 0});
    }
    
    vector<int> res;
    for (int k = 0; k < n && !pq.empty(); k++) {
        auto [sum, i, j] = pq.top();
        pq.pop();
        res.push_back(sum);
        
        if (j + 1 < B.size()) {
            pq.push({A[i] + B[j + 1], i, j + 1});
        }
    }
    return res;
}

int main() {
    int T;
    scanf("%d", &T);
    while (T--) {
        scanf("%d%d", &m, &n);
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                scanf("%d", &a[i][j]);
            }
            sort(a[i], a[i] + n);
        }
        
        vector<int> res(a[0], a[0] + n);
        for (int i = 1; i < m; i++) {
            vector<int> cur(a[i], a[i] + n);
            res = mergeTwoClear(res, cur);
        }
        
        for (int i = 0; i < n; i++) {
            printf("%d", res[i]);
            if (i < n - 1) printf(" ");
        }
        printf("\n");
    }
    return 0;
}


