---
title: 【剑指offer】  树问题
date: 2018-08-21 19:16:15
tags: [tree] 
categories: [剑指offer]    

---

1、输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

	 //如果root2为root1的子树，则root2的前序遍历字段必为root1的子串
    public boolean HasSubtree(TreeNode root1,TreeNode root2) {
        if (root1==null||root2==null)//如果为空，则不必判断
            return false;
            String str1=preTraver(root1);//root1的前序遍历字段
            re="";//置空前序遍历方法的结果串
            String str2=preTraver(root2);//root2的前序遍历字段
            if (str1.contains(str2)) //str1包含str2，则root2为root1的子树
                return true;
            else
                return false;
    }

2、操作给定的二叉树，将其变换为源二叉树的镜像。
	
	
    /**操作给定的二叉树，将其变换为源二叉树的镜像。
     * 可以用递归的方法将所有的节点的左右节点换位即可
     * @param root
     */
    public static void Mirror(TreeNode root) {
         if (root==null)
             return;
            tem=root.left;//缓存左子树
            root.left=root.right;//将右子树赋值给左子树
            root.right=tem;//将左子树赋值给右子树
            if (root.left!=null)
                Mirror(root.left);//递归左子树
            if (root.right!=null)
                Mirror(root.right);//递归右子树
    }


备注：

	TreeNode类：
	public class TreeNode {
	    int val = 0;
	    TreeNode left = null;
	    TreeNode right = null;
	    public TreeNode(int val) {
	        this.val = val;
    }

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