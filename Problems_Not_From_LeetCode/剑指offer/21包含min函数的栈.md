## Tag:
Stack;Easy;divergent thinking；

## Description：
Define a data structure of stack while implementing a 'min' function to get the minist element in the stack. The time complexity should be O(n1).

## Solution:
```C++
//刚开始想到用一个指针指向最小值，但是若该最小值弹出就找不到次小值。
//所以需要保存次小值，进而需要保存所有状态下的最小值。
//也就是多一个栈来对应存储每个原始栈不同状态下的最小值。
//一同弹出，一同压入，辅助栈压入原始栈当前最小值。
class Solution {
public:
    stack<int>mainSta;
    stack<int>affSta;
    void push(int value) {
        mainSta.push(value);
        if(affSta.size())
            affSta.push(value<affSta.top()?value:affSta.top());
        else
            affSta.push(value);
        
    }
    void pop() {
        mainSta.pop();
        affSta.pop();
    }
    int top() {
        return mainSta.top();
    }
    int min() {
        return affSta.top();
    }
};
```
