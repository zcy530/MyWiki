## 数据结构与算法 | 总结下

#### 广度优先搜索
层次遍历

```c++
//leetcode 102 二叉树的层次遍历

vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result; //结果
        queue<TreeNode*> que;
        //循环队列是否为空，不为空从头部去一个元素
        //遍历取出来这个元素得两个子节点，然后继续放到队列中
    
        if (root != NULL) que.push(root);
        while (!que.empty()) {
            int size = que.size();
            vector<int> vec;//分别装每一层的结果
         
            for (int i = 0; i < size; i++) {
                TreeNode* node = que.front();
                que.pop();
                vec.push_back(node->val);
                if (node->left) que.push(node->left);
                if (node->right) que.push(node->right);
            }
            result.push_back(vec);
        }
        return result;
}
```

```c++
//leetcode 429 N叉树的层次遍历

vector<vector<int>> levelOrder(Node* root) {
        vector<vector<int>> result;
        queue<Node*> que;
    
        if (root != NULL) que.push(root);
        while (!que.empty()) {
            int size = que.size();
            vector<int> vec;
            
            for (int i = 0; i < size; i++) { 
                Node* node = que.front();
                que.pop();
                vec.push_back(node->val);
                for (int i = 0; i < node->children.size(); i++) { 
                    // 将节点孩子加入队列
                    if (node->children[i]) que.push(node->children[i]);
                }
            }
            result.push_back(vec);
        }
        return result;
}
```

```c++
//leetcode 199 二叉树的右视图

vector<int> rightSideView(TreeNode* root) {
        vector<int> result; //结果
        queue<TreeNode*> que;
    
        if (root != NULL) que.push(root);
        while (!que.empty()) {
            int size = que.size();
         
            for (int i = 0; i < size; i++) {
                TreeNode* node = que.front();
                que.pop();
                if(i==size-1) result.push_back(node->val);
                //判断是否遍历到单层的最后面的元素，如果是，就放进result数组中
                if (node->left) que.push(node->left);
                if (node->right) que.push(node->right);
            }
        }
        return result;
}
```

```c++
//leetcode 111 二叉树的最小深度

int minDepth(TreeNode* root) {
        int depth=0;
        if(root==NULL) return 0;
    
        queue<TreeNode*> que;
        que.push(root);
        while(!que.empty())
        {
            int size=que.size();
            depth++;//记录最小深度
            int flag=0;//还没有遇到叶子节点
            for(int i=0;i<size;i++)
            {
                TreeNode *node=que.front();
                que.pop();
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
                if(!node->right&&!node->left)
                {
                    flag=1;//当左右孩子都为空的时候，遇到了叶子节点
                    break;
                }
            }
            if(flag==1) break;
        }
        return depth;
}

```

迷宫的最短路径

```c++
#include <iostream>
#include <queue>
using namespace std;
int startx,starty;
int endx,endy;
int m,n,min=INT_MAX;
int a[m][n];//地图数组，1表示空地，2表示障碍物
int v[m][n];//访问数组，0表示未访问，1表示访问
int dx[4]={0,1,0,-1};
int dy[4]={1,0,-1,0};
struct point{
    int x;
    int y;
    int step;
}
queue<point>r;//bfs一定要用到的queue
int main(){
    cin>>m>>n;
    for(int i=1;i<=m;i++)
        for(int j=1;j<=n;j++)
            cin>>a[i][j];
    cin>>startx>>starty>>endx>>endy;
    point start;
    start.x=startx;
    start.y=starty;
    start.step=0;
    r.push(start);
    v[startx][starty]=1;
    
    while(!r.empty()){
        int x=r.front().x;
        int y=r.front().y;
        if(x==endx && y=endy){
            cout<<r.front().step<endl;
            break;
        }
        for(int k=0;k<=3;k++){
            int tx,ty;
        	tx = x+dx[k];
        	ty = y+dy[k];
        	if(a[tx][ty]=1 && v[tx][ty]==0){
            	point temp;
                temp.x=tx;
                temp.y=ty;
                temp.step=r.front().step+1;
                r.push(temp);
                v[tx][ty]=1;
        	}
        }
        r.pop();
    }
    return 0;
}
```

