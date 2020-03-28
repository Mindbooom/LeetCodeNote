## Tag:
Greedy;Medium;
## Description:
There is a pile of n wooden sticks. The length and weight of each stick are known in advance. The sticks are to be processed by a woodworking machine in one by one fashion. It needs some time, called setup time, for the machine to prepare processing a stick. The setup times are associated with cleaning operations and changing tools and shapes in the machine. The setup times of the woodworking machine are given as follows:

(a) The setup time for the first wooden stick is 1 minute.
(b) Right after processing a stick of length l and weight w , the machine will need no setup time for a stick of length l' and weight w' if l<=l' and w<=w'. Otherwise, it will need 1 minute for setup.

You are to find the minimum setup time to process a given pile of n wooden sticks. For example, if you have five sticks whose pairs of length and weight are (4,9), (5,2), (2,1), (3,5), and (1,4), then the minimum setup time should be 2 minutes since there is a sequence of pairs (1,4), (3,5), (4,9), (2,1), (5,2).  
 Input:
 The input consists of T test cases. The number of test cases (T) is given in the first line of the input file. Each test case consists of two lines: The first line has an integer n , 1<=n<=5000, that represents the number of wooden sticks in the test case, and the second line contains n 2 positive integers l1, w1, l2, w2, ..., ln, wn, each of magnitude at most 10000 , where li and wi are the length and weight of the i th wooden stick, respectively. The 2n integers are delimited by one or more spaces.
 <br>
 Output:
 The output should contain the minimum setup time in minutes, one per line.  
 Sample Input
3   
5   
4 9 5 2 2 1 3 5 1 4   
3   
2 2 1 1 2 2   
3   
1 3 2 2 3 1  
 

Sample Output  
2  
1  
3  
## Solution:
```C++
//先排序再贪心
//排序的时候注意选择长度与重量的优先级
//先按照重量升序排序，然后对于每一个没有使用过的木棍，找后面长度与重量都大于它的木棍
//注意sort的cmp函数写法，a<b为升序,a>b为降序。
#include <stdio.h>
#include <string.h>
#include <algorithm>
using namespace std;
// 结构体保存木头
struct moodG {
    int len; // 长度
    int heavy; // 重量
    int valid; // 是否安装
}mood[5001];

//  重量优先 长度其次
//sort函数的cmp函数
bool cmp(moodG m1,moodG m2) {
    if(m1.heavy == m2.heavy)
        return m1.len<m2.len;
    return m1.heavy<m2.heavy;

}

int main() {
    int cas,n,i,j,k,t,tmp;
    scanf("%d",&cas);
    for(i=0; i<cas; i++) {
        scanf("%d",&n);
        t = 0;
        for(j=0; j<n; j++) {
            scanf("%d%d",&mood[j].len,&mood[j].heavy);
            mood[j].valid = 0; // 初始化
        }
        sort(mood, mood+n, cmp);  // 排序
        for(j=0; j<n; j++) {
            // 找到第一根需要1分钟安装的木头
            if(!mood[j].valid) {
                mood[j].valid = 1;
                t++;
                tmp = j;
                // 对此后每根长度>=L  宽度>=W的木头
                for(k=j+1; k<n; k++) {
                    if(!mood[k].valid && mood[tmp].len<=mood[k].len && mood[tmp].heavy<=mood[k].heavy) {
                        mood[k].valid = 1;
                        tmp = k;
                    }
                }
            }
        }
        printf("%d\n",t);
    }
    return 0;
}
```
## Thought：
From an online test of a company and HDU 1051. 
[HDU 1051](http://acm.hdu.edu.cn/showproblem.php?pid=1051)
