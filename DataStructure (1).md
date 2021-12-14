## 数据结构与算法C++

caiyii

#### Constant

```c++
INT_MIN  -2147483648
INT_MAX  2147483647
LONG_LONG_MAX
LONG_LONG_MIN
```

#### Math

```c++
#include <cmath>

int a = pow(4,2);    //4的平方
int b = pow(4,0.5);  //4的平方根
int c = sqrt(4);     //4的平方根
int c = abs(b-c);    //整数绝对值
double d = fabs(b-c);//浮点数绝对值
```

最大公约数和最小公倍数

```c++
int gcd(int a, int b) //最大公约数,辗转相除
{
    while (a%b != 0) 
    {
        int tmp = a;
        a = b;
        b = tmp % a;
    }
    return b;
}
int gcd(int a,int b)//最大公约数，递归
{
    if(b==0) return a;
    else return gcd(b,a%b);
}
//两个数互质判断：最大公约数为1
int lcm(int a, int b) //最小公倍数
{
    return a * b / gcd(a, b);
}
```

判断素数

```c++
//判断素数1
bool is_prime(long long n){
    if(n==1) return false;
    for(long long i=2;i<=sqrt(n);i++)
        if(n%i==0) return false;
    return true;
}
//判断素数2
int main() {
    const int maxnum = 100;
    int isPrime[maxnum];
    int i, x;
    for (i = 0; i < maxnum; i++) 
        isPrime[i] = 1;//把数组所有元素初始为1
    //元素的下标代表判断的数字，值为1表示素数，值为0不是
    for (x = 2; x < maxnum; x++) {
        if (isPrime[x]) 
            for (i = 2; i * x < maxnum; i++) 
                isPrime[i * x] = 0; //从2开始，把每个数的倍数都挨个排除掉
    }
    for (i = 2; i < maxnum; i++) printf("%d\t", i);
    return 0;
}
//判断素数3
int isPrime(int x, int knownPrimes[], int count) {
    int ret = 1;
    int i;
    for (i = 0; i < count; i++) {
        if (x % knownPrimes[i] == 0) {
            ret = 0;
            break;
        }
    }
    return ret;
}
int main() {
    const int number = 100;
    int knownPrimes[number] = { 2 };
    int count = 1;//Number of known primes
    int i = 3;
    while (i<number){
        if (isPrime(i, knownPrimes, count)) 
            knownPrimes[count++] = i;
        i++;
    }
    for (i = 0; i < number; i++) 
        printf("%d ", knownPrimes[i]);
    return 0;
}
```

十进制转任意进制函数

```c++
void dex_to_x(int n, int r) {//n是数，r是要转化的进制
    if (n < 0){
        printf("-"); n = -n;
    }
    if (n == 0)  printf("0");
    int c = 0, a[10000];
    while (n){
        a[c] = (n % r);
        c++;
        n /= r;
    }
    for (int i = c - 1; i >= 0; i--){
        if (a[i] >= 10)
            printf("%c", a[i] - 10 + 'A') ;
        else printf("%d",a[i]);
    }
 }

int char2int(char x) {
	if (x >= '0' && x <= '9') return x - '0';
	return x - 'A' + 10;
}
char int2char(int x) {
	if (x >= 0 && x <= 9) return x + '0';
	return x - 10 + 'A';
}
```

同余性质

```c++
//边乘边取模的思想，而不是算完再取模
//(x + y) = ((x mod m) + (ymod m))(mod m)
(x * y) % m = ((x % m) * (y % m)) % m;
(x + y) % m = ((x % m) + (y % m)) % m;
//减法表达式略有不同，考虑到减完会有负数
(x - y) % m = ((x % m) - (y % m) + m) % m;
    
//例子：求n!(mod m)
long long fac_mod(int n, long long m){
    long long ans=1;
    for(int i=1;i<=n;i++){
        ans*=i;
        ans%=m;
    }
    return ans%m;
}

//快速幂：x^y(mod m) = (x mod m)^y mod m
	//如果y是偶数，x^y(mod m) = ((x^2)^(y/2))(mod m)
	//如果y是偶数，x^y(mod m) = ((x^2)^(y/2)*x)(mod m)
long long power_int(long long a,long long b,long long c){
    long long ans=1;
    a=a%c;
    while(b>0){
        if(b%2==1)
            ans=(ans*a)%c;
        b=b/2;
        a=(a*a)%c;
    }
    return ans%c;
}
```

#### Stack

