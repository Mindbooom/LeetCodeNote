## Partition函数
源自快排中的partition，可以将数组中小于指定元素的元素与大于指定元素的元素分隔在该元素左右。
## Code:
```C++
    int partition(vector<int> input,int low,int high)
      {
        int pivotkey=input[low];   //pivot:枢纽
        //这里的pivotkey也可以是[low,high]区间一个随机数，也可以是三数取中，九数取中，详情见<<大话数据结构>>
        //int pivotkey=input[RandInRange(start,end)];
        while(low<high)
          {
            while(low<high&&pivotkey<input[high])
                high--;
            swap(&input[low],&input[high]);
            while(low<high&&pivotkey>=input[low])
                low++;
            swap(&input[low],&input[high]);
          } 
        return low;
      }
     
    /*这个partition是优化了不必要的交换，将swap用赋值替换
    int partition(vector<int> &input, int begin, int end)
     {
       int low = begin;
       int high = end;
       int pivot = input[low];
       while (low < high)
        {
          while (low < high&&pivot <= input[high])
             high--;
          input[low] = input[high];         //优化不必要的替换
          while (low < high&&pivot >= input[low])
             low++;
          input[high] = input[low];         //优化不必要的替换
        }
          input[low] = pivot;
          return low;
      }
    */
    ```
# 涉及题目：
[数组中出现次数大于一半的数字](https://github.com/Mindbooom/LeetCodeNote/blob/master/Problems_Not_From_LeetCode/%E5%89%91%E6%8C%87offer/%E6%95%B0%E7%BB%84%E4%B8%AD%E5%87%BA%E7%8E%B0%E6%AC%A1%E6%95%B0%E8%B6%85%E8%BF%87%E4%B8%80%E5%8D%8A%E7%9A%84%E6%95%B0.md)
[数组中最小的k个数](https://github.com/Mindbooom/LeetCodeNote/blob/master/Problems_Not_From_LeetCode/%E5%89%91%E6%8C%87offer/%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E6%9C%80%E5%B0%8Fk%E4%B8%AA%E6%95%B0.md)
