## Tag:
Easy;Double Pointer
## Description:
输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。
## Solution:
```c++
1.
//O(n)
//头尾指针往中间移动
//若当前值大于目标，尾指针左移
//若当前值小于目标，头指针右移
//另保存一个变量存储最小乘积与对应位置
class Solution {
public:
    vector<int> FindNumbersWithSum(vector<int> array,int sum) {
        vector<int>res;
        if(array.size()<2)return res;
        int left=0,right=array.size()-1;
        int tempAdd = array[0]+array.back();
        int tempPro=0;
        int leftBest = 0,rightBest=0;
        while(left<right)
        {
            if(tempAdd==sum)
            {
                if(tempPro==0||array[left]*array[right]<tempPro)
                {
                    tempPro=array[left]*array[right];
                        leftBest = left;
                        rightBest = right;
                        tempAdd-=array[left];
                        left++;
                }
                else
                {
                        tempAdd-=array[left];
                        left++;
                }
            }
            else if(tempAdd<sum)
            {
                tempAdd-=array[left];
                left++;
                tempAdd+=array[left];
            }
            else
            {
                tempAdd-=array[right];
                right--;
                tempAdd+=array[right];
            }
        }
        if(tempPro==0)return res;
        res.push_back(array[leftBest]);
        res.push_back(array[rightBest]);
        return res;
    }
};
2.
//简化方案
/*
数列满足递增，设两个头尾两个指针i和j，
若ai + aj == sum，就是答案（相差越远乘积越小）
若ai + aj > sum，aj肯定不是答案之一（前面已得出 i 前面的数已是不可能），j -= 1
若ai + aj < sum，ai肯定不是答案之一（前面已得出 j 后面的数已是不可能），i += 1
O(n)
*/
typedef vector<int> vi;
class Solution {
public:
    vi FindNumbersWithSum(const vi& a,int sum) {
        vi res;
        int n = a.size();
        int i = 0, j = n - 1;
        while(i < j){
            if(a[i] + a[j] == sum){
                res.push_back(a[i]);
                res.push_back(a[j]);
                break;
            }
            while(i < j && a[i] + a[j] > sum) --j;
            while(i < j && a[i] + a[j] < sum) ++i;
        }
        return res;
    }
};
```
