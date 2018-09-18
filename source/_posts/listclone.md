
---
title: 	"【剑指offer】 复杂链表的赋值"   
date:  2018-09-18 18:45:27
tag: [list]     
categories: [剑指offer]  
        
---
####题目描述
输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）    
算法实现思路：虽然是复杂链表，但还是可以跟简单链表一个思路，先备份头结点，然后复制简单链表，最后根据原链表同步复制随机指针，为了便捷的找到指针，我采用hashmap用于查询节点，从而快速找到节点位置

    public RandomListNode Clone(RandomListNode pHead) {
        HashMap<Integer,RandomListNode>  data= new HashMap<>();//用于复制随机指针时快速定位到指针位置
        if (pHead==null)
            return null;
        RandomListNode tempPHead=pHead;
        RandomListNode head, tempHead, foot;
        foot=new RandomListNode(pHead.label);
        data.put(pHead.label,foot);
        head=foot;
        //拷贝简单的链表
        while (pHead!=null){
            pHead=pHead.next;
            foot.next=new RandomListNode(pHead.label);
            foot=foot.next;
            data.put(pHead.label,foot);//保存复制出来的节点索引
        }
        tempHead=head;
        //拷贝random
        while (tempPHead!=null){
            if (tempPHead.random!=null){
                tempHead.random= data.get(tempPHead.random.label);//获取节点索引
            }
            tempHead=tempHead.next;
            tempPHead=tempPHead.next;
        }
        return head;
    }



