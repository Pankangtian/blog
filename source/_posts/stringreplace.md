---
title: 【剑指offer】 字符串替换
date: 2018-08-17 19:29:47
tags: [string]
categories: [剑指offer]   

---

####  题目：
> ####  请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

------
1、     
     为了减少插入时字符串的移位消耗，可生成一个对象去进行append操作，而不是在原来字符串进行插入操作；
      为了减少不必要的append，可以通过start和end确定要进行append的子串，通过判断是否为空格进行append的时机；
    

    public static String replaceSpace(StringBuffer str) {
        StringBuffer stringBuffer=new StringBuffer();
        int start=0;
        int end=0;
        int lenght=str.length();
        while (end<lenght){
            //计算从何处开始append，减少append次数
            if (str.charAt(end)!=' '){
                end++;
            }else {//当char 等于空格时开始替换
                stringBuffer.append(str.substring(start,end)).append("%20");
                end++;
                start=end;
            }
        }
        stringBuffer.append(str.substring(start,end));//最后一次，将末尾start,end的子串插入
        return stringBuffer.toString();
    }


2、 不新生成对象，采用统计空格数，重新赋值字符串长度，然后采用从尾部赋值的操作方式，减少移位，提升效率。

     public static String replaceSpace2(StringBuffer str) {
        int count=0;
        int oldlen=str.length();
       for (int i=0;i<oldlen;i++){//计算空格数
           if (str.charAt(i)==' ')
               count++;
       }
       int newlen=oldlen+count*2; //计算新字符串长度
       str.setLength(newlen);
        for (int i=oldlen-1;i>=0;i--){//从尾开始进行赋值操作，避免从头部操作时的char的移位
            char data=str.charAt(i);
            if (data!=' '){//如果不等于空格则直接赋值
                str.setCharAt(--newlen,data);
            }
            else {//如果等于空格，则赋值%20
                str.setCharAt(--newlen,'0');
                str.setCharAt(--newlen,'2');
                str.setCharAt(--newlen,'%');
            }
        }
        return str.toString();
    }


    <center>[Coding Blog](http://kangtian.coding.me)     &nbsp;&nbsp;&nbsp;    [Github Blog  ](http://pankangtian.github.io/) </center>