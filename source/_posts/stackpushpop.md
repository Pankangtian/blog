
---
title: 	"【剑指offer】 栈的压入弹出序列"   
date:  2018-09-18 16:58:38
tag: [stack]     
categories: [剑指offer]  
         
---
####题目描述：
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）    

解题思路：我们可以根据根据弹出序列的值来判断是否执行出栈操作，当循环完后，压入序列未出栈完，则认为该弹出序列不是该压栈序列的弹出序列。

 	static   ArrayList<Integer> stack = new ArrayList<Integer>();
    public static boolean IsPopOrder(int[] pushA, int[] popA) {
        int len = pushA.length;
        int i = 0;
        int k = 0;
        while (i < len) {
            stack.add(pushA[i]);//将序列压入栈中
            if (pushA[i] == popA[k]) {//当栈顶元素等于弹出序列k的值时，说明是栈顶元素出栈了
                stack.remove((Integer) pushA[i]);
                k++; i++;
            }else//否则继续压栈操作
                i++;
            while ((stack.size()>0&&stack.get(stack.size()-1) == popA[k])) {//当栈顶元素等于弹出序列k的值时，说明是栈顶元素该出栈了
                stack.remove(stack.size() - 1);//执行出栈操作
                k++;
            }
        }
        if (stack.size()==0)//所有元素入栈且出栈完，说明其是弹出序列
            return true;
        else
            return false;
    }



