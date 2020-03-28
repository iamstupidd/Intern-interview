# Tencent面试经历
这是我的第一次面试，有点丢人，挂在了一面，下来想想确实没有问什么难的问题，但是一紧张，人家问啥啥不会。真的是太菜了，开始重视基础吧。。。
## 流程
1. 提前一天打了电话，然后预约了时间
2. 到了时间打电话，邮箱里给了个腾讯文档，上面有四个题，不难，真的不难，而且优化都挺简单的。。。但是当时真的脑抽。。。
3. 约定完成时间，挂断电话，开始做，我约定了40min
4. 35min做完之后，开始针对每一道题出题问优化；
5. 题看完之后给了一道开放题。。。。真心不太会，问了点分布式，大数据，数据结构的问题。
# 题目以及当时写的内容
* 代码题（C/C++）
从非递减链表中去除重复的元素
举例：(1, 1, 3, 3, 3, 5, 5, 5, 9, 9, 9, 9) -> (1, 3, 5, 9).
struct LinkNode {
　　int val;
　　struct LinkNode * next;
};
实现这个函数。给出时间复杂度和空间复杂度。
~~~c++
LinkNode* UniqueOrderedList(LinkNode* head)
{
if(!head) return head;
LinkNode* pre = head , *tmp = head;
while(head->next){
//head = head->next;
if(head->val == pre->val){
LinkNode* tmp =head;
head = head->next;
delete tmp;// = NULL;
}
else{
pre->next = head;
pre = head;
}
}
return tmp;
}

O(n)
O(1)
~~~
* 代码题（C/C++）
给定两个自然数数组A和B，从A中任取一个元素a，从B中任取一个元素b。d=绝对值(a-b)，求d的最小值。A和B的长度都不为0
举例：A={ 1, 3, 2, 10}，B = {7, 13, 9, 13}，输出1（即10-9）
给出时间复杂度和空间复杂度。
~~~c++
int GetMinDiff(const std::vector<int>& A, const std::vector<int>& B)
{
vector<int> tmp_A = A,tmp_B=B;
sort( tmp_A.begin(), tmp_A.end());
sort( tmp_B.begin(), tmp_B.end());
int len_a = A.size(),len_b=B.size();
int res =  INT_MAX;
for(int i=0;i<len_a;i++){
for(int j=0;j<len_b;j++){
int tmp1=tmp_A[i]-tmp_B[j];
res = min(abs(tmp1),res);
if(tmp1<0) break;
}
}
return res;
}

O(n^2)
O(n)
~~~
* 代码题（C/C++）
找出uint32_t的二进制bit串中连续0的最大长度
举例：20202020二进制为00000001001101000100001000100100，连续0的最大长度为7
给出时间复杂度和空间复杂度。
~~~c++
int max_continuous_zero_length(uint32_t x)
{
uint32_t  tmp = 1;
int max_len = INT_MIN;
int count = 1,len=0;
while(count++<=32){
int curtmp = x & tmp;
if(!curtmp){
len++;
}
else{
max_len = max(max_len,len);
len=0;
}
x>>1;
}
max_len = max(max_len,len);
return max_len;
}

O(1)
O(1)
~~~
* 代码题（C/C++）
从int矩阵的左上角移动到右下角，每次可以向右、向下或者向右下移动一次。求移动路径上数字之和的最大值。
举例：矩阵 = 
[
  0, -2, 1, 2,
  3, 1, 0, -1,
  4, -2, 3, 0
]
最大和为8，即0+3+4-2+3+0
给出时间复杂度和空间复杂度。
~~~c++
int MaxSum(const std::vector< std::vector<int> >& M)
{
if(!M.size() || !M[0].size()) return 0;
int col_len = M.size(),row_len =M[0].size();
int[][] dp = new int[col_len][row_len];
dp[0][0] = M[0][0];
for(int i=0;i<col_len;i++){
for(int j=0;j<row_len;j++){
if(i==0&&j==0) continue;
else if(i==0){
dp[i][j] = dp[i][j-1]+M[i][j];
}
else if(j==0){
dp[i][j]= dp[i-1][j] + M[i][j];
}
else{
int tmp1 = dp[i-1][j]+ M[i][j],tmp2 = dp[i][j-1]+M[i][j],tmp3 = 	dp[i-1][j-1]+M[i][j];
dp[i][j] = max(tmp1,tmp2);
dp[i][j] = max(dp[i][j],tmp3);
}
}
}
return dp[col_len-1][row_len-1];  
}
O(n^2)
O(n^2)
~~~

设计一个短链服务，可以将长URL转换为短URL。要求如下：
    a) 任意的长URL得到一个短URL
    b) 可以根据短URL查询长URL
    c) 短URL的格式为http://t.cn/X 其中X是由0-9、a-z、A-Z组成的长度为8的字符串，比如http://t.cn/4X8hfgDk
    d) 系统需要存储200亿的URL。
给出接口定义和每个接口的实现思路，不必实现代码，可以使用伪代码帮助表达。

## 各个问题问的具体的题
1. 如何释放指针？malloc,new,delete,free有什么区别？
2. 优化，在提示下想到了，排序后O(n)
3. 位运算
4. 动规，就是空间复杂度太高了，可以O(n)
5. hashmap的底层原理，分布式，数据库，磁盘和内存的映射关系。