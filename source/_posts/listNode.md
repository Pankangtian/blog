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


备注：

	class ListNode {
	    int val;
	    ListNode next = null;
	    ListNode(int val) {
	        this.val = val;
	    }
	}
