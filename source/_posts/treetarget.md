---
title: 	"【剑指offer】 二叉树中和为某值的路径"   
date:  2018-09-18 17:18:02
tag: [tree]     
categories: [剑指offer]  
        
---

####题目描述：
输入一颗二叉树的跟节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。(注意: 在返回值的list中，数组长度大的数组靠前)   
利用前序遍历，遍历所有节点，利用target减为零和子节点是否都空判断是不是叶子节点

	 private ArrayList<ArrayList<Integer>> arrayLists;
	
	    /**
	     * 题目描述
	     * 输入一颗二叉树的跟节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。
	     * 路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。
	     * (注意: 在返回值的list中，数组长度大的数组靠前)
	     * @param root
	     * @param target
	     * @return
	     */
	    public ArrayList<ArrayList<Integer>> FindPath(TreeNode root, int target) {
	        arrayLists=new ArrayList<ArrayList<Integer>>();
	        FindPath(root,target,"");
	        return arrayLists;
	    }
	    //递归遍历各节点，并利用String 统计路径，当满足target==0 &root.left==null&root.right==null，路径和为target，且为叶子节点
	    public void   FindPath(TreeNode root, int target,String path) {
	        if (root!=null) {
	            path += root.val+",";//记录路径
	            target=target-root.val;//和为target，即target减其为0
	            if (target==0 &root.left==null&root.right==null){//root.left==null&root.right==null为判断其是否叶子节点
	                ArrayList<Integer> arrayList=new ArrayList<>();
	                String[] st = path.split(",");
	                for (int i=0;i<st.length;i++)//将路径添加到list中
	                    arrayList.add(Integer.valueOf(st[i]));
	                arrayLists.add(arrayList);
	            }
	            if (target<0)//当小于零时，则其以下节点不用考虑
	                return ;
	            if (root.left != null)
	                FindPath(root.left,target,path);
	            if (root.right != null)
	                FindPath(root.right,target,path);
	        }
	    }
	
	
