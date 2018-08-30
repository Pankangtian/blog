---
title: 【剑指offer】  重排数组
date: 2018-08-21 19:16:15
tags: [array] 
categories: [剑指offer]    

---
1、输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。


	public void reOrderArray(int [] array) {
        int len=array.length;
        int[] arr=array.clone(); //拷贝一份数组
        int p=0;
        for (int i=0;i<len;i++){//遍历拷贝数组，先插入奇数
            if ((arr[i]&1)==1){
                array[p++]=arr[i];
            }
        }
        for (int i=0;i<len;i++){//遍历拷贝数组，插入偶数
            if ((arr[i]&1)==0){
                array[p++]=arr[i];
            }
            if (p==len)//所有元素已经插入后，无需再继续遍历
                break;
        }
    }


<center>[Coding Blog](http://kangtian.coding.me)     &nbsp;&nbsp;&nbsp;    [Github Blog  ](http://pankangtian.github.io/) </center>