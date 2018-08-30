---
title: 【剑指offer】  树的遍历
date: 2018-08-21 19:16:15
tags: [tree] 
categories: [数据结构]    

---

1、利用递归的方式获取树的前序遍历结果

	 //获取树的前序遍历
    public static String preTraver(TreeNode root){
        if (root!=null) {
            re += root.val;
            if (root.left != null)
                preTraver(root.left);
            if (root.right != null)
                preTraver(root.right);
        }
        return re;
    }

2、 利用递归的方式获取树的中序遍历结果

	    //获取树的中序遍历
    public static String medTraver(TreeNode root){
        if (root!=null) {
            if (root.left != null)
                medTraver(root.left);
            re += root.val;
            if (root.right != null)
                medTraver(root.right);
        }
        return re;
    }

3、利用递归的方式获取树的后序遍历结果

    //获取树的后序遍历
    public static String aftTraver(TreeNode root){
        if (root!=null) {
            if (root.left != null)
                preTraver(root.left);
            if (root.right != null)
                preTraver(root.right);
            re += root.val;
        }
        return re;
    }


4、利用队列实现层次遍历
 
	//获取树的层次遍历
    public static String levelTraver(TreeNode root){
        Queue<TreeNode> queue = new ArrayDeque<TreeNode>();
        TreeNode node;
     if (root!=null)
         queue.offer(root);
     while (!queue.isEmpty()){
         node=queue.poll();
         re+=node.val;
         if (node.left!=null)
             queue.offer(node.left);
         if (node.right!=null)
             queue.offer(node.right);
     }
        return re;
    }




<center>[Coding Blog](http://kangtian.coding.me)     &nbsp;&nbsp;&nbsp;    [Github Blog  ](http://pankangtian.github.io/) </center>