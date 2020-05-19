## Tag:
Medium;doublepointer
## Description:
小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!
## Solution:
```c++
//O(n)
//使用双指针法，前后移动。
//当前值小于目标，右指针右移
//当前值大于目标，左指针右移
class Solution {
public:
    vector<vector<int> > FindContinuousSequence(int sum) {
        vector<vector<int>> res;
        if(sum<2)return {};
        int left=1,right=2;
        int temp = 3;
        while(left<(1+sum)/2)
        {
            if(temp==sum)
            {
                vector<int>tempVec;
                for(int i =left;i<=right;i++)
                    tempVec.push_back(i);
                res.push_back(tempVec);
                temp-=left;
                left++;
                
            }
            else if (temp<sum)
            {
                right++;
                temp+=right;
            }
            else
            {
                temp-=left;
                left++;
            }
        }
        return res;
    }
};
```
