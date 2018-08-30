---
title: 【剑指offer】 旋转数组的最小数字 
date: 2018-08-19 16:25:55   
tags: [array,search]   
categories:  [剑指offer]      

---

>  题目描述
>  
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

--------------
####### 题目的要点在于判定数组从何处旋转，即array[start]>array[start+1]处。只需循环到符合条件，便可认为其为最小值。该题目还需注意两个边界值，一是最大索引处即start+1要小于等于数组长度，一是为0时，直接返回0，1时直接返回1。
                                                          

     
     public int minNumberInRotateArray(int [] array) {
           int start=0;
        int end=array.length-1;
        int mid;
        if (end<0)//长度为零直接返回0
            return 0;
        if (end==0)//长度为1直接返回array[0]处数值
            return array[0];
        while (start<end){//循环数组
            //当array[start]>array[start+1] 由有序旋转数组定义可知，array[start+1]即为最小值。array[start]为最大值
            if (array[start]>array[start+1])
                return array[start+1];
            start++;
        }
        return 0;
    }




<center>[Coding Blog](http://kangtian.coding.me)     &nbsp;&nbsp;&nbsp;    [Github Blog  ](http://pankangtian.github.io/) </center>