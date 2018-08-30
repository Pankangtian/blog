---
title: 【剑指offer】  从尾到头打印链表
date: 2018-08-19 14:02:42
tags: [linked-list]
categories: [剑指offer]

---
####   [题目](https://kangtian.coding.me/2018/08/19/printListFromTailToHead/)：输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。

----

1.利用递归实现

     //递归实现
    public  ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        if (listNode!=null){
            this.printListFromTailToHead(listNode.next);//先递归到末尾元素
            arrayList.add(listNode.val);//依次将元素添加进数组
        }
        return arrayList;
    }


2.利用栈的先进后出实现

   
       //利用栈的先进后出
    public  ArrayList<Integer> printListFromTailToHead1(ListNode listNode) {
        Stack<Integer> stack=new Stack<Integer>();
        while (listNode!=null){ //利用栈的先进后出 将ListNode缓存进栈中
            stack.push(listNode.val);
            listNode=listNode.next;
        }
        while (!stack.isEmpty()){//当栈非空时
            arrayList.add(stack.pop());//将元素出栈，并添加到数组里。
        }
        return arrayList;
    }



3.先将指针逆转，再一次添加到链表

     //逆转指针
    public static   ArrayList<Integer> printListFromTailToHead2(ListNode listNode) {//假有四个节点，方向1》2,》3,》4  listNode >1
      ListNode buf=listNode; //buf>listNode>      1》2,》3,》4
      ListNode pre=buf;    //pre>buf>listNode>    1》2,》3,》4
      if (listNode==null)
          return  arrayList;
      while (listNode.next!=null){ //判断节点是否还有下一个元素
          buf=listNode.next; //  buf>2>3>4
          listNode.next=buf.next;//   listNode>1>3>4
          buf.next=pre;//buf>2>1>3>4
          pre=buf;//pre>2>1>3>4
      }
      //buf>4>3>2>1
      while (buf!=null){
          arrayList.add(buf.val);
          buf=buf.next;
      }
      return arrayList;
    }

    <center>[Coding Blog](http://kangtian.coding.me)     &nbsp;&nbsp;&nbsp;    [Github Blog  ](http://pankangtian.github.io/) </center>