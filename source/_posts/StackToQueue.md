---
title: 【剑指offer】 用两个栈实现队列   
date: 2018-08-19 16:25:55   
tags: [stack,queue]   
categories:  [剑指offer]      

---

>  题目描述
>  
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

--------------
##### 用栈实现队列的原理是双重否定，经过两次后进先出的队列，其数据也就转换为了先进后出的队列。实现的要点在于区分何时将数据从栈转移到另一个栈   
                                                          

     
    Stack<Integer> stack1 = new Stack<Integer>();//用来进行push操作
    Stack<Integer> stack2 = new Stack<Integer>();//用来进行pop操作
    public void push(int node) {
        stack1.push(node);
    }
    public int pop() {
        if (stack2.isEmpty()){//当stack2为空时，尝试将stack1的所有元素移到stack2.
            //将stack1的所有元素移到stack2.由于经过stack1和Stack2后，后进先出的,变为先进先出的队列
            while (!stack1.isEmpty()){
                stack2.push(stack1.pop());
            }   
        }
          return  stack2.pop();
    }