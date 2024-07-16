# 算法与数据结构
## 经典框架
### 滑动窗口

```c++
void slidingWindow(string s) {
    // 用合适的数据结构记录窗口中的数据
    unordered_map<char, int> window;
    
    int left = 0, right = 0;
    while (right < s.size()) {
        // c 是将移入窗口的字符
        char c = s[right];
        window.add(c)
        // 增大窗口
        right++;
        // 进行窗口内数据的一系列更新
        ...

        /*** debug 输出的位置 ***/
        // 注意在最终的解法代码中不要 print
        // 因为 IO 操作很耗时，可能导致超时
        printf("window: [%d, %d)\n", left, right);
        /********************/
        
        // 判断左侧窗口是否要收缩
        while (left < right && window needs shrink) {
            // d 是将移出窗口的字符
            char d = s[left];
            window.remove(d)
            // 缩小窗口
            left++;
            // 进行窗口内数据的一系列更新
            ...
        }
    }
}
```
***
### 二分法

1. **常规左闭右闭写法**
```c++
int binary_search(vector<int>& nums, int target) {
    int left = 0, right = nums.size()-1; 
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1; 
        } else if(nums[mid] == target) {
            // 直接返回
            return mid;
        }
    }
    // 直接返回
    return -1;
}
```
2. **寻找左边界**
```c++
int left_bound(vector<int>& nums, int target) {
    int left = 0, right = nums.size()-1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定左侧边界
            right = mid - 1;
        }
    }
    // 判断 target 是否存在于 nums 中
    if (left < 0 || left >= nums.size()) {
        return -1;
    }
    // 判断一下 nums[left] 是不是 target
    return nums[left] == target ? left : -1;
}
```
3. **寻找右边界**
```c++
int right_bound(vector<int>& nums, int target) {
    int left = 0, right = nums.size()-1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定右侧边界
            left = mid + 1;
        }
    }
    // 判断 target 是否存在于 nums 中
    // if (left - 1 < 0 || left - 1 >= nums.size()) {
    //     return -1;
    // }
    
    // 由于 while 的结束条件是 right == left - 1，且现在在求右边界
    // 所以用 right 替代 left - 1 更好记
    if (right < 0 || right >= nums.size()) {
        return -1;
    }
    return nums[right] == target ? right : -1;
}
```
***
### 前缀和

```c++
class NumArray {
    private:
        // 前缀和数组
        vector<int> preSum;
    
    public:
        /* 输入一个数组，构造前缀和 */
        NumArray(vector<int>& nums) {
            // preSum[0] = 0，便于计算累加和
            preSum.resize(nums.size() + 1);
            // 计算 nums 的累加和
            for (int i = 1; i < preSum.size(); i++) {
                preSum[i] = preSum[i - 1] + nums[i - 1];
            }
        }
        
        /* 查询闭区间 [left, right] 的累加和 */
        int sumRange(int left, int right) {
            return preSum[right + 1] - preSum[left];
        }
};
```
***
### 差分

```c++
// 差分数组工具类
class Difference {
    // 差分数组
    private:
        int* diff;
    
    /* 输入一个初始数组，区间操作将在这个数组上进行 */
    public:
        Difference(int* nums, int length) {
            assert(length > 0);
            diff = new int[length]();
            diff[0] = nums[0];
            for (int i = 1; i < length; i++) {
                diff[i] = nums[i] - nums[i - 1];
            }
        }

        /* 给闭区间 [i, j] 增加 val（可以是负数）*/
        void increment(int i, int j, int val) {
            diff[i] += val;
            if (j + 1 < sizeof(diff) / sizeof(diff[0])) {
                diff[j + 1] -= val;
            }
        }

        /* 返回结果数组 */
        int* result() {
            int* res = new int[sizeof(diff) / sizeof(diff[0])]();
            res[0] = diff[0];
            for (int i = 1; i < sizeof(diff) / sizeof(diff[0]); i++) {
                res[i] = res[i - 1] + diff[i];
            }
            return res;
        }
};
```
***
### 单调栈

```c++
#include <stack>
#include <vector>

std::vector<int> nextGreaterElement(std::vector<int>& nums) {
    int n = nums.size();
    // 存放答案的数组
    std::vector<int> res(n);
    std::stack<int> s; 
    // 倒着往栈里放
    for (int i = n - 1; i >= 0; i--) {
        // 若 非空 且 栈顶元素小于当前
        while (!s.empty() && s.top() <= nums[i]) {
            // 弹出栈顶
            s.pop();
        }
        // 结果为栈顶元素，末位入栈
        res[i] = s.empty() ? -1 : s.top();
        s.push(nums[i]);
    }
    return res;
}
```
***
### 二叉树遍历