```c++
//POJ 3984 迷宫

#define MAXN 5
#define STARTROW 1
#define STARTCOL 1
#define ENDROW MAXN
#define ENDCOL MAXN
#define DIRECTSIZE 4
 
struct direct {
    int drow;
    int dcol;
}direct[DIRECTSIZE] = {{0, -1}, {0, 1}, {-1, 0}, {1, 0}};
 
struct node {
    int row;
    int col;
};

int maze[MAXN+2][MAXN+2];
node father[MAXN+2][MAXN+2];
queue<node> q;
 
void print_result()
{
    node path[MAXN*MAXN];
    int count = 0;
    // 逆序搜索，放入路径数组中
    path[count].row = ENDROW;
    path[count].col = ENDCOL;
    for(;;) {
        if(path[count].row == STARTROW && path[count].col == STARTCOL)
            break;
 
        path[count+1] = father[path[count].row][path[count].col];
        count++;
    }
    // 顺序输出结果
    while(count >= 0) {
        printf("(%d, %d)\n", path[count].row-1, path[count].col-1);
        count--;
    }
}
 
void bfs()
{
    node start; // 设置起始节点
    start.row = STARTROW;
    start.col = STARTCOL;
    q.push(start);
 
    while(!q.empty()) {
        node front = q.front(); q.pop();
        if (front.row == ENDROW && front.col == ENDCOL) {
            print_result();
            return;
        }
        for(int i=0; i<DIRECTSIZE; i++) {
            int nextrow = front.row + direct[i].drow;
            int nextcol = front.col + direct[i].dcol;
            if(maze[nextrow][nextcol] == 0) {
                father[nextrow][nextcol] = front;
                node v;
                v.row = nextrow;
                v.col = nextcol;
                q.push(v);
            }
        }
        maze[front.row][front.col] = 1; // 搜索过的节点不再搜索
    }
}
int main(void)
{
    int i, j;
    //把边界设为1的墙
    for(i=0; i<MAXN+2; i++) {
        maze[0][i] = 1;
        maze[MAXN+1][i] = 1;
        maze[i][0] = 1;
        maze[i][MAXN+1] = 1;
    }
 
    // 输入数据
    for(i=1; i<=MAXN; i++)
        for(j=1; j<=MAXN; j++)
            scanf("%d", &maze[i][j]);
 
    bfs(); // 开始搜索
    return 0;
}
```

#### DFS（深度优先算法）

走迷宫

```c++
#include <iostream>
using namespace std;
int p,q,m,n,min=INT_MAX;
int a[m][n];//地图数组，1表示空地，2表示障碍物
int v[m][n];//访问数组，0表示未访问，1表示访问
int dx[4]={0,1,0,-1};
int dy[4]={1,0,-1,0};
void dfs(int x,int y,int step){
    //如果到达终点
    if(x==p && y==q){
        if(step<min) min=step;
        return;
    }
    //顺时针试探
    for(int k=0;k<=3;k++){
        int tx,ty;
        tx = x+dx[k];
        ty = y+dy[k];
        if(a[tx][ty]=1 && v[tx][ty]==0){
            v[tx][ty]=1;
        	dfs(tx,ty,step+1);
        	v[tx][ty]=0;
        }
    }
    return;
}
int main(){
    int startx,starty;
    cin>>m>>n;
    for(int i=1;i<=m;i++)
        for(int j=1;j<=n;j++)
            cin>>a[i][j];
    cin>>startx>>starty>>p>>q;
    v[startx][starty]=1;
    dfs(startx,starty,0);
    cout<<min<<endl;
    return 0;
}
```

#### BigInt

大数相加

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace  std;
const int len = 510;

int main() {
    string x, y;
    while (cin>>x>>y)
    {
        int result[len] = { 0 };
        int lenx = x.length();
        int leny = y.length();
        int pos = len - 1;
        int i, j;

        int posx = lenx - 1;
        int posy = leny - 1;
        
        //开始倒着逐位相加
        while (posx>=0 && posy>=0)
            result[pos--] = (x[posx--] - '0') + (y[posy--] - '0');
            //attention！
           
        //如果两个长度不一样
       if(lenx>leny)
           while (posx>=0)
              result[pos--] = x[posx--] - '0';
       else
           while (posy >= 0)
               result[pos--] = y[posy--] - '0';

        //对result进位处理
        for (i = len - 1; i >= 0; i--) {
            if (result[i] >= 10) {
                result[i - 1] += result[i] / 10;
                result[i] = result[i] % 10;
            }
        }
   
       //找到第一个不为0的位置
        int start = 0;
        for (i = 0; i < len; i++) {
            if (result[i] != 0) break;
            start++;
        }
        
        for (i = start; i <= len-1; i++)
            cout << result[i];
        cout << endl;
    } 
    return 0;
}
```

大数相乘：计算a^n

```c++
#include <iostream>
using namespace std;
const int len = 1000;
int main() 
{
    int t;
    cin >> t;
    for (auto z = 0; z < t; z++)
    {
        int num[len] = { 0 };
        num[len - 1] = 1;
        int a, n; //a^n
        cin >> a >> n;
        for (auto i = 0; i < n; i++)
        {
            for (auto j = len - 1; j >= 0; j--)
                num[j] *= a;  //先每一位加a
            for (auto j = len - 1; j >= 0; j--)
                if (num[j] >= 10)
                {
                    num[j - 1] += num[j] / 10;
                    num[j] = num[j] % 10;
                }
        } //再考虑溢出和进位

        int start;
        for (auto i = 0; i < len; i++)
            if (num[i] == 0 && num[i + 1] != 0)
            {
                start = i + 1;
                break;
            }
        cout << "case #" << z << ":" << endl;
        for (auto i = start; i < len; i++)
            cout << num[i];
        cout.put('\n');
    }
    return 0;
}
```

计算组合数Cmn

```c++
//dp[i][j] = dp[i - 1][j] + dp[i - 1][j - 1]
//就是杨辉三角
#include <iostream>
#include <string.h>
using namespace  std;
using LL = long long;
LL dp[41][41];
int main() {
    int num;
    cin >> num;
    for (int k = 0; k < num; ++k) {
        int m, n;
        cin >> m >> n;
        memset(dp, 0, sizeof(dp));//数组每个元素置为0
        
        for (int i = 0; i <= m; ++i) {
            dp[i][0] = 1;
        }//每一行第一个元素置为1
        
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                dp[i][j] = dp[i - 1][j] + dp[i - 1][j - 1];
            }
        }
        //杨辉三角
        cout << "case #" << k << ":" << endl;
        cout << dp[m][n] << endl;
    }
    return 0;
}
```

大数相除


#### 动态规划

```c++
//leetcode70 爬楼梯
int climbStairs(int n) {
    vector<int>memo(n+1,-1);
    memo[0]=1;
    memo[1]=1;
        
    for(int i=2;i<=n;i++)
        memo[i]=memo[i-1]+memo[i-2];
    return memo[n];
}
```

```c++
//EOJ2846 统计不包含“101”字符串个数
#include <iostream>
using namespace std;
int main() {

    int strnum[21] = { 0,2,4,7 };
    for (int i = 4; i < 21; i++)
        strnum[i] = strnum[i - 1] * 2 - strnum[i - 2] + strnum[i - 3];
    int n;
    cin >> n;
    while (n != -1) {
        cout << strnum[n] << endl;
        cin >> n;
    }
    return 0;
}
```

```c++
//leetcode343 整数拆分
//将正整数n拆分为至少两个正整数的和，并使这些整数的乘积最大化
int max3(int a,int b,int c){
        return max(a,max(b,c));
}
    
