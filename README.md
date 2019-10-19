# x80H
基于x80H移动机器人的上位机软件开发（C#）
删除链表的倒数第N个节点
方法一
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if(head==NULL)
            return head;
        
        //遍历链表，求链表长度lenth
        int lenth=1;
        ListNode *p=head;
        while(p->next!=NULL)
        {
            ++lenth;
            p=p->next;
        }
        
       //遍历链表的倒数第n个节点
        ListNode *goal=head;
        ListNode *last=NULL;
        int i=0;
        while(i<(lenth-n)&&goal->next!=NULL)
        {
            last=goal;
            goal=goal->next;
            i++;
        }
              
        if (i==0)    //删除节点在起始位置
        {
            head=goal->next;
            delete goal;
            return head;
        }
      
        else//删除节点在中间其他位置
        {
            last->next=goal->next;
            delete goal;
            return head;
        }  
    }
};
方法二双指针法
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        
            if(head==NULL)
            return head;
        
    
           
            ListNode * slow=head;
            ListNode * fast=head;
            for(int i=0;i<n;i++)
                fast=fast->next;
            if(!fast)//删除结点在起始位置情况
            {
                head=head->next;
                return head;
            }
           //删除结点在其他位置情况
            while(fast->next)
            {
                slow=slow->next;
                fast=fast->next;
            }
            slow->next=slow->next->next;
            return head;
    }
};
