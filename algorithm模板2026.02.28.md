![ICPCLogo](C:\Users\ztx\Pictures\Camera Roll\ICPCLogo.png)

  <div style="border-top: 10px solid black; margin: 10px auto; width: 65%;"></div>



<div style="text-align: center; font-size: 35px; font-family: 'Microsoft YaHei', sans-serif; font-weight: bold;">
𝔅𝔩𝔲𝔢𝔶𝔢𝔰_𝔳𝔟𝔰‘s XCPC
</div>



<div style="text-align: center; font-size: 35px; font-family: 'Microsoft YaHei', sans-serif; font-weight: bold;">
Algorithm Template(&#8544)
</div>














<div style="text-align: center; font-size: 30px; font-family: 'Microsoft YaHei', sans-serif; font-weight: bold;">
v1.2 2026.02.28
</div>









<div style="text-align: center; font-size: 28px; font-family: 'Microsoft YaHei', sans-serif; font-weight: bold;">
Author : Blueyes_vbs
</div>

<div style="page-break-after: always;"></div>

<div class="汉仪瘦金体"> <h2 style="text-align:center; font-size: 50px;"> 目录</div>

#### 1 [数据结构](# 1 数据结构) ...... 4

- 1.1 树状数组
- 1.2 线段树
- 1.3 主席树 
- 1.4 Trie树
- 1.5 ST表
- 1.6 区间gcd
- 1.7 扫描线
- 1.8 线性基
- 1.9 对顶堆
- 1.10 笛卡尔树

#### 2 [杂类](# 2 杂类) ...... 11

- 2.0 头文件
- 2.1 对拍
  - 2.1.1 checker.cpp
- 2.2 二分
- 2.3 随机数
- 2.4 快速幂及快读快写
- 2.5 Lambda函数
- 2.6 STL
- 2.7 全排列函数 
- 2.8 前缀和差分
- 2.9 组合数
- 2.10 bitset


#### 3 [字符串](# 3 字符串) ...... 20

- 3.1 KMP1
- 3.2 KMP2
- 3.3 回文串个数
- 3.4 字符串哈希

#### 4 [搜索与图论](# 4 搜索与图论) ...... 23

- 4.1 Dijkstra
- 4.2 分层图最短路
- 4.3 Floyd 
- 4.4 Kruskal
- 4.5 Prim
- 4.6 SPFA
- 4.7 拓扑排序
- 4.8 三类并查集
- 4.9 树的直径
- 4.10 最近公共祖先
- 4.11 SCC(强连通分量)
- 4.12 IDDFS
- 4.13 双向bfs
- 4.14 Astar
- 4.15 环的大小
- 4.16 双向dfs
- 4.17 IDAstar
- 4.18 dfs剪枝
- 4.19 ksm优化最短路
- 4.20 最小环（floyd）
- 4.21 最小环（dfs）
- 4.22 eDCC(边双连通分量)
- 4.23 vDCC(点双连通分量)
- 4.24 匈牙利算法
- 4.25 欧拉回路(路径)

#### 5 [数论](# 5 数论) ...... 41

- 5.1 高精度
- 5.2 线性筛 
- 5.3 裴蜀定理
- 5.4 扩展欧几里得(exgcd)
- 5.5 gcd
- 5.6 数论分块
- 5.7 约数个数
- 5.8 试除法
- 5.9 规律
- 5.10 逆序对
- 5.11 莫队
- 5.12 FFT
- 5.13 高斯消元
- 5.14 SG函数

#### 6 [DP大类](# 6 DP大类) ...... 52

- 6.1 多重背包

- 6.2 区间dp

- 6.3 最长上升子序列（贪心优化）

- 6.4 最长公共子序列（贪心优化）

- 6.5 最长公共上升子序列

- 6.6 状压dp

- 6.7 期望dp

- 6.8 树形dp

- 6.9 数位dp

- 6.10 单调队列优化dp

- 6.11 斜率优化dp

- 6.12 差值背包

- 6.13 换根dp

- 6.14 矩阵快速幂优化dp

#### 7 [计算几何](# 7 计算几何) ...... 64

- 7.1 凸包

<div style="page-break-after: always;"></div>

# 1 数据结构

## 1.1 树状数组

```cpp
#include<iostream>
#include<algorithm>
using namespace std;
const int MAXN=1e5+10;
int a[MAXN];//原数组
int b[MAXN];//树状数组，维护原数组的，单点修改，区间查询

int lowbit(int x){
    return x&-x;//找到x最右边的1
}

int n;//数组实际大小
void add(int x,int num){
    for(int i=x;i<=n;i+=lowbit(i)){
        b[i]+=num;
    }
}

int sum(int r){
    int ans=0;
    for(int i=r;i>0;i-=lowbit(i)){
        ans+=b[i];
    }
    return ans;
}

int query(int l,int r){
    return sum(r)-sum(l-1);
}

void init(int n){
    for(int i=1;i<=n;i++){
        add(i,a[i]);
    }
}
//**********************************************************************************************
//区间修改，区间查询
int Tree1[MAXN];//维护D[i]的树状数组
int Tree2[MAXN];//维护(i-1)*D[i]的树状数组
void add(int Tree[],int x,int num){
    for(int i=x;i<=n;i+=lowbit(i)){
        Tree[i]+=num;
    }
}

void add1(int l,int r,int num){//区间修改
    add(Tree1,l,num);
    add(Tree1,r+1,-num);
    add(Tree2,l,(l-1)*num);
    add(Tree2,r+1,-r*num);
}
int sum(int Tree[],int r){
    int ans=0;
    for(int i=r;i>0;i-=lowbit(i)){
        ans+=Tree[i];
    }
    return ans;
}
int query1(int l,int r){//区间查询
    return r*sum(Tree1,r)-(l-1)*sum(Tree1,l-1)-(sum(Tree2,r)-sum(Tree2,l-1));
}
void init1(int n){
    for(int i=1;i<=n;i++){
        add1(i,i,a[i]);
    }
}

signed main(){
    n=5;
    for(int i=1;i<=5;i++){
        cin>>a[i];
    }
    init1(5);
    add(1,2,5);
    cout<<query1(1,5)<<" ";
    return 0;
}
```

## 1.2 线段树

```cpp
//范围修改，范围查询
#include<iostream>
using namespace std;
#define ll long long
const int N=1e6+1;
int n,m;
int w[N];

struct Node{
    int l,r;
    ll sum;             //sum要用ll存储，防止爆掉int
    ll lazy;
}tree[N<<2];

void pushup(int u){      //求父节点的和
    tree[u].sum = tree[u<<1].sum + tree[u<<1|1].sum;
}

void pushdown(int u){    //将懒惰标记往下传
    ll lazy = tree[u].lazy;
    if(lazy){
        tree[u<<1].lazy += lazy;
        tree[u<<1|1].lazy += lazy;
        tree[u<<1].sum += (tree[u<<1].r - tree[u<<1].l + 1) * lazy;
        tree[u<<1|1].sum += (tree[u<<1|1].r - tree[u<<1|1].l + 1) * lazy;
        tree[u].lazy = 0;   //父节点懒惰标记传完之后一定要将父节点的懒惰标记重置为0
    }
}

void build(int u,int l,int r){           //建线段树
    if(l == r)  tree[u] = {l, r, w[r]};
    else{
        tree[u] = {l, r};
        int mid = (l+r) >> 1;
        build(u<<1, l, mid), build(u<<1|1, mid+1, r);
        pushup(u);
    }
}

ll query(int u,int l,int r){             //求区间和
    if(l <= tree[u].l && tree[u].r <= r)    return tree[u].sum;
    else{
        pushdown(u);                    //如果父节点没有被完全覆盖，此时要记得将懒惰标记往下传。
        int mid = (tree[u].l + tree[u].r) >> 1;
        ll sum = 0;
        if(l <= mid)  sum += query(u<<1, l, r);
        if(r > mid)   sum += query(u<<1|1, l, r);
        return sum;
    }
}

void update(int u,int l,int r,int d){    //区间修改
    if(l <= tree[u].l && tree[u].r <= r){          //完全覆盖父节点，则标记一下懒惰标记即可，先不着急往下传，求和需要用到时再往下传
        tree[u].lazy += d;
        tree[u].sum += (tree[u].r - tree[u].l + 1) * d;
    }
    else{
        pushdown(u);
        int mid = tree[u].l + tree[u].r >> 1;
        if(l <= mid)  update(u<<1, l, r, d);
        if(r > mid)  update(u<<1|1, l, r, d);
        pushup(u);
    }
}

signed main(){
    cin>>n>>m;
    for(int i = 1; i <= n; i++){
        cin>>w[i];
    }
    build(1, 1, n);
    // cout<<tree[5].lazy<<endl;
    for(int i = 0; i<m; i++){
        int op = 1;
        cin>>op;
        if(op == 1){
            int l, r, d;
            cin>>l>>r>>d;
            update(1, l, r, d);
        }
        else{
            int l, r;
            cin>>l>>r;
            cout<<query(1, l ,r)<<endl;
        }
    }
    return 0;
}
```

## 1.3 主席树

```cpp
#include<bits/stdc++.h>
const int MAXN = 1e5 + 10;
using namespace std;

class segTree{
public:
    struct node{
        int l, r;
        int sum;
    };

    int n;
    int cnt;
    vector<node>t;

    segTree() = default;
    segTree(int _n) : n(_n){
        assert(n > 0);
        cnt = 0;
        t.resize(n << 5);
    }

    void clear(){
        cnt = 0;
        fill(t.begin(), t.end(), node());
    }

    int build(int l ,int r){
        int u = ++cnt;
        if(l >= r) return u;
        int mid = (l + r) >> 1;
        t[u].l = build(l, mid);
        t[u].r = build(mid+1, r);
        return u;
    }

    int update(int pre, int l, int r, int x){
        int u = ++cnt;
        t[u] = t[pre];
        t[u].sum = t[pre].sum + 1;
        if(l >= r) return u;

        int mid = (l + r) >> 1;
        if(x <= mid) t[u].l = update(t[pre].l, l, mid, x);
        else t[u].r = update(t[pre].r, mid + 1, r, x);

        return u;
    }

    int kth(int u, int v, int l, int r, int k){
        if(l == r) return l;
        int cnt1 = t[t[v].l].sum - t[t[u].l].sum;
        int mid = (l + r) >> 1;

        if(k <= cnt1) return kth(t[u].l, t[v].l, l, mid, k);
        else return kth(t[u].r, t[v].r, mid+1, r, k-cnt1);
    }
};

int n, m, root[MAXN], a[MAXN], b[MAXN];
segTree tree(MAXN);

signed main(){
    map<int, int>mp;
    cin >> n >> m;
    for(int i = 1; i <= n; i++) cin >> a[i], mp[a[i]] = 0;
    int cnt = 0;
    for(auto &[x, y] : mp){
        y = ++cnt, b[cnt] = x;
    }

    for(int i = 1; i <= n; i++){
        root[i] = tree.update(root[i-1], 1, cnt, mp[a[i]]);
    }
    while(m--){
        int i, j, k;
        cin >> i >> j >> k;
        int idx = tree.kth(root[i-1], root[j], 1, cnt, k);
        cout << b[idx] << endl; 
    }
    return 0;
}
```

## 1.4 Trie树

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N = 2e5 + 10;
int son[N][26], cnt[N], idx;
char str[N];

void insert(string& s)
{
    int p = 0;  //类似指针，指向当前节点
    for(int i = 0; i < s.size(); i++)
    {
        int u = s[i] - 'a'; //将字母转化为数字
        if(!son[p][u]) son[p][u] = ++idx;   //该节点不存在，创建节点
        p = son[p][u];  //使“p指针”指向下一个节点
    }
    cnt[p]++;  //结束时的标记，也是记录以此节点结束的字符串个数
}

int query(string& s)
{
    int p = 0;
    for(int i = 0; i < s.size(); i++)
    {
        int u = s[i] - 'a';
        if(!son[p][u]) return 0;  //该节点不存在，即该字符串不存在
        p = son[p][u]; 
    }
    return cnt[p];  //返回字符串出现的次数
}

int query1(string& s)
{
    int p = 0, ans = 0;
    for(int i = 0; i < s.size(); i++)
    {
        int u = s[i] - 'a';
        if(!son[p][u]) break;  //该节点不存在，即该字符串不存在
        p = son[p][u];
        ans += cnt[p]; 
    }
    return ans;  //返回该字符串的前缀出现的次数
}

signed main(){
    int n, m;
    cin >> n >> m;
    string s;
    for(int i = 1; i <= n; i++){
        cin >> s;
        insert(s);
    }
    for(int i = 1; i <= m; i++){
        cin >> s;
        cout << query1(s) << endl;
    }
    return 0;
}
```

## 1.5 ST表

```cpp
#include<bits/stdc++.h>
const int MAXN=5e5+10;
using namespace std;

int n;
//stmax[i][j]表示，从i开始数2^j个数，里面最大的数， stmin相同, log2[i]表示log以2为底i的值取整
int arr[MAXN],LOG2[MAXN],stmax[MAXN][19],stmin[MAXN][19];

void build(){
    LOG2[0] = -1;
    for(int i = 1;i <= n; i++){
        LOG2[i] = LOG2[i>>1]+1;
        stmax[i][0] = arr[i];
        stmin[i][0] = arr[i];
    }
    for(int p = 1; p <= LOG2[n]; p++){
        for(int i=1; i+(1<<p)-1 <= n; i++){
            stmax[i][p] = max(stmax[i][p-1], stmax[i + (1<<p-1)][p-1]);
            stmin[i][p] = min(stmin[i][p-1], stmin[i + (1<<p-1)][p-1]);
        }
    }
}

//求区间最值
int query(int l,int r){
    int p=LOG2[r-l+1];
    int a=max(stmax[l][p],stmax[r-(1<<p)+1][p]);//区间最大值
    // int b=min(stmin[l][p],stmin[r-(1<<p)+1][p]);//区间最小值
    return a;//或者return b;
}
signed main(){
    int n;
    cin>>n;
    for(int i=1; i<=n; i++) cin>>arr[i];
    build();
    return 0;
}
```

## 1.6 区间gcd

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 5e5 + 10;
const int M = 64;
const int mod = 998244353;
using PI3 = array<int, 3>;

// 区间gcd定理
// 令b[i] = a[i] - a[i - 1], i >= 2
// gcd(a[l], a[l+1],..., a[r]) = gcd(a[l], b[l + 1],..., b[r]);
int n, m;
int a[N],  b[N];

struct node{
    int l, r;
    int sum; // 差分维护a[i]
    int g; // 维护b[i]的区间gcd
}tree[N << 2]; 

void pushup(int u){
    tree[u].sum = tree[u << 1].sum + tree[u << 1 | 1].sum;
    tree[u].g = gcd(tree[u << 1].g, tree[u << 1 | 1].g);
}

void build(int u, int l, int r){
    if(l == r) tree[u] = {l, r, b[l], b[l]};
    else{
        tree[u] = {l, r};
        int mid = l + r >> 1;
        build(u << 1, l, mid), build(u << 1 | 1, mid + 1, r);
        pushup(u);
    }
}

void update(int u, int x, int d){
    if(tree[u].l == x && tree[u].r == x){
        tree[u].sum += d;
        tree[u].g += d;
    }
    else{
        int mid = tree[u].l + tree[u].r >> 1;
        if(x <= mid) update(u << 1, x, d);
        if(mid < x) update(u << 1 | 1, x, d);
        pushup(u);
    }
}

// 还可以直接query返回node
int query_gcd(int u, int l, int r){
    if(l <= tree[u].l && tree[u].r <= r) return tree[u].g;
    else{
        int mid = tree[u].l + tree[u].r >> 1;
        int g = 0;
        if(l <= mid) g = gcd(g, query_gcd(u << 1, l, r));
        if(mid < r) g = gcd(g, query_gcd(u << 1 | 1, l, r));
        return g;
    }
}

int query_sum(int u, int l, int r){
    if(l <= tree[u].l && tree[u].r <= r) return tree[u].sum;
    else{
        int mid = tree[u].l + tree[u].r >> 1;
        int sum = 0;
        if(l <= mid) sum += query_sum(u << 1, l, r);
        if(mid < r) sum += query_sum(u << 1 | 1, l, r);
        return sum;
    }
}

void solve(){
    cin >> n >> m;
    for(int i = 1; i <= n; i++){
        cin >> a[i];
        b[i] = a[i] - a[i - 1];
    }

    build(1, 1, n);
    for(int i = 1; i <= m; i++){
        char op; int l, r, d;
        cin >> op;
        if(op == 'C'){ // 区间修改
            cin >> l >> r >> d;
            update(1, l, d);
            if(r + 1 <= n) update(1, r + 1, -d);
        }
        else{ // 区间查询
            cin >> l >> r;
            if(l == r) cout << query_sum(1, 1, l) << endl;
            else{
                cout << gcd(query_sum(1, 1, l), query_gcd(1, l + 1, r)) << endl;
            }
        }
    }
}

signed main(){
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 1.7 扫描线

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 1e5 + 10;
const int M = 64;
const int mod = 998244353;
using PI3 = array<int, 3>;

int n;
// 求矩形面积并
// 以垂直线扫描x轴, 线段树维护y轴的长度
struct Segment{
    double x, y1, y2;
    int op;
    bool operator < (const Segment &t) const {
        return x < t.x;
    }
}seg[N << 1];

struct node{
    int l, r; // 每个点代表的是ys[i]~ys[i + 1]的一段线段
    int cnt;
    double len;
}tree[N << 3]; 

vector<double>ys;

int get(double y1){ // 离散化
    return lower_bound(ys.begin(), ys.end(), y1) - ys.begin();
}

void pushup(int u){ // 只查询根节点信息和pushup的写法导致不需要懒标记
    if(tree[u].cnt) tree[u].len = ys[tree[u].r + 1] - ys[tree[u].l];
    else if(tree[u].l != tree[u].r){
        tree[u].len = tree[u << 1].len + tree[u << 1 | 1].len;
    }
    else tree[u].len = 0;
}

void build(int u, int l, int r){
    if(l == r) tree[u] = {l, r, 0, 0};
    else{
        tree[u] = {l, r, 0, 0};
        int mid = l + r >> 1;
        build(u << 1, l, mid), build(u << 1 | 1, mid + 1, r);
        pushup(u);
    }
}

void update(int u, int l, int r, int d){
    if(l <= tree[u].l && tree[u].r <= r){
        tree[u].cnt += d;
        pushup(u);
    }
    else{
        int mid = tree[u].l + tree[u].r >> 1;
        if(l <= mid) update(u << 1, l, r, d);
        if(mid < r) update(u << 1 | 1, l, r, d);
        pushup(u);
    }
}


void solve(int t){
    ys.clear();
    
    for(int i = 1; i <= n; i++){
        double x1, y1, x2, y2; cin >> x1 >> y1 >> x2 >> y2;
        seg[2 * i - 1] = {x1, y1, y2, 1};
        seg[2 * i] = {x2, y1, y2, -1};
        ys.push_back(y1), ys.push_back(y2);
    }   

    sort(ys.begin(), ys.end());
    ys.erase(unique(ys.begin(), ys.end()), ys.end());
    build(1, 0, ys.size() - 2);

    sort(seg + 1, seg + 2 * n + 1);
    double ans = 0;
    for(int i = 1; i <= 2 * n; i++){
        if(i > 1){
            ans += tree[1].len * (seg[i].x - seg[i - 1].x);
        }
        update(1, get(seg[i].y1), get(seg[i].y2) - 1, seg[i].op);
    }
    cout << "Test case #" << t << endl;
    cout << "Total explored area: ";
    cout << fixed << setprecision(2) << ans << endl << endl;
}

signed main(){
    int T = 0;
    // cin >> T;
    while(cin >> n && n){
        solve(++T);
    }
    return 0;
}
```

## 1.8 线性基

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 1e5 + 10;
const int M = 32;
const int mod = 998244353;
using PI3 = array<int, 3>;

int n;
int a[N], b[N];
int d[M];
bitset<N>path[M], ans;
// path[i]是路径还原

void insert(int x, int pos){
    int mask = 0;
    for(int i = M - 1; i >= 0; i--){
        if(!(x >> i & 1)) continue;
        if(!d[i]){
            d[i] = x;
            path[i].reset();
            path[i].set(pos);
            for(int j = M - 1; j >= 0; j--){
                if(mask >> j & 1) path[i] ^= path[j];
            } 
            return ;
        }
        x ^= d[i];
        mask ^= (1ll << i);
    }
}

bool can(int x){ // 判断能不能组合异或成x这个数
    for(int i = M - 1; i >= 0; i--){
        if(x >> i & 1){
            if(d[i]) x ^= d[i], ans ^= path[i];
        }
    }
    return x == 0;
}

int qmax(){
    int ans = 0;
    for(int i = M - 1; i >= 0; i--) ans = max(ans, ans ^ d[i]);
    return ans;
}

int qmin(){
    for(int i = 0; i < M; i++){
        if(!d[i]) return d[i];
    }
}

// 时间复杂度O(N * M + M * M * N / 64)
void solve(){
    cin >> n;
    ans.reset();
    for(int i = 0; i < M; i++){
        d[i] = 0;
        path[i].reset();
    }

    int tar = 0;
    for(int i = 1; i <= n; i++) cin >> a[i], tar ^= a[i];
    for(int i = 1; i <= n; i++) cin >> b[i], insert(a[i] ^ b[i], i);
    
    if(!can(tar)) cout << -1 << endl;
    else{
        for(int i = 1; i <= n; i++){
            if(ans.test(i)) cout << b[i] << " ";
            else cout << a[i] << " ";
        }
        cout << endl;
    }
}

signed main(){
    IOS();
    int T = 1;
    cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 1.9 对顶堆

```cpp
// 动态维护中位数
priority_queue<int>h1;
priority_queue<int, vector<int>, greater<>>h2;
vector<int>p; // 求n为奇数时候的中位数
for(int i = 1; i <= n; i++){
    int x; cin >> x;
    if(h2.size() && x > h2.top()) h2.push(x);
    else h1.push(x);
    while(h1.size() > i / 2){
        auto u = h1.top();
        h2.push(u);
        h1.pop();
    }
    while(h2.size() > (i + 1) /2){
        auto u = h2.top();
        h1.push(u);
        h2.pop();
    }

    if(i&1) p.push_back(h2.top());
}
```

## 1.10 笛卡尔树

```cpp
int a[N];
int l[N], r[N];
int root;

// 维护一个大根堆的笛卡尔树(是一个二叉树, 每个结点权值都大于它的左右结点), 时间复杂度O(n)
// lca(u, v)的权值就是区间[u, v]的最值
// 大根堆的树, 根到叶子结点的路径就是先减后增的
void build(){
    fill(l, l + n + 1, 0);
    fill(r, r + n + 1, 0);
    stack<int>stk;
    // 利用栈维护, 大根堆就是小压大, 栈底就是根结点
    for(int i = 1; i <= n; i++){
        int v = 0;
        while(stk.size() && a[stk.top()] < a[i]){
            v = stk.top();
            stk.pop();
        }
        if(v) l[i] = v;
        if(stk.size()) r[stk.top()] = i;
        stk.push(i);
    }
    while(stk.size()) root = stk.top(), stk.pop();
}

int mx;
// 求最深深度
void dfs(int u, int dep){
    mx = max(mx, dep);
    // cout << u << " " << l[u] << " " << r[u] << endl;
    if(l[u]) dfs(l[u], dep + 1);
    if(r[u]) dfs(r[u], dep + 1);
}
```



<div style="page-break-after: always;"></div>

# 2 杂类

## 2.0 头文件

```cpp
#include<iostream>
#include<cstdio>
#include<algorithm>
#define _USE_MATH_DEFINES 
#include<cmath>
#include<cstdlib>
#include<cstring>
#include<vector>
#include<set>
#include<map>
#include<stack>
#include<queue>
#include<unordered_map>
#include<unordered_set>
#include<bitset>
#include<ctime>
#include<random>
#include<array>
#include<list>
#include<iomanip>
#include<fstream>
#include<ostream>
#include<sstream>
#define PI M_PI
#define read(a) {char c;while((c=getchar())>47) a=a*10+(c^48);}
using i64 = long long;
using i128 = __int128_t;
using namespace std;

typedef long long LL;
typedef pair<LL, LL> PLL;
typedef pair<int, int> PII;
typedef unsigned long long ULL;
typedef pair<ULL, ULL> PUU;
typedef pair<double, double> PDD;

//交互题记得注释掉
#define endl "\n"
#define double long double
#define big_heap(T) priority_queue<T>
#define small_heap(T) priority_queue<T, vector<T>, greater<>>
#define PI M_PI
#define F1 first
#define F2 second
#define read(a) {char c;while((c=getchar())>47) a=a*10+(c^48);}
const int MAXN = 2e6 + 10;
const int N = 2e5 + 10;
const int M = 2e5 + 10;
const double EXP = 1e-8;
const int mod = 998244353;
const int INF = 0x3f3f3f3f;
const LL LNF = 0x3f3f3f3f3f3f3f3f;
void IOS(){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
}
```

## 2.1 对拍

### 2.1.1checker.cpp

```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;
const int T = 100;

void IOS(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
}

int randint(int min, int max){
    static random_device rd;
    static mt19937 gen(rd());
    uniform_int_distribution<long long>dis(min, max);
    return dis(gen);
}

void DATA(){
    FILE *fp = fopen("F.in", "w");
    int n = randint(1, 10), q = randint(1, 10);
    fprintf(fp, "%d %d\n", n, q);
    for(int i = 1; i <= n; i++){
        int x = randint(1, 10);
        fprintf(fp, "%d ", x);
    }
    fclose(fp);
}

signed main(){
    for(int i = 1; i <= 1e5; i++){
        DATA();
        system("bf.exe < F.in > bf.out");
        system("std.exe < F.in > std.out");
        if(system("fc bf.out std.out 1>nul")){
            printf("WA at test %d\n", i);
            system("pause");
        }
        printf("AC!\n");
    }
    return 0;
}
```

## 2.2 二分

```cpp
#include<iostream>
using namespace std;
int l,r;
//判断是否满足条件
bool check(int mid){

}
int main(){
    int ans=0;
    //往左侧找
    while(l<=r){
        int mid=l+r>>1;
        if(check(mid)){
            ans=mid;
            r=mid-1;
        }
        else l=mid+1;
    }
    //往右侧找
    while(l<=r){
        int mid=l+r>>1;
        if(check(mid)){
            ans=mid;
            l=mid+1;
        }
        else r=mid-1;

    }
    cout<<ans;
}
```

## 2.3 随机数

```cpp
int randint(int min, int max) {//强大的随机数生成器，需要头文件#include<random>
    static random_device rd;  // 用于生成种子
    static mt19937 gen(rd()); // 使用 Mersenne Twister 生成器
    uniform_int_distribution<long long> dis(min, max);
    return dis(gen);
}
```

## 2.4 ksm及快读快写

```cpp
#include<bits/stdc++.h>
using namespace std;
#define MOD 998244353

// 预处理1~n的逆元
// inv[1] = 1;
// for(int i = 2;i <= n;i++)  inv[i] = (mod -  mod / i) * inv[mod % i] % mod;

long long fasterpower(long long base,long long power){
    long long result=1;
    while(power){
        if(power&1){
        result=result*base%MOD;
        }
        power>>=1;
        base=base*base%MOD;
    }
    return result;
}

inline void print(__int128_t n){
    if(n<0) cout << -1, n *= (-1);
    if(n>9) print(n/10);
    int num = n%10;
    cout << num;
}

__int128_t read(){
    __int128_t x = 0;
    int f = 1;
    char ch = getchar();
    if(ch == '-') f = -1, ch = getchar();
    while(ch >= '0' && ch <= '9'){
        x = x*10 + ch - '0';
        ch = getchar();
    }
    return x*f;
}

__int128_t ksm(__int128_t base, __int128_t power){
    __int128_t ans=1;
    while(power){
        if(power&1) ans*=base;
        power>>=1;
        base*=base;
    }
    return ans;
}

//求逆元, 用费马小定理, a^(p-1) ≡ 1 (mod p)
//使用条件 p为质数, gcd(a, p) = 1, 
//那么 a的逆等于 a^(p-2)

signed main(){
    __int128_t x = read();
    print(x);
    return 0;
}
```

## 2.5 Lambda函数

```cpp
/*
[capture](parameters) -> return_type {
    // 函数体
};

capture：捕获列表，用于捕获外部变量。可以是=（按值捕获所有外部变量）、&（按引用捕获所有外部变量），或者指定具体的变量。
parameters：参数列表，与普通函数的参数列表类似。
return_type：返回类型，可以省略，编译器会自动推导。
函数体：Lambda函数的实现代码。

eg1:
// 定义一个Lambda函数，接受两个int参数，返回它们的和
auto add = [](int a, int b) -> int {
    return a + b;
};

int result = add(3, 4);  // 调用Lambda函数
std::cout << "Result: " << result << std::endl;  // 输出: Result: 7
```

## 2.6 STL

```cpp
#include<bits/stdc++.h>
#include<iomanip>
#define PII pair<int, int>
using namespace std;
// cout<<setiosflags(ios::fixed)<<setprecision(n+i)<<PI<<endl;保留小数点后几位输出
//cout<<fixed<<setprecision(i)<<endl;
// string::npos
// (1LL << i), 位运算的时候务必要用lLL或者1ll, 不然会爆int
// fprintf(fp, "%s\n", s.c_str()); c语言输出string要用string内置函数c_str()

// Lambda函数
function<void(ll)> dfs = [&](ll u) -> void {
    if (vis.count(u)) return;
    vis.insert(u);
    for (ll v : adj[u]) dfs(v);
};

// 使用仿函数排序
struct cmp{
    bool operator() (const PII&x, const PII&y)const{
        return (x.F2 == y.F2 ? x.F1 > y.F1 : x.F2 > y.F2);
    }  
};
set<PII, cmp>st;

//stringstream用法
std::string str = "one two three four";
std::stringstream ss(str);
std::string word;
while (ss >> word) {
    std::cout << word << std::endl;
}

// vector a(n, 0); n个元素, 初始值为0
// 初始化vector的行列
vector prea(n+1, vector<int>(32)), preb = prea, pre = prea;
//设置行数
vector<vector<int>>a;
a.resize(n);
//vector去重
sort(a.begin(), a.end());
a.erase(unique(a.begin(), a.end()), a.end());

// 三角函数sin(), 反三角函数asin()
```

## 2.7 全排列函数

```cpp
#include<bits/stdc++.h>
using namespace std;

signed main(){
    int n;
    vector<int> a(n + 1);
    for(int i = 1; i <= n; i++) cin >> a[i];
    sort(a.begin(), a.end());//全排列函数必要条件

    do{
        //内容
    }while(next_permutation(a.begin(), a.end()));
    return 0;
}
```

## 2.8 前缀和差分

```cpp
#include <bits/stdc++.h>
using namespace std;
const int MAXN=1e4+10;

int diff[MAXN][MAXN];//二维差分数组
int maxn=0;
void solve(){
    int x1,y1,x2,y2;
    cin>>x1>>y1>>x2>>y2;
    x1+=2;y1+=2;x2++;y2++;
    maxn=max(max(max(x1,x2),max(y1,y2)),maxn);
    //区间修改
    diff[x1][y1]++;
    diff[x1][y2+1]--;
    diff[x2+1][y1]--;
    diff[x2+1][y2+1]++;
}

signed main(){
    int T,cnt=0;
    cin>>T;
    for(int i=0;i<T;i++)solve();
    // cout<<maxn<<endl;
    for(int i=1;i<=maxn;i++){
        for(int j=1;j<=maxn;j++){
            diff[i][j]+=diff[i][j-1]+diff[i-1][j]-diff[i-1][j-1];//二维前缀和
            // cout<<diff[i][j]<<" ";
            if(diff[i][j])cnt++;
        }
    }
    cout<<cnt<<endl;
    return 0;
}
```

## 2.9 组合数

```cpp
int C(int a, int b){
    if(a < b) return 0;
    int zi = fac[a];
    int mu = fac[b] * fac[a - b] % mod;
    return zi * inv(mu) % mod;
}

// 当a, b 很大比如>= 1e9, 模数P很小比如1e6+3, 可以用lucas定理求组合数, 时间复杂度O(logP + P)
int lucas(int a, int b){
    if(a < mod && b < mod) return C(a, b);
    return lucas(a / mod, b / mod) * C(a % mod, b % mod) % mod;
}

// 当a, b很小比如<= 1e3, 可以n^2预处理组合数和排列数
void init1(){
    C[0][0] = A[0][0] = 1;
    for(int i = 1; i < N; i++){
        C[i][0] = A[i][0] = 1;
        for(int j = 1; j <= i; j++){
            C[i][j] = (C[i - 1][j - 1] + C[i - 1][j]) % mod;
            A[i][j] = (j * A[i - 1][j - 1] % mod + A[i - 1][j]) % mod;
        }
    }
}
```

## 2.10 bitset

```cpp
#include <bits/stdc++.h>
using namespace std;

/*
 * =========================================
 * C++ bitset 用法全集模板（注释版），可优化常数1/64
 * =========================================
*/

const int N = 1024;   // bitset 大小必须是【编译期常量】

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    /* =========================
     * 一、定义与初始化
     * ========================= */

    bitset<N> a;                  // 默认全 0
    bitset<N> b(5);               // 用整数初始化（二进制形式存入）
    bitset<N> c("10101");         // 用字符串初始化（右边是低位）

    /* =========================
     * 二、单点访问与修改
     * ========================= */

    a[i];                         // 访问第 i 位（0-based）
    a.test(i);                    // 安全访问（返回 bool）

    a.set(i);                     // 第 i 位设为 1
    a.reset(i);                   // 第 i 位设为 0
    a.flip(i);                    // 第 i 位取反

    a.set(i, 1);                  // 指定赋值为 1
    a.set(i, 0);                  // 指定赋值为 0

    /* =========================
     * 三、整体操作
     * ========================= */

    a.set();                      // 所有位设为 1
    a.reset();                    // 所有位设为 0
    a.flip();                     // 所有位取反

    /* =========================
     * 四、位运算（核心能力）
     * ========================= */

    bitset<N> x, y, z;

    z = x & y;                    // 按位与
    z = x | y;                    // 按位或
    z = x ^ y;                    // 按位异或
    z = ~x;                       // 按位取反

    /* =========================
     * 五、位移操作（非循环）
     * ========================= */

    z = x << 3;                   // 左移 3 位，低位补 0，高位溢出丢弃
    z = x >> 2;                   // 右移 2 位，高位补 0，低位丢弃

    /* =========================
     * 六、统计与状态判断
     * ========================= */

    x.count();                    // 统计 1 的个数
    x.any();                      // 是否存在至少一个 1
    x.none();                     // 是否全为 0
    x.all();                      // 是否全为 1

    /* =========================
     * 七、转换
     * ========================= */

    bitset<32> num;

    num.to_ulong();               // 转 unsigned long（位数不能超）
    num.to_ullong();              // 转 unsigned long long

    num.to_string();              // 转 string（高位→低位）

    /* =========================
     * 八、遍历所有为 1 的位置（GNU 扩展，高效）
     * ========================= */

    // 从第一个为 1 的位开始找
    for (int i = a._Find_first(); i < N; i = a._Find_next(i)) {
        // i 为一个值为 1 的位置
    }

    /* =========================
     * 九、bitset 优化 DP（子集和模型）
     * ========================= */

    /*
     * dp[s] = 是否能凑出和 s
     * 状态转移：dp |= dp << w
     */

    const int MAXS = 10000;
    bitset<MAXS + 1> dp;

    dp[0] = 1;                    // 初始状态

    vector<int> w = {3, 5, 7};
    for (int v : w) {
        dp |= (dp << v);          // 子集和转移
    }

    /* =========================
     * 十、bitset 优化图论（传递闭包 / Floyd）
     * ========================= */

    /*
     * reach[i][j] = i 是否能到达 j
     * Floyd 核心：
     * if (reach[i][k]) reach[i] |= reach[k];
     */

    const int V = 500;
    bitset<V> reach[V];

    // 加边示例：u -> v
    int u = 1, v = 2;
    reach[u][v] = 1;

    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            if (reach[i][k]) {
                reach[i] |= reach[k];   // bitset 批量并集
            }
        }
    }

    /* =========================
     * 十一、常见用途总结
     * ========================= */

    /*
     * 1) 子集 DP
     *    dp |= dp << w
     *
     * 2) 图可达性
     *    reach[i] |= reach[k]
     *
     * 3) 状态压缩
     *    bitset 表示集合
     *
     * 4) 快速交集统计
     *    (a & b).count()
     *
     * 5) 快速并集
     *    a |= b
     */

    return 0;
}

```



<div style="page-break-after: always;"></div>

# 3 字符串

## 3.1 KMP1

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 1e6 + 10;

string s, t;
int n, m, ne[N];

void kmp(){
    for(int i = 2, j = 0; i <= m; i++){
        while(j && t[i] != t[j + 1]) j = ne[j];
        if(t[i] == t[j + 1]) j++;
        ne[i] = j;
    }

    for(int i = 1, j = 0; i <= n; i++){
        while(j && s[i] != t[j + 1]) j = ne[j];
        if(s[i] == t[j + 1]) j++;
        if(j == m){
            cout << i - j + 1 << endl;
            j = ne[j];
        }
    }
}

void solve(){
    cin >> s >> t;
    n = s.size(), m = t.size();
    s = " " + s;
    t = " " + t;
    kmp();
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 3.2 KMP2

```cpp
#include<iostream>
const int MAXN=1e5+10;
using namespace std;
void getNext(string t,int next[]){//i是后缀末尾,j是前缀末尾，也代表最长相等前后缀的长度
    int j=0,k=-1;
    next[0]=-1;
    while(j<t.size()-1){
        if(k==-1||t[j]==t[k]){
            j++,k++;
            next[j]=k;
        }
        else k=next[k];
    }

}

void getNextval(string t,int nextval[]){
    int j=0,k=-1;
    nextval[0]=-1;
    while(j<t.size()-1){
        if(k==-1||t[j]==t[k]){
            j++,k++;
            if(t[j]!=t[k]) nextval[j]=k;
            else nextval[j]=nextval[k];
        }
        else k=nextval[k];
    }
}

int KMP(string s,string t){
    int nextval[MAXN],i=0,j=0;
    getNextval(t,nextval);
    while(i<s.size()&&j<t.size()){
        if(j==-1||s[i]==t[j]){
            i++,j++;
        }
        else j=nextval[j];
    }
    if(j>=t.size())return i-t.size();
    else return -1;
}

int a[MAXN],nextval[MAXN];
int main(){
    string S="aabcabC8dab";
    string t="abcaabbabcab";
    getNext(t,a);
    getNextval(t,nextval);
    for(int i=0;i<=11;i++){
        cout<<a[i]<<" ";
    }
    cout<<endl;
    for(int i=0;i<=11;i++){
        cout<<nextval[i]<<" ";
    }
    return 0;
}
```

## 3.3 回文串个数

```cpp
#include<iostream>
using namespace std;
int count;
    int expand(string s,int left,int right){
        int cnt=0;
        while(left>=0&&right<s.size()&&s[left]==s[right]){
            left--;
            right++;
            cnt++;
        }
        return cnt;
    }
    int countSubstrings(string s) {
        count=0;
        for(int i=0;i<s.size();i++){
            count+=expand(s,i,i);
            count+=expand(s,i,i+1);
        }
        return count;
    }
```

## 3.4 字符串哈希

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int unsigned long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 3e2 + 10;
const int M = 6e4 + 10;
// 单模哈希, P取131或者13331, 模数为2^64(要求P与模数互质), unsigned long long自然溢出
const int P = 131; 
const int mod = 998244353;

void IOS(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
}

int n, q, m, K;
int fac[M];
string s[N], sq[N];
int hs[N][M], ht[N][M];

// 预处理P的幂
void init(){
    fac[0] = 1;
    for(int i = 1; i <= m; i++){
        fac[i] = fac[i - 1] * P;
    }
}

// 计算区间字符串的哈希值
int cal1(int i, int l, int r){
    return hs[i][r] - hs[i][l - 1] * fac[r - l + 1];
}

int cal2(int i, int l, int r){
    return ht[i][r] - ht[i][l - 1] * fac[r - l + 1];
}


void solve(){
    cin >> n >> q >> m >> K;
    init();
    for(int i = 1; i <= n; i++){
        cin >> s[i];
        s[i] = " " + s[i];
        hs[i][0] = 0;
        for(int j = 1; j <= m; j++){
            // 字符串哈希
            hs[i][j] = hs[i][j - 1] * P + (s[i][j] - 'a');
        }
    }   

    for(int i = 1; i <= q; i++){
        cin >> sq[i];
        sq[i] = " " + sq[i];
        ht[i][0] = 0;
        for(int j = 1; j <= m; j++){
            ht[i][j] = ht[i][j - 1] * P + (sq[i][j] - 'a');
        }

        int ans = 0;

        for(int j = 1; j <= n; j++){
            int lst = 0, diff = 0;        
            for(int k = 1; k <= K + 1; k++){
                int l = lst + 1, r = m;
                int tar = m + 1;
                while(l <= r){
                    int mid = (l + r) / 2;
                    if(cal1(j, lst + 1, mid) != cal2(i, lst + 1, mid)){
                        tar = mid;
                        r = mid - 1;
                    }
                    else l = mid + 1;
                }
                
                if(tar > m){
                    break;
                }
                diff++;
                lst = tar;
            }
            if(diff <= K){
                ans++;
                // cout << s[j] << endl;
            } 
        }

        cout << ans << endl;
    }
}

signed main(){
    IOS();
    int T = 1;
    
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```


<div style="page-break-after: always;"></div>

# 4 搜索与图论

## 4.1 Dijkstra

```cpp
// trick:虚拟源点
#include<bits/stdc++.h>
using namespace std;
const int MAXN=1e3+10;
int head[MAXN];//head[i]表示以i为起点的第一条边的边号
int n,en,s;//n个点，e条边，s原点
int dis[MAXN];//点到源点的距离
int check[MAXN];//标记一个点i的dis[i]已达最优
priority_queue<pair<int,int>,vector<pair<int,int>>,greater<>>heap;

struct Edge{
    int next;//下一条边的边号
    int to;//这条边的终点
    int w;//边的权值
}e[MAXN];

int cnt;//边的条数
void add(int u,int v,int w){//类似头插法
    cnt++;
    e[cnt].next=head[u];
    e[cnt].to=v;
    e[cnt].w=w;
    head[u]=cnt;
}

signed main(){
    cin>>n>>en;
    memset(dis,0x3f,sizeof dis);
    for(int i=1;i<=en;i++){
        int a,b,c;
        cin>>a>>b>>c;
        add(a,b,c);
        add(b, a, c);
    }
    cin>>s;
    dis[s]=0;
    heap.push({dis[s],s});
    while(!heap.empty()){
        auto [minn,minx]=heap.top();
        heap.pop();
        if(check[minx])continue;//去重
        check[minx]=1;
        for(int h=head[minx];h;h=e[h].next){
            int k=e[h].to;
            if(minn+e[h].w<dis[k]){
                dis[k]=minn+e[h].w;
                heap.push({dis[k],k});
            }
        }
    }
    return 0;
}
```

## 4.2 分层图最短路

```cpp
// 洛谷P4568 [JLOI2011] 飞行路线
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int MAXN=1e4+10;
const int N=4e5+10;

int n, m, k, s, t;
struct node{
    int to;
    int next;
    int w;
}e[2*N];

int dis[MAXN][20];
int head[MAXN];
bool visited[MAXN][20];
int cnt;

void add(int u, int v, int w){
    cnt++;
    e[cnt].to=v;
    e[cnt].w=w;
    e[cnt].next=head[u];
    head[u]=cnt;
}

priority_queue<PLL, vector<PLL>, greater<>>heap;

void dijstra(int p){
    dis[s][p]=0;
    heap.push({0, s});
    while(!heap.empty()){
        int x = heap.top().second;
        heap.pop();
        if(visited[x][p]) continue;
        visited[x][p] = 1;
        for(int i=head[x]; i; i=e[i].next){
            int x1=e[i].to, w1=e[i].w;
            if(dis[x][p] + w1 < dis[x1][p] || p && dis[x][p-1]< dis[x1][p]){
                dis[x1][p]=dis[x][p] + w1;
                if(p) dis[x1][p]=min(dis[x1][p], dis[x][p-1]);
                heap.push({dis[x1][p], x1});
            }

        }
    }
}

void solve(){
    cin>>n>>m>>k>>s>>t;
    for(int i=0; i<m; i++){
        int u ,v, w;
        cin>>u>>v>>w;
        add(u ,v, w);
        add(v, u, w);
    }
    memset(dis, 0x3f, sizeof(dis));
    for(int i=0; i<=k; i++) dijstra(i);
    cout<< dis[t][k] <<endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.3 Floyd

```cpp
#include<iostream>
using namespace std;
const int inf = 0x7fffff - 1;
int e[10][10];
int n, m;

int main() {
	cin >> n >> m;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			if (i == j)e[i][j] = 0;
			else e[i][j] = inf;
		}
	}
	int src, dst, val;
	for (int i = 0; i < m; i++) {
		cin >> src >> dst >> val;
		e[src][dst] = val;
	}

	//Floyd-Warshall算法核心语句
	for (int k = 0; k < n; k++) {
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				if (e[i][k] + e[k][j] < e[i][j]) {
					e[i][j] = e[i][k] + e[k][j];
				}
			}
		}
	}

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			printf("%5d", e[i][j]);
		}
		cout << endl;
	}
	return 0;
}
```

## 4.4 Kruskal

```cpp
//适用于稀疏图
#include<bits/stdc++.h>
using namespace std;
struct edge{ //直接存边 
	int u,v,w;
};
edge edges[200010];
int parent[5010];
 
int find(int x) //并查集(查找祖先) 
{
	while(x!=parent[x])
	    parent[x]=find(parent[x]);
	return parent[x];
}
 
bool cmp(edge obj1,edge obj2) //对边权进行排序 
{
	return obj1.w<obj2.w;
}
 
int main()
{
	int n,m;
	cin>>n>>m;
	for(int i=1;i<=m;i++) 
		cin>>edges[i].u>>edges[i].v>>edges[i].w;
	for(int i=1;i<=n;i++)
		parent[i]=i;
	sort(edges+1,edges+1+m,cmp); //对边进行排序 
	long long ans=0,cnt=0; //ans表示答案，cnt表示已经有多少条边被加进来了 
	for(int i=1;i<=m;i++) //遍历所有边 
	{
		if(find(edges[i].u)!=find(edges[i].v)) //如果公共祖先不同，那么就算不同的连通块 
		{
			ans+=edges[i].w; //答案更新 
			parent[find(edges[i].u)]=find(edges[i].v); //把新的点加入连通块中 
			cnt++; //边数+1 
		}
	}
	if(cnt<n-1) 
		cout<<"orz"; //n个点要有n-1条边，少于n-1条边说明会有孤立的点 
	else 
		cout<<ans;
	return 0;
}
```

## 4.5 Prim

```cpp
//适用于稠密图
#include<bits/stdc++.h>
using namespace std;
const int N=5010,INF=1e8+10;
int g[N][N];//邻接矩阵
int dist[N];//记录每个节点到当前生成树的最短距离
int st[N];//标记每个节点是否已被加入到生成树中
int n,m;
 
long long prim() //朴素的prim算法 
{
	long long ans=0; //记录答案 
	for(int i=0;i<n;i++)
	{
		int t=-1;  
		for(int j=1;j<=n;j++)
		{
			if(st[j]==0&&(t==-1||dist[j]<dist[t])) //把距离最小的且不在连通块的点加进来 
				t=j;
		}
		
		st[t]=1; //标记这个点已经被加入至连通块中 
		
		if(i!=0&&dist[t]==INF) 
			return INF; 	//如果不是最开始的情况并且最短距离是正无穷，说明是不连通的(最开始的时候dist[t]一定是正无穷，可以简单理解为最小生成树的"根") 
		if(i!=0) 
			ans+=dist[t]; //只要不是最开始的情况(树的根)，就把最短边的长度加入答案中 
		for(int j=1;j<=n;j++) 
			dist[j]=min(dist[j],g[t][j]); //更新各个点到连通块的最小距离 
	}
	return ans;
}
 
int main()
{
	cin>>n>>m;
	for(int i=1;i<=n;i++) //初始化操作 
	{
		dist[i]=INF;
		for(int j=1;j<=n;j++)
			g[i][j]=INF;
	}
	
	for(int i=1;i<=m;i++)
	{
		int x,y,z;
		cin>>x>>y>>z;
		if(x==y) 
			continue; //去掉自环
		//对于重边，取最小值即可 
		g[x][y]=min(g[x][y],z); 
		g[y][x]=min(g[y][x],z);
	}
	
	long long t=prim();
	
	if(t==INF) 
		cout<<"orz"; //表示存在不连通的情况 
	else 
		cout<<t;
	return 0;
}
```

## 4.6 SPFA

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 5e2 + 10;
const int M = 64;
const int mod = 998244353;
using PI3 = array<int, 3>;

void IOS(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
}

vector<PII>g[N];
int n, m1, m2;
bool st[N];
int dis[N], cnt[N];

// 如果存在负环，则返回true，否则返回false
bool spfa(){
    memset(dis, 0x3f, sizeof dis);
    memset(st, 0, sizeof st);
    memset(cnt, 0, sizeof cnt);
    queue<int>que; // 有环时可以用stack优化
    que.push(0);
    dis[0] = 0, st[0] = 1;

    while(que.size()){
        auto u = que.front();
        que.pop();
        st[u] = 0;
        for(auto [w, v] : g[u]){
            if(dis[u] + w >= dis[v]) continue;
            dis[v] = dis[u] + w;
            cnt[v] = cnt[u] + 1;
            if(cnt[v] >= n) return true; // 路径有n个点（不包括起点）说明有环并且是负环
            if(!st[v]){
                que.push(v);
                st[v] = 1;
            }
        }
    }
    return false;
}

void solve(){
    cin >> n >> m1 >> m2;
    for(int i = 1; i <= n; i++) g[i].clear();
    for(int i = 1; i <= m1; i++){
        int u, v, w; cin >> u >> v >> w;
        g[u].push_back({w, v});
        g[v].push_back({w, u});
    }    
    for(int i = 1; i <= m2; i++){
        int u, v, w; cin >> u >> v >> w;
        g[u].push_back({-w, v});
    } 
    
    for(int i = 1; i <= n; i++){
        g[0].push_back({0, i});
    }
    if(spfa()) cout << "YES" << endl;
    cout << "NO" << endl;
    
}

signed main(){
    IOS();
    int T = 1;
    cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.7 拓扑排序

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 2e5 + 10;
const int M = 2e5 + 10;

int n, m;
int ans[N], in[N];
vector<int>v[N];

void solve(){
    cin >> n >> m;
    for(int i = 1; i <= m; i++){
        int x, y;
        cin >> x >> y;
        //初始化
        in[y]++;
        v[x].push_back(y);
    }
    queue<int>que;
    for(int i = 1; i <= n; i++){
        // 现将0度入队
        if(in[i] == 0) que.push(i);
    }
    int cnt = 0;
    // 开始排序
    while(que.size()){
        if(que.size() == 1){
            int t = que.front();
            que.pop();
            ans[t] = ++cnt;
            for(auto i : v[t]){
                if(--in[i] == 0) que.push(i);
            }
        }
        else{
            cout << "No\n";
            return ;
        }
    }
    cout << "Yes\n";
    for(int i = 1; i <= n; i++){
        cout << ans[i] << " \n"[i == n];
    }
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.8 三类并查集

```cpp
#include<iostream>
using namespace std;
int father[100010];
int n;

struct DSU {
    std::vector<int> f, siz;
    
    DSU() {}
    DSU(int n) {
        init(n);
    }
    
    void init(int n) {
        f.resize(n);
        std::iota(f.begin(), f.end(), 0);
        siz.assign(n, 1);
    }
    
    int find(int x) {
        while (x != f[x]) {
            x = f[x] = f[f[x]];
        }
        return x;
    }
    
    bool same(int x, int y) {
        return find(x) == find(y);
    }
    
    bool merge(int x, int y) {
        x = find(x);
        y = find(y);
        if (x == y) {
            return false;
        }
        siz[x] += siz[y];
        f[y] = x;
        return true;
    }
    
    //求祖宗结点所在连通块的点数
    int size(int x) {
        return siz[find(x)];
    }
};


// 带权并查集
int w[N];// 设w[u] = a[u] - a[fa[u]];

struct DSU{
    vector<int>fa;
    DSU(int n = 0){
        fa.resize(n);
        iota(fa.begin(), fa.end(), 0);
    }
    
    int find(int u){
        if(u == fa[u]) return u;
        int f = fa[u];
        int nxt = find(f);
        w[u] += w[f];
        return fa[u] = nxt;
    }
    
    int same(int u, int v){
        return find(u) == find(v);
    }
    
    bool merge(int u, int v, int k){
        int fu = find(u), fv = find(v);
        if(fu == fv) return false;
        w[fu] = k - w[u] + w[v];
        fa[fu] = fv;
        return true;
    }
};
```

## 4.9 树的直径

```cpp
//P4408 [NOI2003] 逃学的小孩
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int MAXN=2e6+10;
const int N=2e5+10;
int n, m;

struct edge{
    int to;
    int next;
    int w;
}e[2*N];

int head[N], dis1[N], dis2[N];
int cnt;

void add(int u, int v, int w){
    cnt++;
    e[cnt].to=v;
    e[cnt].w=w;
    e[cnt].next=head[u];
    head[u]=cnt;
}

int maxdis,beginv;
void dfs1(int u ,int fa, int dis){//求第一个端点
    if(dis > maxdis){
        maxdis=dis;
        beginv=u;
    }
    for(int i=head[u]; i; i=e[i].next){
        int v=e[i].to, w=e[i].w;
        if(v == fa) continue;
        dfs1(v, u, dis+w);
    }
}

int endv;

void dfs2(int u, int fa, int dis){//求第二个端点, 顺便求其他点到第一个端点距离
    dis1[u]=dis;
    if(dis > maxdis){
        maxdis=dis;
        endv=u;
    }
    for(int i=head[u]; i; i=e[i].next){
        int v=e[i].to, w=e[i].w;
        if(v == fa) continue;
        dfs2(v, u, dis+w);
    }
}
//dfs2求完之后, maxdis即为数的直径

void dfs3(int u, int fa, int dis){//求其他点到第二个端点距离
    dis2[u]=dis;
    for(int i=head[u]; i; i=e[i].next){
        int v=e[i].to, w=e[i].w;
        if(v == fa) continue;
        dfs3(v, u, dis+w);
    }
}

void solve(){
    cin>>n>>m;
    for(int i=0; i<m; i++){
        int u, v, w;
        cin>>u>>v>>w;
        add(u, v, w);
        add(v, u, w);
    }
    dfs1(1, 0, 0);
    maxdis=0;
    dfs2(beginv, 0, 0);
    dfs3(endv, 0, 0);
    int res=0;
    for(int i=1; i<=n; i++){
        res=max(res, min(dis1[i], dis2[i]));
    }

    cout<<res+maxdis<<endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.10 最近公共祖先
```cpp
#include<bits/stdc++.h>
const int N = 5e5 + 10;
const int STEP = 20;
using namespace std;

vector<int>g[N];
int n, m, root;
int depth[N], fa[N][STEP];

void dfs(int u, int father){
    depth[u] = depth[father] + 1;
    fa[u][0] = father;
    for(int i = 1; (1 << i) <= depth[u]; i++){
        fa[u][i] = fa[fa[u][i - 1]][i - 1];
    }
    for(auto v : g[u]){
        if(v == father) continue;
        dfs(v, u);
    }
}

int lca(int x, int y){
    if(depth[x] < depth[y]) swap(x, y);
    for(int i = STEP - 1; i >= 0; i--){
        if((depth[x] - depth[y]) & (1 << i)) x = fa[x][i];
    }

    if(x == y) return x;
    for(int i = STEP - 1; i >= 0; i--){
        if(fa[x][i] != fa[y][i]){
            x = fa[x][i], y = fa[y][i];
        }
    }

    return fa[x][0];
}

void solve(){
    cin >> n >> m >> root;
    for(int i = 1; i < n; i++){
        int x, y; cin >> x >> y;
        g[x].push_back(y);
        g[y].push_back(x);
    }
    dfs(root, -1);
    while(m--){
        int a, b; cin >> a >> b;
        cout << lca(a, b) << endl;
    }
}

signed main(){
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.11 SCC(强连通分量)

```cpp
#include <bits/stdc++.h>
using namespace std;
using i64 = long long;
#define int long long
#define endl "\n"
const int N = 2e5 + 10;

vector<int>g[N];
int dfn[N], low[N], tot;// 时间戳dfn[i]表示节点i第一次被访问的顺序, low[i] 表示从节点i出发能访问的最早时间戳
int stk[N], instk[N], top;// stk[]模拟栈, instk[i]表示节点i在栈中
int scc[N], siz[N], cnt;// scc[i]表示节点i的强连通分量的编号, siz[i]表示编号i的scc包含多少节点

//tarjan scc缩点, 缩完的点刚好是拓扑逆序的
void tarjan(int u){ // 时间复杂度O(n + m)
    dfn[u] = low[u] = ++tot;
    stk[++top] = u, instk[u] = 1;
    for(auto v : g[u]){
        if(dfn[v] == 0){// 若v未访问
            tarjan(v);
            low[u] = min(low[u], low[v]);
        }
        else if(instk[v]){// 若v已访问并在栈中
            low[u] = min(low[u], dfn[v]);
        }
    }

    if(dfn[u] == low[u]){// 若u是scc的根
        int t; cnt++;
        do{
            t = stk[top--], instk[t] = 0;
            scc[t] = cnt, siz[cnt]++;
        }while(t != u);
    }
}

int n;
int din[N], dout[N];// din[i]表示入度, dout表示出度

void solve(){
    cin >> n;
    for(int i = 1; i <= n; i++){
        int v;
        while(cin >> v, v){
            g[i].push_back(v);
        }
    }   
    
    for(int u = 1; u <= n; u++){
        if(dfn[u] == 0) tarjan(u);
    }
    
    for(int u = 1; u <= n; u++){
        for(auto v : g[u]){
            if(scc[u] != scc[v]){
                dout[scc[u]]++;
                din[scc[v]]++;
            }
        }
    }
    int cnt1 = 0, cnt2 = 0;
    for(int i = 1; i <= cnt; i++){
        if(din[i] == 0) cnt1++;
        if(dout[i] == 0) cnt2++;
    }
    cout << cnt1 << endl;
    if(cnt == 1) cout << 0 << endl;
    else cout << max(cnt1, cnt2) << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.12 IDDFS

```cpp
#include <bits/stdc++.h>
using namespace std;

#define int long long
#define endl "\n"
const int N = 1e3 + 10;

int n;
int s[100], m;

//剪枝之后时间复杂度O(m^2 * 2^m)
bool dfs(int p, int sum){
    if(p == m) return sum == n;
    if(sum << m-p < n) return false;
    s[p] = sum;
    for(int i = 0; i <= p; i++){
        if(dfs(p + 1, sum - s[i]) || dfs(p + 1, sum + s[i])) return true;
    }
    return false;
}

void solve(){
    //枚举深度
    for(m = 0; !dfs(0, 1); m++);
    cout << m << endl;
}

signed main(){
    while(cin >> n && n){
        solve();
    }
    return 0;
}
```

## 4.13 双向bfs

```cpp
// acwing 190.字符变换
#include <bits/stdc++.h>
using namespace std;
#define endl "\n"
const int N = 5e5 + 10;

int n;
string s0, sn;
unordered_map<string, int>da;
unordered_map<string, int>db;
vector<string>a, b;

int extend(queue<string>& que, unordered_map<string, int>& da, unordered_map<string, int>& db, vector<string>& a, vector<string>& b){
    string s = que.front();
    que.pop();
    for(int i = 0; i < n; i++){
        int l1 = a[i].size();
        for(int j = 0; j <= (int)s.size() - l1; j++){
            if(s.substr(j, l1) == a[i]){
                string t = s;
                t.replace(j, l1, b[i]);
                if(da.count(t)) continue;
                da[t] = da[s] + 1;
                if(db.count(t)) return da[t] + db[t];
                que.push(t);
            }
        }
    }

    return 11;
}

int bfs(){
    if(s0 == sn) return 0;
    queue<string>q1;
    queue<string>q2;
    q1.push(s0), da[s0] = 0;
    q2.push(sn), db[sn] = 0;
    while(q1.size() && q2.size()){
        int d;
        if(q1.size() < q2.size()) d = extend(q1, da, db, a, b);
        else d = extend(q2, db, da, b, a);
        if(d < 11) return d;
    }

    return 11;
}

void solve(){   
    cin >> s0 >> sn;
    string t1, t2;
    while(cin >> t1 >> t2){
        a.push_back(t1);
        b.push_back(t2);
    }
    n = a.size();

    int ans = bfs();
    if(ans < 11) cout << ans << endl;
    else cout << "NO ANSWER!" << endl;
}

signed main(){
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.14 Astar

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
typedef pair<int, int> PII;
#define endl "\n"
const int N = 1e3 + 10;
const int LNF = 0x3f3f3f3f3f3f3f3f;
using PIII = array<int, 3>;

int n, m;
int s, t, k;
vector<PII>g1[N];
vector<PII>g2[N];
int st[N];
int dis[N];// 所有点到终点的最短距离, 预估函数

void dijstra(){
    memset(dis, 0x3f, sizeof dis);
    priority_queue<PII, vector<PII>, greater<>>heap;
    dis[t] = 0;
    heap.push({0, t});
    while(heap.size()){
        auto [min_w, u] = heap.top();
        heap.pop();
        if(st[u]) continue;
        st[u] = true;
        for(auto [v, w] : g2[u]){
            if(dis[u] + w < dis[v]){
                dis[v] = dis[u] + w;
                heap.push({dis[v], v});
            }
        }
    }
}

int Astar(){
    priority_queue<PIII, vector<PIII>, greater<>>heap;
    memset(st, 0, sizeof st);
    heap.push({dis[s], 0, s});
    int cnt = 0;
    while(heap.size()){
        auto [min_w, w, u] = heap.top();
        heap.pop();
        if(st[u] >= k) continue;
        st[u]++;
        if(st[u] == k && u == t) return w;
        for(auto [v, w1] : g1[u]){
            if(st[v] < k)
            heap.push({dis[v] + w + w1, w + w1, v}); // 真实距离 + 预估距离 = 评价值
        }
    }
    return -1;
}

void solve(){
    cin >> n >> m;
    for(int i = 1; i <= m; i++){
        int u, v, w; cin >> u >> v >> w;
        g1[u].push_back({v, w});
        g2[v].push_back({u, w});
    }   

    cin >> s >> t >> k;
    dijstra();
    if(s == t) k++;
    cout << Astar() << endl;
}

signed main(){
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.15 环的大小

```cpp
#include<bits/stdc++.h>
#define int long long
#define endl "\n"
const int N = 2e5 + 10;
using namespace std;

int n, m;
vector<int>g[N];
int st[N];

void dfs(int u, int begin, int cnt){
    for(auto v : g[u]){
        if(st[v]){
            continue;
        }
        if(v == begin){
            // 此时cnt即为环的大小
            // 
        }
        st[v] = 1;
        dfs(v, begin, cnt + 1);
        // st[v] = 0;
    }
}

void solve(){
    cin >> n >> m;
    for(int i = 1; i <= n; i++) g[i].clear(), st[i] = 0;
    for(int i = 1; i <= m; i++){
        int u, v; cin >> u >> v;
        g[u].push_back(v);
        g[v].push_back(u);
    }
}

signed main(){
	int T = 1;
	cin >> T;
	while(T--){
		solve();
	}
}
```

## 4.16 双向dfs

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 46 + 10;

int n, m;
int a[N];
int ans = 0;
vector<int>p;

int find(int x){
    int l = 0, r = (int)p.size() - 1;
    int res = 0;
    while(l <= r){
        int mid = l + r >> 1;
        if(x + p[mid] <= m){
            res = p[mid];
            l = mid + 1;
        }
        else r = mid - 1;
    }
    return x + res;
}

// 存前n/2的dfs的所有可能值
void dfs1(int u, int s){
    if(s > m) return ;
    if(u > n / 2){
        p.push_back(s);
        return ;
    }
    dfs1(u + 1, s + a[u]);
    dfs1(u + 1, s);
}

// 利用第一部分的值来二分
void dfs2(int u, int s){
    if(s > m) return ;
    ans = max(ans, find(s));
    if(u > n) return ;
    dfs2(u + 1, s + a[u]);
    dfs2(u + 1, s);
}

void solve(){
    cin >> m >> n;    
    for(int i = 1; i <= n; i++) cin >> a[i];
    sort(a + 1, a + n + 1, greater());
    dfs1(1, 0);
    sort(p.begin(), p.end());
    p.erase(unique(p.begin(), p.end()), p.end());
    dfs2(n / 2 + 1, 0);
    cout << ans << endl;
}

signed main(){
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.17 IDAstar

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"

int n;
int a[16];
int p[5][16];

int get(){ // 预估函数
    int cnt = 0;
    for(int i = 1; i < n; i++){
        if(a[i + 1] != a[i] + 1) cnt++;
    }
    return (cnt + 2) / 3;
}

bool dfs(int dep, int max_dep){
    if(dep + get() > max_dep) return false;
    if(get() == 0) return true;
    memcpy(p[dep], a, sizeof a);
    for(int len = 1; len <= n; len++){
        for(int i = 1; i + len - 1 <= n; i++){
            for(int k = 1; k < i; k++){
                for(int l = i - 1; l >= k; l--) a[l + len] = a[l];
                for(int l = k; l <= k + len - 1; l++) a[l] = p[dep][l - k + i];
                if(dfs(dep + 1, max_dep)) return true;
                memcpy(a, p[dep], sizeof a);
            }
        }
    }
    return false;
}

void solve(){
    cin >> n;
    for(int i = 1; i <= n; i++) cin >> a[i];
    for(int i = 0; i < 5; i++){
        if(dfs(0, i)){
            cout << i << endl;
            return ;
        }
    }
    cout << "5 or more" << endl;
}

signed main(){
    int T = 1;
    cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.18 dfs剪枝

```cpp
// stick 法（逐根拼棍子）
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 64 + 10;

int n, ans, tar, zu;
int a[N], b[N];
bool st[N];

// dfs(start, u, s)
// start : 从哪根木棒开始尝试（下标）
// u     : 已经拼好的棍子数量
// s     : 当前这根棍子已经拼出的长度
// 返回值: 是否能成功拼完所有棍子
bool dfs(int start, int u, int s) {
    // 如果已经拼好了 zu 根棍子（总数），说明成功
    if (u == zu) return true;

    // 如果当前这根棍子刚好拼满 tar 长度
    // 那么递归去拼下一根棍子（长度从 0 开始）
    if (s == tar) return dfs(0, u + 1, 0);

    // 从 start 开始枚举剩余的木棒
    for (int i = start; i <= n; i++) {
        if (st[i]) continue;             // 木棒已用过，跳过
        if (s + a[i] > tar) continue;    // 超过目标长度，跳过

        st[i] = true;                    // 标记当前木棒已用
        if (dfs(i + 1, u, s + a[i])) return true; // 尝试放入当前棍子
        st[i] = false;                   // 回溯

        // -------- 剪枝部分 --------
        if (s == 0) return false;        // 如果这根棍子的第一个木棒放不进去，直接失败（避免对称）
        if (s + a[i] == tar) return false; // 如果放进去刚好填满但失败了，也直接失败
        // 同层去重：如果有多根木棒长度相同，只尝试一次，避免重复搜索
        int j = i;
        while (j <= n && a[j] == a[i]) j++;
        i = j - 1;
    }
    return false; // 所有尝试都失败
}

void solve(){
    int sum = 0;
    for(int i = 1; i <= n; i++) cin >> a[i], sum += a[i], b[i] = st[i] = 0;
    sort(a + 1, a + n + 1, greater());
    ans = sum;
    for(int i = n; i >= 1; i--){
        if(sum % i) continue;
        tar = sum / i, zu = i;
        if(dfs(1, 0, 0)){
            ans = tar;
            break;
        }
    }
    cout << ans << endl;
}

signed main(){
    int T = 1;
    while(cin >> n && n){
        solve();
    }
    return 0;
}
```

## 4.19 ksm优化最短路

```cpp
//s->t恰好经过k条边的最短路
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 2e2 + 10;
const int M = 2e5 + 10;

int n, p, m, s, t;
int dis[N][N], ans[N][N];
int temp[N][N];
map<int, int>mp; //离散化每个点

void mul(int c[][N], int a[][N], int b[][N]){
    for(int i = 1; i <= n; i++){
        fill(temp[i], temp[i] + n + 1, 1e18);
    }

    for(int k = 1; k <= n; k++){
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= n; j++){
                temp[i][j] = min(temp[i][j], a[i][k] + b[k][j]);
            }
        }
    }

    memcpy(c, temp, sizeof temp);
}

void ksm(){ //倍增
    for(int i = 1; i <= n; i++){
        fill(ans[i], ans[i] + n + 1, 1e18);
        ans[i][i] = 0; //初始经过0条边
    }
    
    while(p){
        if(p&1) mul(ans, ans, dis); // ans = ans * dis;
        mul(dis, dis, dis); // dis = dis * dis;
        p >>= 1;
    }
}

void solve(){
    cin >> p >> m >> s >> t;
    for(int i = 1; i <= 2 * m; i++){
        fill(dis[i], dis[i] + 2 * m + 1, 1e18);
    }

    for(int i = 1; i <= m; i++){
        int u, v, w; cin >> w >> u >> v;
        if(!mp.count(u)) mp[u] = ++n;
        if(!mp.count(v)) mp[v] = ++n;
        u = mp[u], v = mp[v];
        dis[u][v] = dis[v][u] = min(dis[u][v], w);
    }

    s = mp[s], t = mp[t];

    ksm();
    cout << ans[s][t] << endl;
}

signed main(){
    IOS();
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.20 最小环（floyd）

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 1e2 + 10;
const int M = 2e5 + 10;

int n, m;
int dis[N][N], d[N][N];
int mid[N][N];
vector<int>path;

void get_path(int i, int j){
    int k = mid[i][j];
    if(k == 0) return ;
    get_path(i, k);
    path.push_back(k);
    get_path(k, j);
}

void solve(){
    cin >> n >> m;   
    for(int i = 1; i <= n; i++){
        fill(dis[i], dis[i] + n + 1, 1e18);
    }

    for(int i = 1; i <= m; i++){
        int u, v, w; cin >> u >> v >> w;
        dis[v][u] = dis[u][v] = min(dis[u][v], w);
    }
    
    memcpy(d, dis, sizeof d); //存原始边长
    int ans = 1e18;
    for(int k = 1; k <= n; k++){
        for(int i = 1; i < k; i++){ //枚举环上的三个点i,k,j
            for(int j = i + 1; j < k; j++){
                if(dis[i][j] + d[j][k] + d[k][i] < ans){
                    ans = dis[i][j] + d[j][k] + d[k][i];
                    path = {j, k, i};
                    get_path(i, j);
                }
            }
        }

        for(int i = 1; i <= n; i++){ //计算最短路和求中间点
            for(int j = 1; j <= n; j++){
                if(dis[i][k] + dis[k][j] < dis[i][j]){
                    dis[i][j] = dis[i][k] + dis[k][j];
                    mid[i][j] = k; 
                }
    
            }
        }
    }

    if(ans > 1e18/2) cout << "No solution." << endl;
    else{
        for(auto x : path) cout << x << " ";
        cout << endl;
    }

}

signed main(){
    IOS();
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.21 最小环（dfs）

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
typedef pair<int, int> PII;
#define endl "\n"
#define x first
#define y second
const int N = 1e2 + 10;
const int M = 2e5 + 10;

int n, m;
vector<PII>g[N];
int cnt[N], st[N];
vector<int>p;
int mi = 1e18;
vector<int>ans;

void dfs(int u, int fa){
    cnt[u]++;
    for(auto [w, v] : g[u]){
        if(v == fa) continue;
        if(cnt[v]) cnt[v]++;
        if(!cnt[v]){
            dfs(v, u);
        }
    }
}

void loop(int u, int fa, int sum){
    if(sum >= mi) return ;
    st[u] = 1;
    p.push_back(u);
    for(auto [w, v] : g[u]){
        if(v == fa) continue;
        if(st[v]){
            if(sum + w < mi){
                ans = p;
                mi = sum + w;
            }
        }
        else{
            loop(v, u, sum + w);
        }
    }
    st[u] = 0;
    p.pop_back();
}

void solve(){
    cin >> n >> m;  
    map<PII, int>mp;  
    for(int i = 1; i <= m; i++){
        int u, v, w; cin >> u >> v >> w;
        if(u > v) swap(u, v);
        if(mp.count({u, v})) mp[{u, v}] = min(mp[{u, v}], w);
        mp[{u, v}] = w;
    }
    
    for(auto x : mp){
        auto [u, v] = x.x;
        int w = x.y;
        g[u].push_back({w, v});
        g[v].push_back({w, u});
    }

    dfs(1, -1);

    for(int i = 1; i <= n; i++){
        if(cnt[i] > 1) loop(i, -1, 0);
    }

    if(ans.size() == 0) cout << "No solution." << endl;
    else{
        for(auto x : ans) cout << x << " ";
        cout << endl;
    }
}

signed main(){
    IOS();
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.22 eDCC(边双连通分量)

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 5e4 + 10;
const int M = 1e4 + 10;
const int mod = 998244353;
using PI3 = array<int, 3>;

int n, m;
vector<PII>g[N];
int dfn[N], low[N], tot;
stack<int>stk;
int dcc[N], siz[N], cnt;
bool bri[M];

void tarjan(int u, int edge){
    dfn[u] = low[u] = ++tot;
    stk.push(u);
    for(auto [v, id] : g[u]){
        if(!dfn[v]){
            tarjan(v, id);
            low[u] = min(low[u], low[v]);
            if(low[v] > dfn[u]){ // u-v边为割边或桥
                bri[id] = bri[id^1] = 1;
            }
        }
        else if(id != (edge^1)){ // 不是反向边
            low[u] = min(low[u], dfn[v]);
        }
    }

    if(dfn[u] == low[u]){
        int t = -1; cnt++;
        do{
            t = stk.top(), stk.pop();
            dcc[t] = cnt, siz[cnt]++; // 记录edcc
        }while(t != u);
    }
}

int d[N];

void solve(){
    cin >> n >> m;
    for(int i = 0; i < m; i++){
        int u, v; cin >> u >> v;
        g[u].push_back({v, i*2});
        g[v].push_back({u, i*2 + 1});
    }

    for(int i = 1; i <= n; i++){
        if(!dfn[i]) tarjan(i, 0);
    }

    for(int u = 1; u <= n; u++){
        for(auto [v, id] : g[u]){
            if(dcc[u] != dcc[v]){
                d[dcc[u]]++, d[dcc[v]]++;
            }
        }
    }

    int ans = 0;
    for(int i = 1; i <= cnt; i++){
        if(d[i] <= 2) ans++;
    }
    
    if(cnt == 1) cout << 0 << endl;
    else cout << (ans + 1) / 2 << endl;
}

signed main(){
    IOS();
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.23 vDCC(点双连通分量)

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 2e3 + 10;
const int M = 64;
const int mod = 998244353;
using PI3 = array<int, 3>;
using ull = unsigned long long;

int n, m;
int dfn[N], low[N], tot;
stack<int>stk;
vector<int>dcc[N], g[N];
int cut[N], cnt;

void tarjan(int u, int root){
    dfn[u] = low[u] = ++tot;
    stk.push(u);
    if(!g[u].size()){ // 孤立点
        dcc[++cnt].push_back(u);
        return ;
    }

    int child = 0;
    for(auto v : g[u]){
        if(!dfn[v]){
            tarjan(v, root);
            low[u] = min(low[u], low[v]);
            if(low[v] >= dfn[u]){ 
                child++;
                // u为割点
                if(u != root || child > 1) cut[u] = 1; 

                int t = -1; ++cnt;
                do{ // 记录vdcc连通块
                    t = stk.top(), stk.pop();
                    dcc[cnt].push_back(t);
                }while(t != v);
                dcc[cnt].push_back(u);
            }
            
        }
        else low[u] = min(low[u], dfn[v]);
    }
}

void solve(int T){
    n = cnt = tot = 0;
    for(int i = 1; i <= 1e3; i++){
        g[i].clear(), dcc[i].clear();
        cut[i] = dfn[i] = low[i] = 0;
    }
    for(int i = 1; i <= m; i++){
        int u, v; cin >> u >> v;
        g[u].push_back(v);
        g[v].push_back(u);
        n = max({n, u, v});
    }

    for(int i = 1; i <= n; i++){
        if(!dfn[i]) tarjan(i, i);
    }

    ull need = 0, ans = 1;
    for(int i = 1; i <= cnt; i++){
        int num = 0;
        for(auto v : dcc[i]){
            if(cut[v]) num++;
        }
        if(num == 0){
            if(dcc[i].size() > 1) need += 2, ans *= dcc[i].size() * (dcc[i].size() - 1) / 2;
            else need++;
        } 
        else if(num == 1) need++, ans *= dcc[i].size() - 1;
    }
    cout << "Case " << T << ": " << need << " " << ans << endl;
}

signed main(){
    IOS();
    int T = 0;
    // cin >> T;
    while(cin >> m && m){
        solve(++T);
    }
    return 0;
}
```

## 4.24 匈牙利算法

```cpp
// 二分图中, 最大匹配数 = 最小点覆盖, 最大独立集 = n - 最大匹配数 = 最小路径覆盖
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 1e2 + 10;
const int M = 1e3;
const int mod = 998244353;
using PI3 = array<int, 3>;

int n, t;
int g[N][N], match[N][N];
bool vis[N][N];

int d[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

// 男女相亲, 男选女, 可占可让, 贪心匹配
bool dfs(int x0, int y0){
    for(int i = 0; i < 4; i++){ // 只用单向边, 男->女
        int x1 = x0 + d[i][0], y1 = y0 + d[i][1];
        if(x1 < 1 || x1 > n || y1 < 1 || y1 > n || g[x1][y1] || vis[x1][y1]) continue;
        vis[x1][y1] = 1; // 标记妹子
        if(!match[x1][y1] || dfs(match[x1][y1] / M, match[x1][y1] % M)){
            match[x1][y1] = x0 * M + y0; // 配成对
            return true;
        }
    }
    return false;
}

void solve(){
    cin >> n >> t;
    for(int i = 1; i <= t; i++){
        int x, y; cin >> x >> y;
        g[x][y] = 1;
    }

    int ans = 0;
    // 时间复杂度O(n * m) 
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            memset(vis, 0, sizeof vis);
            if((i + j) % 2 == 0 && !g[i][j]){
                if(dfs(i, j)) ans++;
            }
        }
    }
    cout << ans << endl;
}

signed main(){
    IOS();
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 4.25 欧拉回路(路径)

```cpp
// 1.无向图, 所有边联通(可以用dfs判联通):
// 欧拉回路：度数为奇数的点个数为0
// 欧拉路径：度数为奇数的点个数为0或2
// 2.有向图, 所有边联通:
// 欧拉回路：入度不等于出度的点个数为0
// 欧拉路径：入度不等于出度的点个数为0; 或者2, 要求出度=入度+1的点为起点, 入度=出度+1的点为终点
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 1e5 + 10;
const int M = 2e5 + 10;
const int mod = 998244353;
using PI3 = array<int, 3>;

int t, n, m;
vector<PII>g[N];
bool st[2 * M];
int din[N], dout[N];
vector<int>ans; // 求出来的是逆序

// 后序遍历, 求欧拉回路或者欧拉路径的点或者边
void dfs(int u){
    while(g[u].size()){
        auto &[id, v] = g[u].back();
        g[u].pop_back();
        if(st[id]) continue;
        if(t == 1){
            st[id] = st[id^1] = 1;
        }
        else{
            st[id] = 1;
        }

        dfs(v);
        if(t == 1){
            int op = 1;
            if(id&1) op = -1;
            ans.push_back((id/2 + 1) * op);
            st[id] = st[id^1] = 1;
        }
        else{
            ans.push_back(id);
            st[id] = 1;
        }
        
    }
}

void s1(){
    int root = 0;
    for(int i = 0; i < m; i++){
        int u, v; cin >> u >> v;
        g[u].push_back({2 * i, v});
        g[v].push_back({2 * i + 1, u});
        dout[u]++, din[v]++;
        root = u;
    }

    for(int i = 1; i <= n; i++){
        if(din[i] + dout[i] & 1){
            cout << "NO" << endl;
            return ;
        }
    }

    dfs(root);
    if(ans.size() != m){
        cout << "NO" << endl;
        return ;

    }

    cout << "YES" << endl;
    reverse(ans.begin(), ans.end());
    for(auto &x : ans) cout << x << " ";
}

void s2(){
    int root = 0;
    for(int i = 1; i <= m; i++){
        int u, v; cin >> u >> v;
        g[u].push_back({i, v});
        dout[u]++, din[v]++;
        root = u;
    }

    for(int i = 1; i <= n; i++){
        if(din[i] != dout[i]){
            cout << "NO" << endl;
            return ;
        }
    }

    dfs(root);
    if(ans.size() != m){
        cout << "NO" << endl;
        return ;

    }
    cout << "YES" << endl;
    reverse(ans.begin(), ans.end());
    for(auto &x : ans) cout << x << " ";
}

void solve(){
    cin >> t >> n >> m;
    if(t == 1) s1();
    else s2();

}

signed main(){
    IOS();
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```



<div style="page-break-after: always;"></div>

# 5 数论

## 5.1 高精度

```cpp
const int M = 50;
void add(int a[], int b[]){
    static int c[M];
    memset(c, 0, sizeof c);
    int t = 0;
    for(int i = 0; i < M; i++){
        t += a[i] + b[i];
        c[i] = t%10;
        t /= 10;
    }
    memcpy(a, c, sizeof c);
}

void mul(int a[], int b){
    static int c[M];
    memset(c, 0, sizeof c);
    int t = 0;
    for(int i = 0; i < M; i++){
        t += a[i] * b;
        c[i] = t % 10;
        t /= 10;
    }
    memcpy(a, c, sizeof c);
}

void add(vector<int>&A, vector<int>&B){
    int t = 0;
    int la = a.size(), lb = b.size();
    int i;
    for(i = 0; i < la || l < lb; i++){
        if(i < la) t += A[i];
        if(i < lb) t += B[i];
        A[i] = t % 10;
        t /= 10;
    }
    while(t){
        A[i++] = t % 10;
        t /= 10;
    }
}

//高精度乘低精度
void mul(vector<int>&A, int b){
    int t = 0;
    for(int i = 0; i < A.size(); i++){
        t += A[i] * b;
        A[i] = t % 10;
        t /= 10;
    }
    while(t) A.push_back(t%10), t /= 10;

}
```

## 5.2 线性筛

```cpp
//质数都符合 6*n+1 或者 6*n-1
const int N = 5e4 + 10;
int flag[N], prime[N], phi[N]; // phi[i]是欧拉函数(<=i与i互质的个数)
int mobius[N]; // 莫比乌斯函数(-1, 0, 1)
int pnum;

void getPrime(){
    flag[1] = 1, phi[1] = 1, mobius[1] = 1;
    for(int i = 2; i < N; i++){
        if(!flag[i]){
            prime[++pnum] = i;
            phi[i] = i - 1;
            mobius[i] = -1;
        }
        for(int j = 1; j <= pnum && i * prime[j] < N; j++){
            flag[i * prime[j]] = 1;
            if(i % prime[j] == 0){
                phi[i * prime[j]] = phi[i] * prime[j];
                mobius[i * prime[j]] = 0;
                break;
            }
            phi[i * prime[j]] = phi[i] * (prime[j] - 1);
            mobius[i * prime[j]] = mobius[i] * -1;
        } 
    }
}

// 勒让德定理, 求n!里面有多少p的因子
int get(int n, int p){
    int cnt = 0;
    while(n){
        cnt += n / p;
        n /= p;
    }
    return cnt;
}
```

## 5.3 裴蜀定理

```cpp
int x, y, a, b, c, d;

//裴蜀定理
//a*m+b*n=y, a,b,y为定值, 想要找到满足方程的一组整数m, n, 需要使 y可以整除gcd(a, b)
void solve(){
    cin>>x>>y>>a>>b>>c>>d;
    int flag=1;
    if(x%gcd(d,c)) flag=0;
    if(y%gcd(a, b)) flag=0;
    if(flag) cout<<"YES\n";
    else cout<<"NO\n";

}
```

## 5.4 扩展欧几里得(exgcd)

```cpp
// a * x + b * y = gcd(a, b) = d, d是gcd(a, b)的倍数才有解
int exgcd(int a, int b, int &x, int &y){
    if(!b){
        x = 1, y = 0;
        return a;
    }
    int d = exgcd(b, a % b, y, x);
    y -= a / b * x; 
    return d;
}

// 通解 
// x = x + k * (b / d), step_x = b / d; 此处d为gcd(a, b), d若是倍数则需要先将x, y扩大
// y = y - k * (a / d), step_y = a / d;
```

## 5.5 gcd

```cpp
inline int gcd(int a,int b) {
    int r;
    while(b>0) {
        r=a%b;
        a=b;
        b=r;
    }
    return a;
}

inline int gcd1(int a,int b) {
    return b>0 ? gcd(b,a%b):a;
}

inline int gcd2(int a,int b) {
    while(b^=a^=b^=a%=b);
    return a;
}

inline int gcd3(int a,int b) {
	if(b) while((a%=b) && (b%=a));
	return a+b;
}
```

## 5.6 数论分块

```cpp
#include<bits/stdc++.h>
#define int long long
const int N = 2e6+10;
#define PII pair<int, int>
using namespace std;

void solve(){
    int q;
    cin>>q;
    while(q--){
        int x;
        cin>>x;
        int ans = 0;
        for(int l = 1, r; l <= x; l = r + 1){
            r = x/(x/l);
            ans += (r-l+1)*(x/l);
            
        }
        cout << ans << endl;
    }
}
    
signed main(){
    IOS();
    int T = 1;
//     cin>>T;
    while(T--){
        solve();
    }
}
------------------------------------------------------------------------------------------------------
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 1e6 + 10;
const int M = 1e3 + 10;

int n, q;
int a[N], aa[N];//a是原数组, aa是排序后的, 相当于维护了有序的块
//belong[i] 表示第i个元素属于第几块
int belong[N];

struct node{
    int l, r;
    int lazy;
}block[M];//维护每一个分块

void update_part(int j, int l, int r, int w){
    for(int i = l; i <= r; i++){
        a[i] += w;
    }
    l = block[j].l;
    int len = block[j].r - block[j].l + 1;
    memcpy(aa + l, a + l, sizeof(a[0]) * len);
    sort(aa + l, aa + l + len);
}

void update(int l, int r, int w){
    int b1 = belong[l], b2 = belong[r];
    if(b1 == b2){
        update_part(b1, l, r, w);
        return ;
    }
    for(int i = b1 + 1; i <= b2 - 1; i++){
        block[i].lazy += w;
    }
    update_part(b1, l, block[b1].r, w);
    update_part(b2, block[b2].l, r, w);
}

int query_part(int l, int r, int c){
    int ans = 0;
    for(int i = l; i <= r; i++){
        if(a[i] + block[belong[l]].lazy >= c) ans ++;
    }
    return ans;
}

int find(int j, int c){
    int l = block[j].l, r = block[j].r;
    int add = block[j].lazy;
    int idx = r + 1;
    while(l <= r){
        int mid = (l + r) >> 1;
        if(aa[mid] + add >= c){
            r = mid - 1;
            idx = mid;
        }
        else l = mid + 1;
    }
    return idx;
}

// 查询区间 >= c 的个数
int query(int l, int r, int c){
    int b1 = belong[l], b2 = belong[r];
    int ans = 0;
    if(b1 == b2){
        return query_part(l, r, c);
    }

    for(int i = b1 + 1; i <= b2 - 1; i++){
        ans += block[i].r - find(i, c) + 1;
    }
    return ans + query_part(l, block[b1].r, c) + query_part(block[b2].l, r, c);

}

void solve(){
    cin >> n >> q;
    for(int i = 1; i <= n; i++){
        cin >> a[i];
        aa[i] = a[i];
    }
    int len = sqrt(n);//每一块的大小
    for(int i = 1; i <= n; i++){
        belong[i] = (i - 1) / len + 1;
    }
    int cnt = belong[n];//块的个数
    for(int i = 1; i <= cnt; i++){
        block[i].l = (i - 1) * len + 1;
        block[i].r = min(i * len, n);
        sort(aa + block[i].l, aa + block[i].r + 1);
    }
    while(q--){
        char op;
        int l, r, w;
        cin >> op >> l >> r >> w;
        if(op == 'M'){
            update(l, r, w);
        }
        else{
            cout << query(l, r, w) << endl;            
        }
    }
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 5.7 约数个数

```cpp
#include<bits/stdc++.h>
const int MAXN=1e6+10;
using namespace std;
vector<int>pri;
bool flag[MAXN];
int d[MAXN],num[MAXN];
void pre(int n){
    d[1]=1;
    for(int i=2;i<=n;i++){
        if(!flag[i]){
            pri.push_back(i);
            d[i]=2;
            num[i]=1;
        }
        for(auto pri_j:pri){
            if(i*pri_j>n)break;
            flag[i*pri_j]=true;
            if(i%pri_j==0){
                num[i*pri_j]=num[i]+1;
                d[i*pri_j]=d[i]/num[i*pri_j]*(num[i*pri_j]+1);
                break;
            }
            num[i*pri_j]=1;
            d[i*pri_j]=d[i]*2;
        }
    }
}
signed main(){
    pre(100);
    cout<<d[9];
    return 0;
}
```

## 5.8 试除法

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int MAXN=1e7;
int n;

void solve(){
    cin>>n;
    int num=sqrt(n);
    for(int i=2; i <= num; i++){
        if(n == 1) break;
        while(n%i == 0){
            n/=i;
            cout<<i<<" ";
        }
    }
    if(n!=1) cout<<n;
    cout<<endl;
}

signed main(){
    int T;
    cin>>T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 5.9 规律

```cpp
卡特兰数
递推公式 : f[i] = 2*(2*n - 1) / (n + 1) * f[i - 1], f[0] = 1;
通项公式 : f[i] = C(n, 2 * n) / (n + 1) = C(2 * n, n) - C(2 * n, n - 1), C是组合数

斯特林数
通项公式 : {n, k} = {n - 1, k - 1} + k * {n - 1, k}, {n, k}为第n行第k列的数, 非法位置到的数为0

错位排列
a1 = 0, a2 = 1;
ai = (ai-1 + ai-2) * (i - 1), i >= 3

1/n的前n项和为loge(n)

lcm(a, b) = ∏i(1~n)pi^(max(ei, fi))
gcd(a, b) = ∏i(1~n)pi^(min(ei, fi))

两点之间曼哈顿距离
d = abs(x1 - x2) + abs(y1 - y2)
只有两种情况abs((x1 + y1) - (x2 + y2)) || abs((x1 - y1) - (x2 - y2))

容斥原理
求集合并集, A∪B∪C = (A + B + C) - (A∩B + A∩C + B∩C) + A∩B∩C
加 “奇数个集合的交集”, 减 “偶数个集合的交集”

对于一组序列, 交换两个不同的数字的位置, 则改变逆序对总数的奇偶性

min(u, v) = (u + v) / 2 - |u - v| / 2

取整规则
向上取整:
i128 x1 = y / x;
i128 re = y % x;
if(re && ((re > 0) == (x > 0))) x1++;
向下取整:
i128 x1 = y / x;
i128 re = y % x;
if(re && ((re > 0) != (x > 0))) x1--;
```

## 5.10 逆序对

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 5e5 + 10;

int a[N],  tree[N];
int n, cnt;

int lowbit(int x){
    return x&-x;
}

void update(int x){
    for(int i = x; i <= n; i += lowbit(i)){
        tree[i] ++;
    }
}

int sum(int r){
    if(r == 0) return 0;
    int ans = 0;
    for(int i = r; i > 0; i -= lowbit(i)){
        ans += tree[i];
    }
    return ans;
}

int query(int l, int r){
    return sum(r) - sum(l-1);
}

void solve(){
    cin >> n;
    int ans = 0;
    map<int, int>mp;
    for(int i = 1; i <= n; i++){
        cin >> a[i];
        mp[a[i]];
    }
    for(auto &[x, y] : mp){
        y = ++cnt;
    }
    for(int i = n; i >= 1; i--){
        int idx = mp[a[i]];
        ans += sum(idx - 1);
        update(idx);
    }
    cout << ans << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 5.11 莫队

```cpp
//时间复杂度O(n√n)
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 2e5 + 10;

struct Q{
    int l, r, idx;
}q[N];//离线操作

int n, m, res;
int a[N], block[N], ans[N], mp[N];

//加点对区间的影响
void Add(int i){
    int cnt = mp[a[i]]++;
    res += cnt * (cnt - 1) / 2;
}

//减点对区间的影响
void Sub(int i){
    int cnt = mp[a[i]]--;
    res -= (cnt - 1) * (cnt - 2) / 2;
}

void solve(){
    cin >> n >> m;
    for(int i = 1; i <= n; i++){
        cin >> a[i];
    }
	//分块
    int len = sqrt(n);
    for(int i = 1; i <= n; i++){
        block[i] = (i - 1) / len + 1;
    }
    for(int i = 1; i <= m; i++){
        cin >> q[i].l >> q[i].r;
        q[i].idx = i;
    }
	//左端点在一个块内就按右端点排序，否则按左端点所属块排序
    sort(q + 1, q + m + 1, [](const Q& x, const Q& y){
        return block[x.l] == block[y.l] ? x.r < y.r : block[x.l] < block[y.l];
    });    
    //维护一个区间[l, r]
    int l = 1, r = 0;
    for(int i = 1; i <= m; i++){
        //每次只需要加点或减点, 看该点对区间的影响
        while(l > q[i].l) Add(--l);
        while(r < q[i].r) Add(++r);
        while(l < q[i].l) Sub(l++);
        while(r > q[i].r) Sub(r--);
        ans[q[i].idx] = res; 
    }
    for(int i = 1; i <= m; i++){
        cout << ans[i] << endl;
    }
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 5.12 FFT

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
#define double long double
const int N = 4e5 + 10;
const double PI = acos(-1);

struct cp{
    double x, y;
    cp (double xx = 0, double yy = 0) : x(xx), y(yy) {}
    cp operator + (const cp& b) {return cp(x + b.x, y + b.y);}
    cp operator - (const cp& b) {return cp(x - b.x, y - b.y);}
    cp operator * (const cp& b) {return cp(x * b.x - y * b.y, x * b.y + y * b.x);}
};

int rev[N], l;
int limit;

void init(){
    rev[0] = 0;
    // 在原序列中 i 与 i/2 的关系是 ： i可以看做是i/2的二进制上的每一位左移一位得来
    // 那么在反转后的数组中就需要右移一位，同时特殊处理一下奇数
    for(int i = 0; i < limit; i++){
        rev[i] = (rev[i >> 1] >> 1) | ((i&1) << (l - 1));
    }
}

void fft(vector<cp>& A, int op){
    for(int i = 0; i < limit; i++){ //求出要迭代的序列
        if(i < rev[i]) swap(A[i], A[rev[i]]);
    }
    for(int len = 1; len < limit; len <<= 1){ //待合并区间的长度的一半
        cp Wn(cos(PI / len), op * sin(PI / len)); //单位根
        for(int i = len << 1, j = 0; j < limit; j += i){ //i是区间的长度，j表示前已经到哪个位置了
            cp w(1, 0); //幂
            for(int k = 0; k < len; k++, w = w * Wn){ //枚举左半部分
                cp x = A[j + k], y = w * A[j + len + k]; //蝴蝶效应
                A[j + k] = x + y;
                A[j + len + k] = x - y;
            }
        }
    }
}

void solve(){
    string s1, s2; cin >> s1 >> s2;
    int n = s1.size(), m = s2.size();
    reverse(s1.begin(), s1.end());
    reverse(s2.begin(), s2.end());
    limit = 1, l = 0;
    while(limit <= n + m - 2) limit <<= 1, l++;
    init();

    vector<cp>a(limit + 10), b(limit + 10);
    for(int i = 0; i < n; i++) a[i].x = (double)(s1[i] - '0');
    for(int i = 0; i < m; i++) b[i].x = (double)(s2[i] - '0');

    fft(a, 1), fft(b, 1);
    for(int i = 0; i < limit; i++) a[i] = a[i] * b[i];
    fft(a, -1);
    vector<int>ans(limit + 110);
    for(int i = 0; i <= n + m - 2; i++) ans[i] = (int)(a[i].x / limit + 0.5); //四舍五入
    
    int r = n + m - 2;
//     for(int i = 0; i <= r; i++) cout << ans[i];
//     cout << endl;
    for(int i = 0; i <= r + 100; i++){
        int x1 = ans[i] / 2;
        ans[i + 2] -= x1;
        ans[i] %= 2;
        if(ans[i] == -1) ans[i] = 1, ans[i + 2]++;
    }    

    int mark = 0;
    for(int i = r + 100; i >= 0; i--){
        if(ans[i]){
            mark = 1;
        }
        if(mark) cout << ans[i];
    }
    if(!mark) cout << 0;
    cout << endl;
}

signed main(){
    int T = 1;
    cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 5.13 高斯消元

```cpp
int n;
double a[N][N], b[N][N];

// 高斯消元, 时间复杂度O(n^3)
void Guass(){
    // 化成上三角矩阵
    for(int r = 1, c = 1; r <= n; r++, c++){
        int t = r;
        // 找主元
        for(int i = r + 1; i <= n; i++){
            if(fabs(b[i][c]) > fabs(b[t][c])) t = i;
        }

        // 交换第r行和第t行的元素
        for(int j = c; j <= n + 1; j++) swap(b[r][j], b[t][j]);

        // 主元归一(把当前行的主元消成1)
        for(int j = n + 1; j >= c; j--) b[r][j] /= b[r][c];

        // 消元(把下面所有行的第c列全部变成0)
        for(int i = r + 1; i <= n; i++){
            for(int j = n + 1; j >= c; j--){
                b[i][j] -= b[i][c] * b[r][j];
            }
        }
    }

    // 化成最简阶梯型矩阵(本题唯一解, 即对角矩阵)
    for(int i = n; i > 1; i--){
        for(int j = i - 1; j >= 1; j--){
            b[j][n + 1] -= b[i][n + 1] * b[j][i];
            b[j][i] = 0;
        }
    }
}

// 异或高斯消元
// int Gauss(){
//     int r, c;
//     for(r = 1, c = 1; c <= n; c++){
//         int t = r;
//         // 找主元
//         for(int i = r + 1; i <= n; i++){
//             if(a[i][c]) t = i;
//         }
//         if(!a[t][c]) continue;

//         // 交换
//         for(int j = c; j <= n + 1; j++) swap(a[r][j], a[t][j]);

//         // 消元
//         for(int i = r + 1; i <= n; i++){
//             for(int j = n + 1; j >= c; j--){
//                 a[i][j] ^= a[i][c] & a[r][j];
//             }
//         }
//         r++;
//     }

//     int res = 1;
//     if(r < n + 1){
//         for(int i = r; i <= n; i++){
//             if(a[i][n + 1]) return -1; // 出现0 == ！0即无解
//             res *= 2; // 否则每一个自由元有两种取值
//         }
//     }

//     return res;
// }

void solve(){
    cin >> n;
    for(int i = 0; i <= n; i++){
        for(int j = 1; j <= n; j++) cin >> a[i][j];
    }

    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            b[i][j] = 2 * (a[i][j] - a[0][j]);
            b[i][n + 1] += a[i][j] * a[i][j] - a[0][j] * a[0][j];
        }
    }

    Guass();
    cout << fixed << setprecision(3);
    for(int i = 1; i <= n; i++) cout << b[i][n + 1] << " \n"[i == n];

}
```

## 5.14 SG函数

```cpp
// 常用于DAG图
int sg[N]; // 记忆化数组，存储每个节点的 SG 值
// 定义：SG(x) = mex({ SG(y) | x -> y }), 其中 x -> y 表示x -> y的一条有向边。
// SG(x)不为0则表示x->终点先手必胜, 反之则败
// 多个起点则G0 = SG(x1) ^ SG(x2) ^ ... ^ SG(xk), G0不为0则先手必胜, 反之则败
// 这里的 f(u) 就是在递归求解这个公式

int f(int u){
    // 如果已经计算过该点的 SG 值，直接返回（记忆化）
    if(sg[u] != -1) return sg[u];

    set<int> st; // 存储所有后继节点的 SG 值
    for(auto v : g[u]){
        st.insert(f(v)); // 递归计算每一个能到达的点的 SG 值
    }
    // 计算 mex (Minimum Excluded value)
    // 找到集合 st 中最小的未出现的非负整数
    int mex = 0;
    for(auto x : st){
        if(x == mex) mex++; 
        else break;         
    }
    return sg[u] = mex;
}
```



<div style="page-break-after: always;"></div>

# 6 DP大类

## 6.1 多重背包

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 2e4 + 10;

int n, m;
int dp[N], last[N];
int q[N];//单调队列，存体积

void solve(){
    cin >> n >> m;
    //单调队列优化多重背包
    for(int i = 1; i <= n; i++){
        int v, w, s;
        cin >> v >> w >> s;
        //按余数分组
        for(int j = 0; j < v; j++){

            int hh = 1, tt = 0;//头尾指针
            for(int k = j; k <= m; k += v){
                //滑动窗口
                if(hh <= tt && q[hh] < k - s * v) hh++;
                if(hh <= tt ) dp[k] = max(dp[k], last[q[hh]] + (k - q[hh]) / v * w) ;
                //减去偏移量, 消除k的影响
                while(hh <= tt && last[q[tt]] - (q[tt] - j) / v * w <= last[k] - (k - j) / v* w) tt--;
                q[++tt] = k;
            }
        }
        //记录dp[i-1]为last
        memcpy(last, dp, sizeof dp);
    }  

    // //二进制优化多重背包, 相当于把s个物品分成log(s)个物品再01背包
    // for(int i = 1; i <= n; i++){
    //     int v, w, s;
    //     cin >> v >> w >> s;
        
    //     for(int k = 1; k <= s; k *= 2){
    //         for(int j = m; j >= k * v; j--){
    //             dp[j] = max(dp[j], dp[j - k * v] + k * w);

    //         }
    //         s -= k;
    //     }

    //     if(s){
    //         for(int j = m; j >= s * v; j--){
    //             dp[j] = max(dp[j], dp[j - s * v] + s * w);
    //         }
    //     }    
    // }     
    cout << dp[m] << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.2 区间dp

```cpp
//P1880 石子合并
#include <bits/stdc++.h>
using namespace std;
const int MAXN = 2*100 + 10;

//区间 DP 常用模版
// for (int len = 1; len <= n; len++) {         // 区间长度
//     for (int l = 1; l + len - 1 <= n; l++) { // 枚举起点
//         int r = i + len - 1;                 // 区间终点
//         if (len == 1) {
//             dp[l][r] = 初始值
//             continue;
//         }

//         for (int k = l; k < r; k++) {        // 枚举分割点，构造状态转移方程
//             dp[l][r] = min(dp[l][r], dp[l][k] + dp[k + 1][r] + w[l][r]);
//         }
//     }
// }

int n;
int a[MAXN];
int pre[MAXN];
int dp1[MAXN][MAXN];
int dp2[MAXN][MAXN];

//时间复杂度O(n^3)
void solve(){
    cin >> n;
    for(int i = 1; i <= n; i++){
        cin >> a[i];
        a[i+n] = a[i];
    }
    for(int i = 1; i <= 2*n; i++){
        pre[i] = pre[i-1] + a[i];
    }
    memset(dp1, 0x3f, sizeof(dp1));
    memset(dp2, -0x3f, sizeof(dp2));
    // cout << dp2[0][0] << endl;
    int ans1 = INT_MAX, ans2 = INT_MIN;
    for(int len = 1; len <= n; len++){
        for(int i = 1; i <= 2*n - len + 1; i++){
            int j = i + len - 1;
            //初始化
            if(len == 1){
                dp1[i][i] = 0;
                dp2[i][i] = 0;
                continue;
            }
            for(int k = i; k < j; k++){
                dp1[i][j] = min(dp1[i][j], dp1[i][k] + dp1[k+1][j] + pre[j] - pre[i-1]);
                dp2[i][j] = max(dp2[i][j], dp2[i][k] + dp2[k+1][j] + pre[j] - pre[i-1]);
            }
            if(len == n) ans1 = min(ans1, dp1[i][j]), ans2 = max(ans2, dp2[i][j]);
        }       
    }
    cout << ans1 << endl << ans2 << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.3 最长上升子序列（贪心优化）

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 1e6 + 10;
const int M = 2e5 + 10;

int a[N], b[N];
int len;

int find(int x){
    int l = 1, r = len;
    int ans = 0;
    while(l <= r){
        int mid = (l + r) >> 1;
        if(b[mid] >= x){
            ans = mid;
            r = mid - 1; 
        }
        else l = mid + 1;
    }
    return ans;
}

void solve(){
    int n;
    cin >> n;
    for(int i = 1; i <= n; i++){
        cin >> a[i];
    }
    for(int i = 1; i <= n; i++){
        if(a[i] > b[len]){
            b[++len] = a[i];
        }
        else{
            int j = find(a[i]);
            b[j] = a[i];
        }
    }
    cout << len << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.4 最长公共子序列（贪心优化）

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long 
const int N = 1e6 + 10;
const int M = 2e5 + 10;

int n;
int a[N], b[N], c[N], mp[N];
int len;

int find(int x){
    int l = 1, r = len;
    int ans = 0;
    while(l <= r){
        int mid = (l + r) >> 1;
        if(c[mid] >= x){
            ans = mid;
            r = mid - 1;
        }
        else l = mid + 1;
    }
    return ans;
}

void solve(){
    cin >> n;
    //a[i]里的数都不重复
    for(int i = 1; i <= n; i++){
        cin >> a[i];
        mp[a[i]] = i;
    }      
    //让b[i]等于它在a[i]对应的下标, 没有就是下标0
    for(int i = 1 ; i <= n; i++){
        cin >> b[i];
        b[i] = mp[b[i]];
    }
    for(int i = 1; i <= n; i++){
        if(b[i] == 0) continue;
        if(b[i] >= c[len]) c[++len] = b[i];
        else{
            int idx = find(b[i]);
            c[idx] = b[i];
        }
    }
    cout << len << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.5 最长公共上升子序列

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 3e3 + 10;

void IOS(){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
}

int n;
int a[N], b[N];
int dp[N][N]; // a前i, b以j结尾的最长公共子序列长度

void solve(){
    cin >> n;
    for(int i = 1; i <= n; i++) cin >> a[i];
    for(int i = 1; i <= n; i++) cin >> b[i];
    // 时间复杂度O(n^3)
    int ans = 0;
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            dp[i][j] = dp[i - 1][j];
            if(a[i] != b[j]) continue;
            int mx = 1;
            for(int k = 1; k < j; k++){
                if(b[j] > b[k])
                mx = max(mx, dp[i - 1][k] + 1);
            }
            dp[i][j] = max(dp[i][j], mx);
            ans = max(ans, dp[i][j]);
        }
    }
    cout << ans << endl;

    // 时间复杂度O(n^2)
    int ans = 0;
    for(int i = 1; i <= n; i++){
        int mx = 1;
        for(int j = 1; j <= n; j++){
            dp[i][j] = dp[i - 1][j];
            if(a[i] == b[j]) dp[i][j] = max(dp[i - 1][j], mx);
            if(b[j] < a[i]) mx = max(mx, dp[i - 1][j] + 1);
            ans = max(ans, dp[i][j]);
        }
    }
    cout << ans << endl;
    
}

signed main(){
    IOS();
    int T = 1;
    // cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.6 状压dp

```cpp
//p2831 互不侵犯
//状压dp常用状态: dp[当前集合][当前状态]
#include <bits/stdc++.h>
using namespace std;
#define int long long
//交互题记得注释掉
#define endl "\n"
const int N = 10 + 5;
const int M = 2e5 + 10;

//dp[i][j][state] 表示前i行, j个国王位置确定, 第i行的状态为state的方案总数
int dp[N][N * N][1ll << N];
int n, m;
// 预处理cnt[i], i里面1的个数
int cnt[1ll << N]; 
// g[i] 表示第i个状态时,上一行的合法状态的集合, state表示一行合法状态集合
vector<int> g[1ll << N], state;

bool check(int x){
    for(int i = 0; i < n; i++){
        if((x >> i & 1) && (x >> i + 1 & 1)) return 0;
    }
    return 1;
}

int count(int x){ // x里1的个数
    int tot = 0;
    for(int i = 0; i < n; i++){
        if(x >> i & 1) tot ++;
    }
    return tot;
}

void solve(){
    cin >> n >> m;
    for(int i = 0; i < 1ll << n; i++){
        if(check(i)){
            cnt[i] = count(i);
            state.push_back(i); // 存合法状态
        }
    }

    for(int i = 0; i < state.size(); i++){
        for(int j = 0; j < state.size(); j++){
            int a = state[i], b = state[j];
            //a & b保证上下没有相邻的1, check保证a,b没有连续2个1并且4个对角也没有1
            if((a & b) == 0 && check(a | b)){
                g[i].push_back(j);
            }
        }
    }
    int ans = 0;
    dp[0][0][0] = 1;
    for(int i = 1; i <= n + 1; i++){
        for(int j = 0; j <= m; j++){
            for(int k = 0; k < state.size(); k++){
                int a = state[k];
                if(j >= cnt[a]) //个数限制
                    for(auto l : g[k]) dp[i][j][k] += dp[i - 1][j - cnt[a]][l];
                if(i == n && j == m) ans += dp[n][m][k];
            }
        }
    }
    // cout << dp[n + 1][m][0] << endl;//也可以这样
    cout << ans << endl; 
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.7 期望dp

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 2e5 + 10;

int n;
double x1[N], x2[N], dp[N];
//x1[i]表示以i结尾的连续1的长度的期望, 转移方程 x1[i] = (x1[i - 1] + 1) * pi
//x2[i]表示以i结尾的连续1的长度的平方的期望, 转移方程 x2[i] = (x2[i - 1] + 2 * x1[i - 1] + 1) * pi;
//dp[i]表示以1~i的总期望, 转移方程 dp[i] = dp[i - 1] + (3 * x2[i - 1] + 3 * x1[i - 1] + 1) * pi;
//增量 (x + 1)^3 - x^3 = 3*x^2 + 3*x + 1;

void solve(){
    cin >> n;
    double p;
    for(int i = 1; i <= n; i++){
        cin >> p;
        x1[i] = (x1[i - 1] + 1) * p;
        x2[i] = (x2[i - 1] + 2 * x1[i - 1] + 1) * p;
        dp[i] = dp[i - 1] + (3 * x2[i - 1] + 3 * x1[i - 1] + 1) * p;
    }    
    cout << fixed << setprecision(1) << dp[n] << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.8 树形dp

```cpp
//P2015 二叉苹果树
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 100 + 10;

int n, m, ans;
vector<PII>g[N];
int dp[N][N];// dp[i][j]表示以i为根的子树, 选j个边的最大价值

void dfs(int u, int fa){ // 分组背包
    for(auto [v, w] : g[u]){// 物品
        if(v == fa) continue;
        dfs(v, u);
        for(int i = m; i > 0; i--){ // 体积
            for(int j = 0; j < i; j++){// 决策
                dp[u][i] = max(dp[u][i], dp[u][i - j - 1] + dp[v][j] + w);
            }
        }
    }
}

void solve(){
    cin >> n >> m;
    for(int i = 1; i < n; i++){
        int u, v, w;
        cin >> u >> v >> w;
        g[u].push_back({v, w});
        g[v].push_back({u, w});
    }    
    dfs(1, 0);
    cout << dp[1][m] << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.9 数位dp

```cpp
//P13085 windy数 
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 20;

// 做数位dp的时候考虑“树”形
int l, r;
int dp[N][10];//dp[i][j] 含前导零, i+1位(从0位开始的)数字, 第i位为j的所有合法数字的数量

void init(){
    for(int i = 0; i <= 9; i++) dp[0][i] = 1; 
    for(int i = 1; i < N; i++){
        for(int j = 0; j <= 9; j++){
            for(int k = 0; k <= 9; k++){
                if(abs(j - k) >= 2)
                dp[i][j] += dp[i - 1][k];
            }
            // cout << dp[i][j] << " \n"[j == 9];
        }
    }
}

int pre(int n){
    if(!n) return 0;
    vector<int>nums;
    while(n) nums.push_back(n % 10), n /= 10;
    n = nums.size();
    int ans = 0, last = -1;
    for(int i = n - 1; i >= 0; i--){
        int x = nums[i];
        for(int j = 0; j < x; j++){
            if(abs(j - last) >= 2)
                ans += dp[i][j];
        }
        
        if(abs(last - x) >= 2) last = x;
        else break; // 不合法的状态

        if(i == 0) ans++;
        // cout << ans << endl;
    }    

    for(int i = 0; i < n - 1; i++){ // 枚举低位并且首位不为零的数
        for(int j = 1; j <= 9; j++){
            ans += dp[i][j];
        }
    }
    return ans;
}

void solve(){
    cin >> l >> r;
    cout << pre(r) - pre(l - 1) << endl;
}

signed main(){
    init();
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

##  6.10 单调队列优化dp

```cpp
//acwing 1089. 烽火传递
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 5e5 + 10;

int n, m;
int w[N], dp[N], q[N];
// dp[i]表示选第i个烽火台, 前i个烽火台满足条件的最小花费

void solve(){
    cin >> n >> m;
    for(int i = 1; i <= n; i++){
        cin >> w[i];
    }    

    int hh = 0, tt = 0, ans = 1e18;
    for(int i = 1; i <= n; i++){
        if(q[hh] < i - m) hh++;
        dp[i] = dp[q[hh]] + w[i];
        while(hh <= tt && dp[q[tt]] >= dp[i]) tt--;
        q[++tt] = i;

    }
    // 从最后m个里至少选一个烽火台, 故取最后m个dp[i]即为答案
    for(int i = n - m + 1; i <= n; i++){ 
        ans = min(ans, dp[i]);
    }
    cout << ans << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.11 斜率优化dp

```cpp
// acwing 301.任务安排2
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 5e5 + 10;

int n, s;
int dp[N];
int t[N], c[N], q[N];

void solve(){
    cin >> n >> s;
    for(int i = 1; i <= n; i++){
        cin >> t[i] >> c[i];
        t[i] += t[i - 1]; // 前缀t
        c[i] += c[i - 1]; // 前缀c
    }    

    // 斜率优化dp, 根据dp[i]的转移dp[i] = t[i] * c[i] + s * c[n] + dp[j] - (s + t[i]) * c[j]
    // 将未知量dp[j], c[j]放在方程两边, 形成一次函数y = k * x + b
    // dp[j] = (s + t[i]) * c[j] + dp[i] - (t[i] + c[i] + s * c[n])
    // y = dp[j], k = (s + t[i]), x = c[j], b = dp[i] - (t[i] + c[i] + s * c[n])
    int hh = 0, tt = 0;
    q[0] = 0;
    for(int i = 1; i <= n; i++){
        // 队列里的斜率应该为严格单调递增
        // 去掉队头, k = (dp[q[hh + 1]] - dp[q[hh]]) / (c[q[hh + 1]] - c[q[hh]]) <= (t[i] + s)
        while(hh < tt && (dp[q[hh + 1]] - dp[q[hh]]) <= (t[i] + s) * (c[q[hh + 1]] - c[q[hh]])) hh++;
        int j = q[hh];

        // dp[i]的转移
        dp[i] = t[i] * c[i] + s * c[n] + dp[j] - (s + t[i]) * c[j];
        // 队尾斜率k1 >= k2 , 则弹出队尾元素, (dp[q[tt]] - dp[q[tt - 1]]) / (c[q[tt]] - c[q[tt - 1]]) >= (dp[i] - dp[q[tt]]) / (c[i] - c[q[tt]])
        while(hh < tt && (dp[q[tt]] - dp[q[tt - 1]]) * (c[i] - c[q[tt]]) >= (dp[i] - dp[q[tt]]) * (c[q[tt]] - c[q[tt - 1]])) tt--;
        q[++tt] = i;
    }

    cout << dp[n] << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.12 差值背包

```cpp
//https://ac.nowcoder.com/acm/contest/114806/M
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
using i64 = long long;
const int N = 3e4 + 10;

int n, w[N], v[N];
int dp[N];

void solve(){
    cin >> n;
    for(int i = 1; i <= n; i++){
        cin >> w[i];
    }
   
    for(int i = 1; i <= n; i++){
        cin >> v[i];
        v[i] = w[i] - v[i];
    }
    int offset = 1e4;
    memset(dp, -0x3f, sizeof dp);
    dp[offset] = 0;
    for(int i = 1; i <= n; i++){
        if(v[i] >= 0){
            for(int j = 2e4; j >= v[i]; j--){
                dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
            }
        }
        else{
            for(int j = 0; j <= 2e4; j++){
                dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
            }
        }
    }
    cout << dp[offset] << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.13 换根dp

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define double long double
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
const int N = 5e5 + 10;
const int M = 64;
const int mod = 998244353;

void IOS(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
}

int n;
vector<int>g[N];
int down[N][10], up[N][10];
// down[i][j]节点i子树里, 距离节点i有j步的点的个数
// up[i][j]节点i的祖先里, 距离节点i有j步的点的个数

void dfs1(int u, int fa){
    down[u][0] = 1;
    for(auto v : g[u]){
        if(v == fa) continue;
        dfs1(v, u);
        int x = v;
        for(int j = 1; j <= 9; j++){
            down[u][j] += down[v][j - 1];
        }
    }
}

void dfs2(int u, int fa){
//     up[u][0] = 1;
    for(auto v : g[u]){
        if(v == fa) continue;
        for(int j = 1; j <= 9; j++){
            if(j >= 1)
            up[v][j] += up[u][j - 1] + down[u][j - 1];
            if(j >= 2) up[v][j] -= down[v][j - 2];
        }
        dfs2(v, u);
    }
}

void solve(){
    cin >> n;
    for(int i = 1; i < n; i++){
        int u, v; cin >> u >> v;
        g[u].push_back(v);
        g[v].push_back(u);
    }
    
    dfs1(1, 0);
    dfs2(1, 0);
//     for(int i = 1; i <= n; i++){
//         for(int j = 0; j <= 9; j++){
//             cout << up[i][j] << " \n"[j == 9];
//         }
//     }
    for(int i = 1; i <= n; i++) cout << down[i][9] + up[i][9] << " ";
    
}

signed main(){
    IOS();
    int T = 1;
//     cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```

## 6.14 矩阵快速幂优化dp

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
#define PII pair<int, int>
#define x first
#define y second
#define double long double
const int N = 10 + 10;
const int M = 64;
const int mod = 998244353;

void IOS(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
}

int n, m, K, R;
int a[N], c[N], ack[1 << 6], cost[1 << 6];
// A是可达矩阵, G是答案矩阵, B是底数矩阵
int A[1 << 6][1 << 6], G[1 << 6][1 << 6], B[1 << 6][1 << 6];
int t[1 << 6][1 << 6];

// 矩阵乘法
void mul(int A1[][1 << 6], int A2[][1 << 6]){
    // t是临时数组, 用临时数组存答案然后再更新
    memset(t, 0, sizeof t); 
    for(int k = 0; k < (1 << n); k++){
        for(int i = 0; i < (1 << n); i++){
            for(int j = 0; j < (1 << n); j++){
                t[i][j] = max(t[i][j], A1[i][k] + A2[k][j]);
            }
        }
    }

    memcpy(A1, t, sizeof t);
}

void ksm(){
    while(R){
        if(R&1) mul(G, B);
        R >>= 1;
        mul(B, B);
    }
}

void solve(){
    cin >> n >> m >> K >> R;
    for(int i = 0; i < n; i++) cin >> a[i] >> c[i];

    for(int i = 0; i < (1ll << n); i++){
        ack[i] = cost[i] = 0;
        for(int j = 0; j < n; j++){
            if(i >> j & 1) ack[i] += a[j], cost[i] += c[j];
        }
        // cout << ack[i] << endl;
    }

    for(int i = 0; i < (1ll << n); i++){
        for(int j = 0; j < (1ll << n); j++){
            A[i][j] = G[i][j] = B[i][j] = 0;
            int cnt = 0;
            for(int k = 0; k < n; k++){
                if((j >> k & 1) && (i >> k & 1)) cnt++;
            }

            if(cost[j] + cnt * K <= m) A[i][j] = 1;
            else A[i][j] = 0;
            
            if(A[i][j]) B[i][j] = ack[j];
        }
    }

    ksm();
    int ans = 0;

    for(int j = 0; j < (1ll << n); j++){
        ans = max(ans, G[0][j]);
    }

    cout << ans << endl;
}

signed main(){
    IOS();
    int T = 1;
    cin >> T;
    while(T--){
        solve();
    }
    return 0;
}
```



<div style="page-break-after: always;"></div>

# 7 计算几何

## 7.1 凸包

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
const int N = 2e5 + 10;
struct VEX{
    double x, y;
    VEX(double xx = 0, double yy = 0) : x(xx), y(yy){}
    double operator* (const VEX & v2) const {
        return x * v2.x + y * v2.y;
    }
    double operator^ (const VEX & v2) const {
        return x * v2.y - y * v2.x;
    }
    VEX operator- (const VEX & v2) const {
        return VEX(x - v2.x, y - v2.y);
    }
    VEX operator+ (const VEX & v2) const {
        return VEX(x + v2.x, y + v2.y);
    }
    bool operator== (const VEX & v2) const {
        return x == v2.x && y == v2.y;
    }
};

double dis(const VEX &v1,const VEX &v2){
    VEX v = v1 - v2;
    return sqrt(v.x * v.x + v.y * v.y);
}

//按坐标排序
bool cmp(const VEX &v1, const VEX &v2){
    return (v1.x != v2.x ? v1.x < v2.x : v1.y > v2.y);
}

double cross(VEX &v1, VEX &v2, VEX &v3){
    return ((v2 - v1) ^ (v3 - v2));
}

int n;
VEX a[N], st[N];

//Andrew算法
double Andrew(){
    double ans = 0;//算凸包最小周长
    sort(a + 1, a + n + 1, cmp);
    int top = 0;
    for(int i = 1; i <= n; i++){
        while(top > 1 && cross(st[top - 1], st[top], a[i]) <= 0) top--;
        st[++top] = a[i];
    }
    int t = top;
    for(int i = n - 1; i >= 1; i--){
        while(top > t && cross(st[top - 1], st[top], a[i]) <= 0) top--;
        st[++top] = a[i];
    }

    for(int i = 1; i < top; i++){
        ans += dis(st[i], st[i + 1]);
    }

    return ans;
}

//极角排序, 用atan2需注意, 参数严格按向量来的atan2(y, x) != atan2(-y, -x)
//atan2值域[-PI, PI], 第3,4,1,2象限角度递增
bool cmp1(const VEX& v1, const VEX& v2){ 
    double ang1 = atan2(v1.y - a[1].y, v1.x - a[1].x), ang2 = atan2(v2.y - a[1].y, v2.x - a[1].x);
    if(ang1 - ang2 == 0) return dis(a[1], v1) < dis(a[1], v2);
    else return ang1 < ang2;
}

//用叉积写极角排序
bool cmp2(const VEX& v1, const VEX& v2){
    double cross = (v1 - a[1]) ^ (v2 - a[1]);
    if(cross == 0) return dis(v1, a[1]) < dis(v2, a[1]);
    return cross > 0;
}

//Graham算法
double Graham(){
    for(int i = 2; i <= n; i++){
        if(a[i].y < a[1].y || a[i].y == a[1].y && a[i].x < a[1].x){
            swap(a[i], a[1]);
        }
    }
    sort(a + 2, a + n + 1, cmp2);
    int top = 0;

    double ans = 0;
    for(int i = 1; i <= n; i++){
        while(top > 1 && cross(st[top - 1], st[top], a[i]) < 0) top--;
        st[++top] = a[i];
    }
    st[++top] = a[1];
    for(int i = 1; i < top; i++){
        ans += dis(st[i], st[i + 1]);
    }

    return ans;
}

void solve(){
    cin >> n;
    for(int i = 1; i <= n; i++){
        cin >> a[i].x >> a[i].y;
    }
    cout << fixed << setprecision(2) << Graham() << endl;
}

signed main(){
    int T = 1;
    while(T--){
        solve();
    }
    return 0;
}
```

<div style="font-size: 9px; text-align: center; margin-top: 10px;">