```c++
#include <stack>

stack<type>s;     //定义
s.empty();        //如果栈空则返回true, 否则返回false
s.size();         //返回栈中元素的个数
s.top();          //返回栈顶元素, 但不删除该元素
s.pop();          //弹出栈顶元素, 但不返回其值
s.push();         //将元素压入栈顶

//判断两个栈是否相等
int stackcmp(stack<int>s1,stack<int>s2)
{
	if (s1.size() != s2.size()) return 0;
	while (!s1.empty() && !s2.empty())
	{
		if (s1.top() == s2.top())
		{
			s1.pop();
			s2.pop();
		}
		else return 0;
	}
	return 1;
}
```

#### Queue

```c++
#include <queue>

queue<type>s;      //定义
q.empty();         //如果队列为空返回true, 否则返回false     
q.size();          //返回队列中元素的个数
q.front();         //返回队首元素但不删除该元素
q.pop();           //弹出队首元素但不返回其值
q.push();          //将元素压入队列
q.back();          //返回队尾元素的值但不删除该元素

```

```c++
#include <queue>

//优先级队列
priority_queue<int,vector<int>,less<int> > a;    //大根堆
priority_queue<int,vector<int>,greater<int> > a; //小顶堆
priority_queue<int> a;   //默认是大根堆
priority_queue<string> a;//字符序大的排在前面
priority_queue<pair<int, int> > a;//先比较第一个元素，第一个相等比较第二个，大的排在前

//常用操作
a.push(x);
a.empty();
a.top();
a.pop();

//对于自己定义的类型的优先级队列比较方法
struct tmp1 
{
    int x;
    tmp1(int a) {x = a;}
    bool operator<(const tmp1& a) const  //方法1：运算符重载<
    {return x < a.x;} //大顶堆
};
struct tmp2 //方法2：重写仿函数
{
    bool operator() (tmp1 a, tmp1 b) 
    {return a.x < b.x;} //大顶堆
};

int main() 
{
    tmp1 a(1),b(2),c(3);
    //方法1
    priority_queue<tmp1> d;
    //方法2
    priority_queue<tmp1, vector<tmp1>, tmp2> f;
}
```

#### Deque

```c++
#include <deque>

deque<type>c;            //定义
c.push_front('a');       //在队首加入元素
c.push_back('a');        //在队尾加入元素
c.pop_front();           //删除队首元素
c.pop_back();            //删除队尾元素
c.front();               //返回队首元素
c.back();                //返回队首元素
c.insert(pos, elem);     //在pos的位置插入元素elem
c.insert(pos, n, elem);  //在pos的位置插入n个elem
c.empty();               //判断是否为空

```

#### Vector

```c++
#include <vector>

//初始化
vector<int> a(10);        //定义了10个整型元素的向量
vector<int> a(10,1);      //定义了10个整型元素的向量,且每个元素的初值为1
vector<int> a(b);         //用b向量来创建a向量，整体复制性赋值
vector<int> a(b.begin(),b.begin+3); //定义了a值为b中第0个到第2个（共3个）元素

int b[7]={1,2,3,4,5,9,8};
vector<int> a(b,b+7);     //从数组中获得初值

//重要操作
a.assign(b.begin(), b.begin()+3); //将b的0~2个元素构成的向量赋给a
a[i];           //返回a的第i个元素
a.back();       //返回a的最后一个元素
a.front();      //返回a的第一个元素
a.size();       //返回a中元素的个数；
a.clear();      //清空a中的元素
a.empty();      //判断a是否为空，空则返回ture,不空则返回false
a.pop_back();   //删除a向量的最后一个元素
a.push_back(5); //在a的最后一个向量后插入5
a.insert(a.begin()+1,5);          //在a的第1个元素（从第0个算起）的前面插入数值5
a.insert(a.begin()+1,3,5);        //在a的第1个元素（从第0个算起）的位置插入3个5
a.erase(a.begin()+1,a.begin()+3); //删除从a.begin()+1（包括）到a.begin()+3（不包括）
a==b; //b为向量，向量的比较操作还有!=,>=,<=,>,<

```

```c++
#include <algorithm>
#include <vector>

//一些需要头文件algorithm的操作，以下a.begin()（包括它），a.end()（不包括它）
sort(a.begin(),a.end());             //对a中的元素进行从小到大排列
reverse(a.begin(),a.end());          //对a中的元素倒置，但不排列
copy(a.begin(),a.end(),b.begin()+1); //把a中的元素复制到b中，从b.begin()+1的位置（包括）开始复制，覆盖掉原有元素
find(a.begin(),a.end(),10);          //在a中的元素中查找10，若存在返回其在向量中的位置

```

