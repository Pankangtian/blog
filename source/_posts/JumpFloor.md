---
title: 【剑指offer】 斐波那契数列问题
date: 2018-08-21 19:16:15
tags: [math] 
categories: [剑指offer]    

---

1、[斐波那契数列 （Fibonacci sequence）](https://baike.baidu.com/item/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97/99145?fr=aladdin "斐波那契数列")，又称黄金分割数列、因数学家列昂纳多·斐波那契（Leonardoda Fibonacci）以兔子繁殖为例子而引入，故又称为“兔子数列”，指的是这样一个数列：1、1、2、3、5、8、13、21、34、……在数学上，斐波纳契数列以如下被以递推的方法定义：F(1)=1，F(2)=1, F(n)=F(n-1)+F(n-2)（n>=2，n∈N*）

代码实现如下：
      
    // 斐波那契数列的java实现 
    public static int Fibonacci(int n) {
        int last=1,latter=1,result=0; //用于缓存f(n-1) f(n-2)
        if (0==n)
            return 0;
        else if (1==n||2==n)
            return 1;
        else {
            for (int i=3;i<=n;i++){
                result=last+latter;  //计算f(n)
                last=latter;//更新f(n-2)
                latter=result;  //更新f(n-1)
            }
            return result;
        }
    }


2、一只青蛙一次可以跳上1级台阶，也可以跳上2级。 求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。 


  用递推可知其结果为斐波那契数列f(n)=f(n-1)+f(n-2)

    public int JumpFloor(int n) {
    int last=1,latter=2,result=0; //用于缓存f(n-1) f(n-2)
        if (0==n)
            return 0;
        else if (1==n)
            return 1;  
		else if(2==n)
			return 2;
        else {
            for (int i=3;i<=n;i++){
                result=last+latter;  //计算f(n)
                last=latter;//更新f(n-2)
                latter=result;  //更新f(n-1)
            }
            return result;
        }
    }



3、附加：一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

       static int jumpFloorII(int number) {//罗列各项，寻找规律，可知f(n)=2的n-1次方
        int result=1;
        return result<<(number-1);//将乘法优化为位运算
    }


4、我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？罗列各项，寻找规律，递推可知其结果为斐波那契数列f(n)=f(n-1)+f(n-2)

    
     int rectCover(int target) {
        int last=1,latter=2,result=0; //用于缓存f(n)=f(n-1)+f(n-2)
        if (1==target)
            return 1;
        else if (2==target)
            return 2;
        else {
            for (int i=3;i<=target;i++){
                result=last+latter; //计算f(n)
                last=latter; //更新f(n-2)
                latter=result; //更新f(n-1)
            }
            return result;
        }

    }

<center>[Coding Blog](http://kangtian.coding.me)     &nbsp;&nbsp;&nbsp;    [Github Blog  ](http://pankangtian.github.io/) </center>