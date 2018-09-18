
---
title: 	"【剑指offer】 顺时针打印二维数组"   
date:  2018-09-18 15:49:05
tag: [array]
categories: [剑指offer]  
         
---

1.输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

思路：对于矩阵的瞬时针打印，我们可以认为其属于轮循的分别执行打印各边，从而降低问题的难度。


	/**
     * 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵：
     *  1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.
     */
    public ArrayList<Integer> printMatrix(int [][] matrix) {
        int rows=matrix.length;
        int cols=matrix[0].length;
        ArrayList<Integer> arrayList=new ArrayList<>(rows*cols);
        int rowstart=0,rowend=rows-1,colstart=0,colend=cols-1;
        if (rows==1) {
            for (int i = 0; i <= colend; i++)
                arrayList.add(matrix[0][i]);
            return arrayList;
        }
        if (cols==1) {
            for (int i = 0; i <= rowend; i++)
                arrayList.add(matrix[i][0]);
            return arrayList;
        }
        /**顺时针打印矩阵，即意味着可以将矩阵看为一圈又一圈数字组成。
         * 一圈又分为四边，可以分为四个循环，注意各点边界
         */
        while (rowstart<=rowend&colstart<=colend){
            for (int i=colstart;i<=colend;i++)//打印上边
                arrayList.add(matrix[rowstart][i]);
            for (int i=rowstart+1;i<=rowend;i++)//打印右边
                arrayList.add(matrix[i][colend]);
            for (int i=colend-1;i>=colstart&rowstart!=rowend;i--)////打印右边  （当rows小于cols时，会出现重复打印。故需加上判断）
                arrayList.add(matrix[rowend][i]);
            for (int i=rowend-1;i>rowstart;i--)//打印左边
                arrayList.add(matrix[i][colstart]);
            rowstart++;rowend--;colstart++;colend--;
        }
        return arrayList;
    }