#### String

```c++
#include <string>
//构造
string s1;
string s2(10,'a');
string s3(s2);//拷贝构造
const char*str="hello world";
string s4(str);
//赋值
string str,str0;
str="hello world";
str.assign("hello world");
str.assign("hello world",4);//把“hello world”前4个赋值
str.assign(s0);             //也可以直接写成s=s0;
str.assign(10,'a');
//拼接
string str='a',str0="loveyou";
str += "love you";
str.append(str0);
srt.append("love");
str1.append(5,"love");  //在后面拼接5个“love”
str.append(str0,1,3);   //从第0个位置开始，截取3个字符,包括第1个
//查找
string str="abcedfg",str2="de";
str.find(str0);         //如果找到返回起始pos=3，不存在返回string::npos(-1)
str.rfind(str2);        //从右往左查找
//其他常用操作
str.size();
str.length();
str.insert(1,"111");    //在位置1（前面）插入字符
str.erase(1,3);         //从位置1（包括1）删除3个字符
str.replace(1,3,"111"); //从第1个位置开始（包括），替换三个字符
str.compare(str0);      //0:相等 -1:str<str0  1:str>str0
str.substr(1,3);        //从位置1（包括）截取3个字符
ch=toupper(ch);
ch=tolower(ch);
//string与不同类型数据的转换
int i = atoi(s.c_str());        //sting转int
long long i = atoll(s.c_str()); //sting转long long
string s = to_string(i);        //int转string
char t[maxl];      //char*转string
strcpy(t,"abcd");
string s=t;
char t[maxl];      //string转char*
t=s.c_str();
//string输入
getline(cin,str);  //可以有空格
cin>>str;          //不读入'\n'和' '
//string迭代器
reverse(s.begin(),s.end());//反转
    
```

```c++
#include <string>
#include <algorithm>

//全部转换为大写/小写
transform(str.begin(), str.end(), str.begin(), ::toupper); 
transform(str.begin(), str.end(), str.begin(), ::tolower);
```

#### Set

```c++
#include <set>

//初始化
set<int>s;
set<int>s2(s);  
set<int>s2(s.begin(),s.end())
   
int myints[]= {10,20,30,40,50};
set<int>s(myints,myints+5); 

//常用操作
s.begin();            // 返回指向第一个元素的迭代器
s.end();              // 返回指向迭代器的最末尾处（即最后一个元素的下一个位置）
s.clear();            // 清除所有元素
s.count();            // 返回某个值元素的个数
s.empty();            // 如果集合为空，返回true
s.insert(x);          //向set中插入元素
```

#### Sort

```c++
#include <algorithm>
//数组排序
int a[11]={0,1,2,3,4,5,6,7,8,9,10};
sort(a,a+11);
sort(a+4,a+11);
//倒序
bool cmp(int a,int b)
{
    return a>b;
}
sort(a,a+11，cmp);
//重载cmp函数例子
bool cmp(string a,string b)
{
    return a>b;
}
bool cmp(struct Dog a,struct Dog b)
{
    if(a.age==b.age){
        return a.weight<b.weight;//体重升序
    }
    else return a.age>b.age;//年龄降序
}
```

#### Search

```c++
//二分查找，版本1
int BinarySearch1(int a[], int value, int n)
{
    int low, high, mid;
    low = 0;
    high = n-1;
    while(low<=high)
    {
        mid = (low+high)/2;
        if(a[mid]==value)
            return mid;
        if(a[mid]>value)
            high = mid-1;
        if(a[mid]<value)
            low = mid+1;
    }
    return -1;
}
 
//二分查找，递归版本
int BinarySearch2(int a[], int value, int low, int high)
{
    int mid = low+(high-low)/2;
    if(a[mid]==value)
        return mid;
    if(a[mid]>value)
        return BinarySearch2(a, value, low, mid-1);
    if(a[mid]<value)
        return BinarySearch2(a, value, mid+1, high);
}
```

#### Tree

层次遍历

```c++
//二叉树
struct TreeNode {
     int val;
     TreeNode *left;
     TreeNode *right;
     TreeNode() : val(0), left(nullptr), right(nullptr) {}
     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

//N叉树
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}
    Node(int _val) {val = _val;}
    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};

```