---
title: 【剑指offer】  统计二进制1与指数的实现
date: 2018-08-21 19:16:15
tags: [math] 
categories: [剑指offer]    

---

1、输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

	static   int  NumberOf1(int n) { //例如10101
      int count=0;
      while (n!=0){
          count++;
          n=n&(n-1); //除去末尾1   10100&10011=10000
      }
      return count;
    }

2、给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。


	public double Power(double base, int exponent) throws Exception {
        int num=exponent;
        double result=1;
        if (exponent<0) {//当指数为负数时，转为正数
            exponent = -exponent;
            if (base==0)
                throw new Exception("base 不能等于0");
        }
        while (exponent!=0){
            if ((exponent&1)==1)//当末尾为零时
                result*=base;
            base*=base;//倍乘（二进制，每隔差一位为2倍，故应倍乘
            exponent=exponent>>1;//乘或倍乘后右移一位，
        }
        return  num>0?result:1/result; //当指数为负时，返回1/result。否则返回result
    }



<center>[Coding Blog](http://kangtian.coding.me)     &nbsp;&nbsp;&nbsp;    [Github Blog  ](http://pankangtian.github.io/) </center>