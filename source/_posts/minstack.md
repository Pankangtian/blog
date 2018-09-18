
---
title: 	"【剑指offer】 构建含有min函数的栈"   
date:  2018-09-18 15:56:20
tag: [stack]
categories: [剑指offer]  
         
---

####题目描述：
定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。


	import java.util.ArrayList;
	/**采用两个链表，一个链表存储数据，另一个链表存储用于存储最小值
	 * 比如dataList为5 4 7 3 2  ，则minList为5 4 4  3 2 。
	 * 当执行pop操作时，再同步删除两个链表的值，维护数据
	 * 5 4 7 3               5  4 4  3
	 * @param node
	 */
	public class MinStack {
	    ArrayList<Integer> dataList=new ArrayList<Integer>();
	    ArrayList<Integer> minList=new ArrayList<Integer>();
	    private int min=Integer.MAX_VALUE;
	    public void push(int node) {//对于最小栈，始终保持同步存入最小的数
	        dataList.add(node);
	        if (min>node){//如果最小值大于node，存储node
	            minList.add(node);
	            min=node;
	        }else {
	            minList.add(min);//否则存储min
	        }
	    }
	    public int pop() {//同时出栈，维护栈的数据
	        int size=dataList.size();
	        minList.remove(size-1);
	        return  dataList.remove(size-1);
	    }
	    public int top() {
	        return dataList.get(dataList.size()-1);
	    }
	
	    public int min() {
	    return minList.get(minList.size()-1);
	    }
	}
