---
title: JAVA排序算法      
date: 2018-09-14 15:02:06   
tags:  [sort,排序]     
      
categories:  工具

---
1. 选择排序算法    
&nbsp;&nbsp;&nbsp;&nbsp;选择排序算法原理：选择排序算法就是在集合中选择最大或则最小的数，将其放在集合前列，然后循环剩下的集合数据，重复寻找最大或最小值。  

简单算法实现如下

		public static void sortSimple(int [] arr){
	        int len=arr.length;  int tem=0;
	        for (int i=0;i<len-1;i++){
	            int p=i; int m=i;
	            for (int j=len-1;j>i;j--){//寻找剩下里面的最小值
	                if (arr[j]<arr[p])
	                    p=j;
	            }
	            tem=arr[p]; //将最小值交换到i处。
	            arr[p]=arr[i];
	            arr[i]=tem;
	        }
    	}
	

优化选择排序，同时选取最大值和最小值

	public static void sort(int [] arr){
        int len=arr.length;
        int tem=0;
        for (int i=0;i<len-1;i++){
                int p=i;
                int m=i;
            for (int j=len-1;j>i;j--){
               if (arr[j]<arr[p])//寻找剩下里面的最小值
                    p=j;
                if (arr[j]>arr[m])//寻找剩下里面的最大值
                    m=j;
            }
            tem=arr[p];//将最小值交换到i处。
            arr[p]=arr[i];
            arr[i]=tem;
            if (p!=m) {//避免最后的重复交换导致顺序错乱
                tem = arr[len - 1];//将最大值交换到len - 1处。
                arr[len - 1] = arr[m];
                arr[m] = tem;
                len--;//没交换一次，len减1
            }
        }
    }







