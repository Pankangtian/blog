---
title: 【剑指offer】重建二叉树 
date: 2018-08-19 15:21:01
tags:  [tree]    
categories: [剑指offer]

---
>  题目描述:
>  
 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

---------------------

* 递归实现
 
 根据前序遍历和中序遍历还原二叉树的一个要点是，前序遍历的每一个节点可以当成根节点处理，叶子节点即为子节点为空的根节点。而根据前序遍历定义的根节点的值在中序遍历所在索引的左边即为左子树，右边即为右子树。
 
      public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        int len=in.length;
        // 用map是因为其查找效率均衡，在数据量较大时较优.hashMap默认因子为0.75
        HashMap<Integer,Integer> map= new HashMap<Integer, Integer>(len*4/3+2);
        for(int i=0;i<len;i++){
            map.put(in[i],i);
        }
        return reBulid(pre,0,len-1,in,0,len-1,map);
    }
    //递归创建各子树
    public TreeNode reBulid(int [] pre, int prestart, int preend, int [] in, int instart, int inend, HashMap<Integer,Integer> map){
        if(prestart > preend || instart> inend)//说明已无左节点或有节点
            return null;
        TreeNode root = new TreeNode(pre[prestart]);//新建子树的根节点
        //对中序数组进行输入边界的遍历
       //查找子树根节点位置,用map是因为其查找效率均衡，在数据量较大时较优
        int i=map.get(pre[prestart]);
        //递归构建左子树
        //中序遍历的根节点的左边为左子树，并求出器索引位置，前序遍历的前索引位即是左子树，明确边界
        root.left = reBulid(pre,prestart+1,prestart+i-instart,in,instart,i-1,map);
        //递归构建右子树
        //中序遍历的根节点的右边为右子树，并求出其索引位置，前序遍历的后end-索引个即是右子树，明确边界
        root.right = reBulid(pre,prestart+i+1-instart,preend,in,i+1,inend,map);
        return root;
    }