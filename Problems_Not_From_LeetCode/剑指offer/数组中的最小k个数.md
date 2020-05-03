## Tag :
Medium;array;
## Description :
输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4。
## Solution :
```c++
1.
//set与multiset实现结构为红黑树。配合排序函数，可以当做最大堆使用。
//当堆中不满k个，则添加进去
//当已经有k个元素，与最大元素比较，若小于则删除最大元素，进堆。若大于则不管。
class Solution {
public:
    typedef multiset<int,greater<int>> intSet;
    typedef multiset<int,greater<int>>::iterator setIterator;
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        int length = input.size();
        if(length<k)return {};
        intSet resSet;
        vector<int> res;
        vector<int>::iterator ite = input.begin();
        for(;ite!=input.end();ite++)
        {
            if(resSet.size()<k)
                resSet.insert(*ite);
            else
            {
                if(*ite<*resSet.begin())
                {
                    resSet.erase(*resSet.begin());
                    resSet.insert(*ite);
                }
            }
        }
        setIterator setIte = resSet.begin();
        for(;setIte!=resSet.end();setIte++)
        {
            res.push_back(*setIte);
        }
        return res;
    }
};
2.
//使用partition函数辅助
class Solution {
public:
    int partition(vector<int>& input,int low,int high)
      {
        int pivotkey=input[low];   //pivot:枢纽
        //这里的pivotkey也可以是[low,high]区间一个随机数，也可以是三数取中，九数取中，详情见<<大话数据结构>>
        //int pivotkey=input[RandInRange(start,end)];
        while(low<high)
          {
            while(low<high&&pivotkey<input[high])
                high--;
            swap(input[low],input[high]);
            while(low<high&&pivotkey>=input[low])
                low++;
            swap(input[low],input[high]);
          }
        return low;
      }
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        int length = input.size();
        if(length<k||k<1)return {};
         
        int start = 0;
        int end = length-1;
        int index = partition(input,0,end);
        while(index!=k-1)//找到第k个
        {
            if(index>k-1)
            {
                end = index-1;
                index = partition(input,start,end);
            }
            else
            {
                start = index+1;
                index = partition(input,start,end);
            }
        }
        vector<int> res(input.begin(),input.begin()+k);
        return res;
    }
};
```
