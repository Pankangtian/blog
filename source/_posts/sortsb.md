---
title: JAVA排序算法--选择排序和冒泡排序      
date: 2018-09-14 15:02:06   
tags:  [sort,排序]     
      
categories:  [Java工具,排序算法]       

---
1.选择排序算法    
选择排序算法原理：选择排序算法就是在集合中选择最大或则最小的数，将其放在集合前列，然后循环剩下的集合数据，重复寻找最大或最小值。选择排序算法是不稳定的算法    
我们可以简单的依次选择剩下元素中的最小值，将其跟i处的值交换，从而达到排序的效果，不管数据如何，对于选择排序而言，它总是需要轮循n+(n-1)+(n-2)+...+2+1次，即（n+1)*n/2，算法复杂度还是O（n<sup>2</sup>)。

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

 我们可以对选择排序算法进行优化，在选取最小值的同时，选取最大值，将其分别放置在头部和尾部,再对其剩下的部分进行轮循，虽然算法复杂度还是O（n<sup>2</sup>)级别，但优化的效果还是可以的。                         


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

 
2.冒泡排序算法     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;冒泡排序原理：冒泡排序算法是重复地访问未排序序列，依次比较其两个相邻的元素，如果顺序出现问题就交换其两者位置。每次轮训后，其len-i-1的值必定是未排序序列中的最大值或最小值。其算法复杂度为O（n<sup>2</sup>)   

简单的排序算法算法如下         

	 public static void sort(int [] arr){
        int len=arr.length;
        int tem;
        for (int i=0;i<len-1;i++)
            for (int j=0;j<len-i-1;j++)
               //通过不断的比较arr j j+1处位置大小， 把大的数往后挪，
                // 每次都能保证将len-i个里的最大的挪到数组len-i处
                //如1 4 2 3 5 2  第一次，4和2换，4和3换 5和最后一个2换 。得1 2 3 4 2 5
                if (arr[j]>arr[j+1]){
                    tem=arr[j];
                    arr[j]=arr[j+1];
                    arr[j+1]=tem;
                }

    }


我们可以对冒泡排序算法进行一次优化，即在数组已经有序的情况下，避免不必要循环。

	 public static void sort(int [] arr){
        int len=arr.length;
        int tem,count=1;//初始化值为1，确保第一次能进入循环
        for (int i=0;i<len-1;i++) {
            if (count > 0) {//count大于0，说明上次轮循出现了交换，即序列可能是处于无序状态的
                count=0;//赋值为零，进行下一次冒泡，并统计交换次数用于判断数组是否有序
                for (int j = 0; j < len - i - 1; j++) {
                    //通过不断的比较arr j j+1处位置大小， 把大的数往后挪，
                    // 每次都能保证将len-i个里的最大的挪到数组len-i处
                    //如1 4 2 3 5 2  第一次，4和2换，4和3换 5和最后一个2换 。得1 2 3 4 2 5
                    if (arr[j] > arr[j + 1]) {
                        count++;
                        tem = arr[j];
                        arr[j] = arr[j + 1];
                        arr[j + 1] = tem;
                    }
                }
            }else {
                break;//数组已经有序，跳出循环
            }
        }
    }


附:常见算法复杂度表     
<center><img src="/images/timg.jpg"/> </center>