1. **DFS 算法把「做选择」「撤销选择」的逻辑放在 `for` 循环外面**
```c++
void dfs(Node* root) {
    if (root == NULL) return;
    // 做选择
    printf("我已经进入节点 %p 啦\n", root);
    for (Node* child : root->children) {
        dfs(child);
    }
    // 撤销选择
    printf("我将要离开节点 %p 啦\n", root);
}
```
2. **回溯算法把「做选择」「撤销选择」的逻辑放在 `for` 循环里面**
```c++
void backtrack(Node* root) {
    if (root == NULL) return;
    for (Node* child : root->children) {
        // 做选择
        printf("我站在节点 %p 到节点 %p 的树枝上\n", root, child);
        backtrack(child);
        // 撤销选择
        printf("我将要离开节点 %p 到节点 %p 的树枝上\n", child, root);
    }
}
```
3. **输入一棵二叉树的根节点，层序遍历这棵二叉树**
```c++
void levelTraverse(TreeNode* root) {
    if (root == nullptr) return;
    queue<TreeNode*> q;
    q.push(root);

    // 从上到下遍历二叉树的每一层
    while (!q.empty()) {
        int sz = q.size();
        // 从左到右遍历每一层的每个节点
        for (int i = 0; i < sz; i++) {
            TreeNode* cur = q.front();
            q.pop();
            // 将下一层节点放入队列
            if (cur->left != nullptr) {
                q.push(cur->left);
            }
            if (cur->right != nullptr) {
                q.push(cur->right);
            }
        }
    }
}
```
***
### 回溯法

```c++
void backtrack(路径, 选择列表):  //参数
    if (满足结束条件):
        result.push_back(路径)
        return
    
    for 选择 in 选择列表:
	if (used[i] == true) continue;  //去重条件
        做选择
        backtrack(路径, 选择列表)  //递归
        回溯, 撤销选择
```
***
### DFS

```c++
void traverse(TreeNode* root) {
    traverse(root->left);
    traverse(root->right);
}

void dfs(vector<vector<int>>& grid, int i, int j, vector<vector<bool>>& visited) {
    int m = grid.size(), n = grid[0].size();
    if (i < 0 || j < 0 || i >= m || j >= n) {
        return;
    }
    if (visited[i][j]) {
        return;
    }
    visited[i][j] = true;
    dfs(grid, i - 1, j, visited); // 上
    dfs(grid, i + 1, j, visited); // 下
    dfs(grid, i, j - 1, visited); // 左
    dfs(grid, i, j + 1, visited); // 右
}
```

```c++
vector<vector<int>> dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

void dfs(vector<vector<int>>& grid, int i, int j, vector<vector<bool>>& visited) {
    int m = grid.size(), n = grid[0].size();
    if (i < 0 || j < 0 || i >= m || j >= n) {
        // 超出索引边界
        return;
    }
    if (visited[i][j]) {
        // 已遍历过 (i, j)
        return;
    }

    // 进入节点 (i, j)
    visited[i][j] = true;
    // 递归遍历上下左右的节点
    for (auto &d : dirs) {
        int next_i = i + d[0];
        int next_j = j + d[1];
        dfs(grid, next_i, next_j, visited);
    }
    // 离开节点 (i, j)
}
```
***
### BFS

```c++
int BFS(Node start, Node target) {
    queue<Node> q; 
    set<Node> visited;
    
    q.push(start); 
    visited.insert(start);

    while (!q.empty()) {
        int sz = q.size();
        for (int i = 0; i < sz; i++) {
            Node cur = q.front();
            q.pop();
            if (cur == target)
                return step;
            for (Node x : cur.adj()) {
                if (visited.count(x) == 0) {
                    q.push(x);
                    visited.insert(x);
                }
            }
        }
    }
    // 如果走到这里，说明在图中没有找到目标节点
}

```
***
### 并查集

```c++
class UF {
private:
    // 连通分量个数
    int count;
    // 存储每个节点的父节点
    int *parent;

public:
    // n 为图中节点的个数
    UF(int n) {
        this->count = n;
        parent = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
    
    // 将节点 p 和节点 q 连通
    void union_(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        
        if (rootP == rootQ)
            return;
        
        parent[rootQ] = rootP;
        // 两个连通分量合并成一个连通分量
        count--;
    }

    // 判断节点 p 和节点 q 是否连通
    bool connected(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        return rootP == rootQ;
    }

    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    // 返回图中的连通分量个数
    int count_() {
        return count;
    }
};
```
***
___
## 动态规划专篇

```python
# 自顶向下递归的动态规划
def dp(状态1, 状态2, ...):
    for 选择 in 所有可能的选择:
        # 此时的状态已经因为做了选择而改变
        result = 求最值(result, dp(状态1, 状态2, ...))
    return result

# 自底向上迭代的动态规划
# 初始化 base case
dp[0][0][...] = base case
# 进行状态转移
for 状态1 in 状态1的所有取值：
    for 状态2 in 状态2的所有取值：
        for ...
            dp[状态1][状态2][...] = 求最值(选择1，选择2...)
```
***
___
## 经典问题
### 排列/组合/子集问题

