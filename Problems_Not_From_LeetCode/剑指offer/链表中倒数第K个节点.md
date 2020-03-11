## Tag:
Linked list;Easy;
## Description:
Given a linked list and a number k, output the k-th node from the bottom.
## Solution:
```c++
//使用快慢指针，快指针先走k步，然后快慢指针一起走，当快指针走到末尾时满指针到达倒数第k个节点。
//注意关注特殊情况，如空指针输入，k大于节点数
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
        if(k<1||!pListHead)return nullptr;
        ListNode* slow=pListHead;
        ListNode* fast=pListHead;
        for(int i=1;i<=k;i++ )
        {
            if(!fast)return nullptr;
            fast = fast->next;
        }
        while(fast)
        {
            fast = fast->next;
            slow = slow->next;
        }
                  return slow;
    }
};
```
