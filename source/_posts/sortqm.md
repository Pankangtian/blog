---
title: JAVA排序算法--快速排序和归并排序  
date: 2018-09-17 14:50:08
tags:  [sort,排序]     
      
categories:  [Java工具,排序算法]       


---

1.快速排序算法    
>原理：  快速排序由C. A. R. Hoare在1962年提出。它的基本思想是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

根据快排的原理，我们可以知道快排是一个不断将序列分为独立的两个序列的过程，其中一部分数据要比另外一部分小，快排的重点是找到这个poit点，从而是序列很好的切分开。具体算法如下，但可以通过排序点的选取对代码进一步优化

	 public static void sort(int[] arr){
            sort(arr, 0, arr.length-1);
    }
    public static void sort(int[] arr,int s,int e){
        if (s<e) {
            int p = getPoit(arr, s, e);
            sort(arr, s, p - 1);
            sort(arr, p + 1, e);
        }
    }
    public static int getPoit(int[] arr,int start,int end){//s为start ，e为end缩写
        int  tem=arr[start];//选取排序点
        while (start<end){//通过排序使start左边的值都大于tem，右边的值都大于tem
            while (start<end&&arr[end]>=tem)//从右边开始查找，找到小于tem处位置
                end--;
            arr[start]=arr[end];//将其移到tem左边
            while (start<end&&arr[start]<=tem)//从左边开始查找，找到大于tem处位置
                start++;
         arr[end]=arr[start];//将其移到tem的右边
        }
        arr[start]=tem;
        return start;
    }


2.归并排序   
>原理：归并排序（MERGE-SORT）是采用分治法（Divide and Conquer）的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为二路归并。    

算法实现，第一，现将序列递归为长度为2的有序序列，由于序列是有序的，故而其合并后的序列也是有序的。其算法复杂度为O（nlogn)级别的，此处仅实现二路归并排序，有想法的朋友可以优化一下。

	public static void sort(int[] arr){
        sort(arr,0,arr.length-1);
    }
    public static void sort(int[] arr,int start,int end){
        int mid=(start+end)/2;
        if (start<end){
            sort(arr,start,mid);//无限细分序列
            sort(arr,mid+1,end);
            merge(arr,start,mid,end);//合并序列（由于细分序列后的数组已是有序，归并后的数组故而也是有序的）
        }
    }
    public static void merge(int[] arr,int start,int mid,int end){
        int i=start,j=mid+1,k=0;
        int len=end - start + 1;
        int[] temp = new int[len];//辅助数组，利用空间换取移位的时间耗时
        while (i<=mid&&j<=end){//由于序列不一定等长，故会存在其中一个序列没有合并完
            if (arr[i]<arr[j])//合并序列
                temp[k++]=arr[i++];
            else
                temp[k++]=arr[j++];
        }
        while (i<=mid)//如果i<=mid即i到mid未合并完，合并该部分
            temp[k++]=arr[i++];
        while (j<=end)//如果j<=end即j到end未合并完，合并该部分
            temp[k++]=arr[j++];
        for ( i=0;i<len;i++) //将有序数据复值到原数组中
            arr[start++]=temp[i];
    }

附:常见算法复杂度表     
<center><img src="/images/timg.jpg"/> </center>