### 背包问题

### 股票买卖

***

## 备忘录

```cpp
// vector操作
*Max_element()
distance()
emplace_back()push_back()
accumulate(vec.begin(), vec.end(), 0)
```

```cpp
//string操作
reverse()
#include <algorithm>
transform(str.begin(), str.end(), str.begin(), ::tolower);
transform(str.begin(), str.end(), str.begin(), ::toupper);
```

```cpp
//优先级队列
//升序队列
priority_queue <int, vector<int>, greater<int>> q;
//降序队列
priority_queue <int, vector<int>, less<int>> q;

top // 访问队头元素
empty // 队列是否为空
size // 返回队列内元素个数
push // 插入元素到队尾 (并排序)
emplace // 原地构造一个元素并插入队列
pop // 弹出队头元素
swap // 交换内容

struct tmp {
    pair<int, int> t;
    friend bool operator < (tmp day1, tmp day2) {
        return (day1.t.second - day1.t.first) < (day2.t.second - day2.t.first);
    }
} tmp1;
```

[进制转换](https://blog.csdn.net/vir_lee/article/details/80645066)

```cpp
// 指定进制格式输出
#include <bitset>  
#include <iostream>
using namespace std;  
int main()  
{  
    cout << "35的8进制:" << std::oct << 35<< endl;  
    cout << "35的10进制" << std::dec << 35 << endl;  
    cout << "35的16进制:" << std::hex << 35 << endl;  
    cout << "35的2进制: " << bitset<8>(35) << endl;      //<8>：表示保留8位输出
    return 0;  
} 


// 任意2-36进制数转化为10进制数
int Atoi(string s,int radix)    //s是给定的radix进制字符串
{
	int ans = 0;
	for(int i = 0; i < s.size(); i++)
	{
		char t = s[i];
		if(t >= '0' && t <= '9') ans = ans * radix + t - '0';
		else ans = ans * radix + t - 'a' + 10;
	}
	return ans;
}


#include<cstdio>
int main()  
{  
    char buffer[20] = "10549stend#12";  
    char *stop;  
    int ans = strtol(buffer, &stop, 8);   //将八进制数1054转成十进制，后面均为非法字符
    printf("%d\n", ans);  
    printf("%s\n", stop);   
    return 0;
}


// 将10进制数转换为任意的n进制数，结果为char型。
string intToA(int n,int radix)    //n是待转数字，radix是指定的进制
{
	string ans = "";
	do {
		int t = n % radix;
		if(t >= 0 && t <= 9) ans += t + '0';
		else ans += t - 10 + 'a';
		n /= radix;
	} while (n != 0);	//使用do{}while（）以防止输入为0的情况
	reverse(ans.begin(), ans.end());
	return ans;	
}

#include<cstdio> 
#include<cstdlib> 
int main()  
{  
    int num = 10;  
    char str[100];  
    _itoa(num, str, 2);  //c++中一般用_itoa，用itoa也行,
    printf("%s\n", str);  
    return 0;  
}

#include<cstdio>  
int main()  
{  
	char s[100] = {0};
	sprintf(s, "%d", 123); //十进制输出产生"123"
	sprintf(s, "%4d%4d", 123, 4567); //指定宽度不足的左边补空格，产生：" 1234567"
	sprintf(s, "%8o", 123);	//八进制输出，宽度占8个位置
	sprintf(s, "%8x", 4567); //小写16 进制，宽度占8 个位置，右对齐
	sprintf(s, "%10.3f", 3.1415626); //产生：" 3.142"
	int i = 100;
	sprintf(s, "%.2f", i);	//注意这是不对的
	sprintf(s, "%.2f", (double)i);	//要按照这种方式才行
	return 0;  
}


// 使用字符串流stringstream(头文件#include<sstream>)
// 将八，十六进制转十进制。
#include<iostream>
#include<string>
#include<sstream>
using namespace std;
int main(void)
{
	string s = "20";
	int a;
	stringstream ss;
	ss << hex << s;    //以16进制读入流中
	ss >> a;        //10进制int型输出
	cout << a << endl;
    return 0;
}
//输出：32

// 将十进制转八，十六进制。
#include<cstdio>
#include<iostream>
#include<string>
#include<sstream>
using namespace std;
int main(void)
{
	string s1,s2;
	int a = 30;
	stringstream ss;
	ss << oct << a;        //10进制转成八进制读入流中，再以字符串输出
	ss >> s1;			
	cout << s1 << endl;        //输出：36
	ss.clear();		//不清空可能会出错。
	ss << hex << a;		 //10进制转成十六进制读入流中，，再以字符串输出
	ss >> s2;			
	cout << s2 << endl;        //输出：1e
    return 0;
}
```