int integerBreak(int n) {
    vector<int>memo( n+1 , -1);
    memo[1] = 1;
    for (int i = 2; i <= n; i++) 
    //求解memo[i]
        for (int j = 1; j < i; j++) 
        //分解成j+(i-j)
            memo[i] = max3(memo[i], j * (i - j), j * memo[i - j]);
        
    return memo[n];
}
```

```c++
//leetcode198 打家劫舍
//不能偷两间相邻的房屋的情况下，金额最大
int rob(vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;
    if (n == 1) return nums[0];

    vector<int>state(n, 0); //用于储存Si
    state[0] = nums[0];     //第一个房子
    state[1] = max(nums[0], nums[1]);  //第二个房子
    for (int i = 2; i < n; i++) 
        state[i] = max(state[i - 1], state[i - 2] + nums[i]);
    return state[n-1];
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200603213539737.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0NhaXlpaTUzMA==,size_16,color_FFFFFF,t_70)

```c++
//leetcode121 买卖股票的最佳时间
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    int minprice = int(1e9);
    int maxprofit = 0;
    for (int i = 0; i < n; i++) {
        maxprofit = max(maxprofit, prices[i] - minprice);
        minprice = min(minprice, prices[i]);
    }
    return maxprofit;
}
```

```c++
//EOJ2854 统计包含m个连续1的字符串个数
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    int n, m;
    int amt[32];//一个自变量为字符串长度的数组
    amt[0] = 0;
    cin >> n >> m;
    while (n!=-1||m!=-1){
        for (int i = 1; i <= n; i++) {
            if (i < m) amt[i] = 0;
            else if (i == m) amt[i] = 1;
            else
                amt[i] = 2 * amt[i - 1] + (int)pow(2,i - m - 1) - amt[i - m - 1];
        }
        cout << amt[n] << endl;
        cin >> n >> m;
    }
    return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200805143916617.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0NhaXlpaTUzMA==,size_16,color_FFFFFF,t_70)

```c++
//总和最大的连续数列
int maxSubArray(vector<int>& nums) {
        if(nums.size() == 0) return INT_MIN; 
        int maxSum = nums[0];
        for(int i = 1; i < nums.size(); i++){
            if(nums[i-1] >= 0)
                nums[i] += nums[i-1];
            maxSum = max(maxSum, nums[i]);
        }
        return maxSum;
}
```



#### 递归

```c++
//EOJ3054 前置波兰式求值
#include <iostream>
#include <iomanip>
using namespace std;
double cal() {
    char str[20];
    cin >> str; 
    //因为输入的时候每个字符用空格隔开的，所以每调用一次输入一次相当于
    switch (str[0]){
    	case '+':return cal() + cal(); break;
    	case '-':return cal() - cal(); break;
   		case '*':return cal() * cal(); break;
    	case '/':return cal() / cal(); break;
    	default:return atof(str);
    }
}
int main() {
    int n;
    cin >> n;
    for(int i=0;i<n;i++){
        cout << "case #" << i << ":" << endl;
        cout << setiosflags(ios::fixed) << setprecision(6) << cal() << endl;
        //保留精度的方法
    }
    return 0;
}
```