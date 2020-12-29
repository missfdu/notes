### [#2 Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

#### MySolution

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *p1=l1, *p2=l2, *p=new ListNode(), *head=p, *sp;
        int flow=0,sum=0;
        for(p1=l1,p2=l2;p1!=NULL&&p2!=NULL;p1=p1->next,p2=p2->next){
            sum=p1->val+p2->val+flow;
            if(sum>=10){
                flow=1;
                sum-=10;
            }
            else flow=0;
            p->val=sum;
            sp=p;
            p->next=new ListNode();
            p=p->next;
        }
        while(p1!=NULL){
            sum=p1->val+flow;
            if(sum>=10){
                flow=1;
                sum-=10;
            }
            else flow=0;
            p->val=sum;
            sp=p;
            p->next=new ListNode();
            p=p->next;
            p1=p1->next;
        }
        while(p2!=NULL){
            sum=p2->val+flow;
            if(sum>=10){
                flow=1;
                sum-=10;
            }
            else flow=0;
            p->val=sum;
            sp=p;
            p->next=new ListNode();
            p=p->next;
            p2=p2->next;
        }
        if(flow) p->val=1;
        if(!p->val)sp->next=nullptr;
        return head;
    }
};
```

Cons:

- not concise, even ugly

- use much memory

  

#### GoodSolution

```cpp
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(-1);
        ListNode l = dummyHead;
        int carry = 0;
        
        while(l1 != null || l2 != null) {
            int sum = carry;
            if(l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            
            if(l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }
            
            l.next = new ListNode(sum % 10);
            l = l.next;
            carry = sum / 10;
        }
        
        if(carry != 0) 
            l.next = new ListNode(carry);
        
        return dummyHead.next;
    }
}
```

Pros:

- simplify the procedure, only one loop (use OR instead of AND, so if one list is over, just keep it `null`)