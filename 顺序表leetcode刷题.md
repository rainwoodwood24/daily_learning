# 顺序表leetcode刷题

## 1、反转链表：leetcode——206

https://leetcode.cn/problems/reverse-linked-list/description/

1->2->3->4->5

反转：5->4->3->2->1

思路：遍历链表，每次将遍历到的链表插入到新链表的头结点后面

代码实现如下：

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
       ListNode new_head,*q; //为了降低编码难度，添加一个虚拟头结点new_head
       new_head.next=NULL;
        while(head){
            q=head->next;
            head->next=new_head.next;
            new_head.next=head;
            head=q;
        }
        return new_head.next;
    }
};
```

方法2：递归

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head==NULL||head->next==NULL) return head;
        ListNode *tail=head->next;
        ListNode *p=reverseList(head->next);
        head->next=tail->next;
        tail->next=head;
        return p;
    }
};
```



## 2、环形链表:leetcode——141

https://leetcode.cn/problems/linked-list-cycle/description/

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode *p=head,*q=head;
        while(q&&q->next){
            p=p->next;
            q=q->next->next;
            if(p==q) return true;
        }
        return false;
    }
};
```



## 3、快乐数：leetcode——202

https://leetcode.cn/problems/happy-number/description/

数据结构分为两个层面：

- 实现在程序中的具体结构
- 长在我们脑子里的长期训练的思维逻辑结构

将快乐数问题转化成最后能否指到NULL，进而转化为判断链表是否有环的问题

```c++
class Solution {
public:
    int getNext(int x){
        int y=0,n;
        while(x){
            n=x%10;
            y+=n*n;
            x/=10;
        }
        return y;
    }
    bool isHappy(int n) {
        int p=n,q=n;
        while(q!=1){
            p=getNext(p);
            q=getNext(getNext(q));
            if(p==q&&p!=1) return false;
        }
        return true;
    }
};
```



## 4、旋转链表：leetcode——61

https://leetcode.cn/problems/rotate-list/description/

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    int head_length(ListNode *head){
        int n=0;
        while(head){
            n++;
            head=head->next;
        }
        return n;
    }
    ListNode* rotateRight(ListNode* head, int k) {
        if(head==NULL) return head;
        int n=head_length(head);
        k=k%n;
        if(k==0) return head;
        int t=k+1;
        ListNode *p=head,*q=head;
        while(t--) p=p->next;
        while(p) p=p->next,q=q->next;
        p=q->next;
        q->next=NULL;
        ListNode *temp=p;
        while(temp->next!=NULL) temp=temp->next;
        temp->next=head;
        return p;
    }
};
```

自己想一下while(p)和while(p->next)的区别：

while(p):最后跳出循环的时候p为空



## 5、删除链表倒数第N个节点：leetcode——19

https://leetcode.cn/problems/remove-nth-node-from-end-of-list/

**双指针移动法+虚拟头结点**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode new_head,*p=&new_head,*q=p;
        new_head.next=head;
        int t=n+1;
        while(t--) p=p->next;
        while(p) p=p->next,q=q->next;
        q->next=q->next->next;
        return new_head.next;
    }
};
```



## 6、环形链表II：leetcode——142

https://leetcode.cn/problems/linked-list-cycle-ii/description/

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
       ListNode *p=head,*q=head;
        while(q&&q->next){
            p=p->next;
            q=q->next->next;
            if(p==q) break;
        }
        if(q==NULL||q->next==NULL)return NULL;
        p=head;
        while(p!=q)p=p->next,q=q->next;
        return p;
    }
};
```



## 7、反转链表：leetcode——92

**递归：此题对于理解递归函数有帮助**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if(left==1&&right==1) return head;
        if(left!=1){
            head->next=reverseBetween(head->next,left-1,right-1);
        }else{
            ListNode *tail=head->next,*new_head;
            new_head=reverseBetween(head->next,left,right-1);
            head->next=tail->next;
            tail->next=head;
            head=new_head;
        }return head;
    }
};
```

