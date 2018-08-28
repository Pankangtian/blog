---
title: 【剑指offer】  输出倒数第k个结点以及逆转指针
date: 2018-08-21 19:16:15
tags: [array] 
categories: [剑指offer]    

---

1、输入一个链表，输出该链表中倒数第k个结点。

	public ListNode FindKthToTail(ListNode head,int k) {
        ListNode tem=head;//缓根节点
        while (k>0&tem!=null) { //tem 先行到k处
            tem = tem.next;
            k--;
        }
        if(k!=0)
            return null;
        while (tem!=null){//head和tem一起向下走，当tem是尾节点。head所在位置恰好与tem相差k
            head=head.next;
            tem=tem.next;
        }
        return head;
    }


2、输入一个链表，反转链表后，输出新链表的表头。

	
    public ListNode ReverseList(ListNode head) {
		ListNode buf=head; //buf>listNode>      1》2,》3,》4
	    ListNode pre=buf;    //pre>buf>listNode>    1》2,》3,》4
	      if (head==null)
	            return  null;
	      while (head.next!=null){ //判断节点是否还有下一个元素
	        buf=head.next; //  buf>2>3>4
	          head.next=buf.next;//   listNode>1>3>4
	        buf.next=pre;//buf>2>1>3>4
	        pre=buf;//pre>2>1>3>4
	    }
	    return buf;
    }


3、输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。


	  public static ListNode Merge(ListNode list1,ListNode list2) {
        ListNode head=list1;//记录头部节点
        ListNode tem;
        ListNode node;
        while (list2!=null){// 以list1为链表，将list2插入list1，故判断list2是否为空
            if (list1.next==null){//当list1已到达尾节点时，避免空指针
                if (list1.val<=list2.val) {//list1值小于list2值，则list2后续节点皆大于list2。故可直接将所有节点插入，跳出循环
                    list1.next = list2;
                    break;
                }
                else {//否则将list2的值插入list1前
                    node=new ListNode(list1.val);
                    list1.next=node;
                    list1.val=list2.val;
                    list1=list1.next;
                    list2=list2.next;
                }
            }
            if (list1.val<=list2.val){
                if (list1.next.val>list2.val) {//判断是否合适插入点
                    tem = list1.next;
                    node = new ListNode(list2.val);
                    list1.next = node;
                    node.next = tem;
                    list1=list1.next;
                    list2 = list2.next;
                }
                else//否则继续寻找合适插入点
                    list1=list1.next;
            }else {//互换值，确保list1<list2  （尚可以优化，按 list1.next.val<list2.val）
                int num=list1.val;
                list1.val=list2.val;
                list2.val=num;
            }

        }
        return head;
    }


备注：

	class ListNode {
	    int val;
	    ListNode next = null;
	    ListNode(int val) {
	        this.val = val;
	    }
	}
