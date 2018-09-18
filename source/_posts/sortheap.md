---
title: JAVA排序算法--堆排序  
date: 2018-09-17 14:50:08   
tags:  [sort,排序]         
categories:  [Java工具,排序算法]       

---
堆排序算法：
>堆排序的基本思想是：将待排序序列构造成一个大顶堆，此时，整个序列的最大值就是堆顶的根节点。将其与末尾元素进行交换，此时末尾就为最大值。然后将剩余n-1个元素重新构造成一个堆，这样会得到n个元素的次小值。如此反复执行，便能得到一个有序序列了


因此堆排序算法是一个不断将堆顶元素取出，并重新构建堆的过程。其算法实现如下：


	 public  void sort(int arr[]){
        int len=arr.length;
        for (int i=0;i<len;i++) {
            adjust(arr, len - 1 - i);//构建堆
            swap(arr, 0, len - i - 1);//把堆顶元素取出
        }
        int i=0,end=arr.length-1;
        while (i<end){
            swap(arr,i,end);
            i++;end--;
        }
    }





1.堆的父类

	/**
	 *堆是一组元素按照完全二叉树的形式存储在一个数组里面，并且在这个完全二叉树里面满足父节点和子节点的关系为
	 * Ki <= K2*i+1 且 Ki<= K2*i+2(或Ki >= K2*i+1 且 Ki >= K2*i+2) i = 0，1，2…， 的一种数据结构。
	 */
	public  class Heap {
	    int size=0,len=16;double capacity=1.5;
	    int [] heap;
	    public Heap(){
	        heap=new int[len];
	    }
	    public Heap(int len){
	        this.len=len;
	        heap=new int[len];
	    }
	    public Heap(int len,int capacity){
	        this.len=len;
	        this.capacity=capacity;
	        heap=new int[len];
	    }
	    public int peek(){
	        return heap[0];
	    }
	    public void printHeap(){
	        for (int i=0;i<size;i++)
	            System.out.print(heap[i]+" , ");
	        System.out.println();
	    }
	    public static void swap(int arr[],int a,int b){
	        int tem=arr[a];
	        arr[a]=arr[b];
	        arr[b]=tem;
	    }
	    public int pop(){
	        int tem=heap[0];
	        heap[0]=heap[size-1];
	        size--;
	        adjust(heap,size-1);
	        return size;
	    }
	    public  void adjust(int heap[] ,int end){
	
	    }
	
	    public  boolean isEmpty(){
	        return size==0;
	    }
	    public  boolean isFull(){
	        return size==len;
	    }
	    public static boolean isHeap( int[] arr){
	        boolean is=true;
	        int len=arr.length-1;
	        if (len<=1)
	            return is;
	        if (arr[0]<arr[1])
	        for(int i=(len-1)/2;i>=0;i--){
	            int k=i;//k对应树的根节点
	            while(k*2+1<=len){
	                int j=2*k+1;//对应子节点
	                    if(j<len&&arr[j]>arr[j+1])
	                        j++;
	                if(arr[k]>arr[j]){//判断根节点是否大于子节点，如果是，则不满足小堆
	                  is=false;i=-1;
	                    break;
	                }
	                else {
	                    k=j;
	                }
	            }
	        }
	        else
	            for(int i=(len-1)/2;i>=0;i--){
	                int k=i;
	                while(k*2+1<=len){
	                    int j=2*k+1;
	                    if(j<len&&arr[j]>arr[j+1])
	                        j++;
	                    if(arr[k]<arr[j]){//判断根节点是否小于父节点，如果是，则不满足大堆
	                        is=false;i=-1;
	                        break;
	                    }else{
	                       k=j;
	                    }
	                }
	            }
	        return is;
	    }
	}
	
	
	

	
2.最大堆


	
	public class MaxHeap extends Heap {
	    public MaxHeap(){
	        heap=new int[len];
	    }
	    public MaxHeap(int len){
	        this.len=len;
	        heap=new int[len];
	    }
	    public MaxHeap(int len,int capacity){
	        this.len=len;
	        this.capacity=capacity;
	        heap=new int[len];
	    }
	    public MaxHeap(int [] arr){
	        len=arr.length;
	        heap=new int[len];
	        for (int i=0;i<len;i++) {
	                insert(arr[i]);
	        }
	    }
	
	    public void insert(int num)  {
	        if (isFull()){
	            len=(int) (len*capacity);
	            int tem[] =new int[len];
	            for (int i=0;i<size;i++)
	                tem[i]=heap[i];
	            heap=tem;
	        }
	        int i = size;//指向插入元素后堆中的最后一个元素的位置
	        for(;i>0 && heap[(i-1)/2]<num;i=(i-1)/2){
	            heap[i] = heap[(i-1)/2];
	        }
	        heap[i] = num;
	        size++;
	    }
	
	    //调整数组，使其保持堆的性质
	    @Override
	    public  void adjust(int heap[] ,int end){
	        for(int i=(end-1)/2;i>=0;i--){
	            int k=i;//根节点
	            while(k*2+1<=end){
	                int j=2*k+1;
	                if(j<end){
	                    if(heap[j]<heap[j+1]){
	                        j++;
	                    }
	                }
	                if(heap[k]<heap[j]){//判断
	                    swap(heap,k,j);
	                    k=j;
	                }else{
	                    break;
	                }
	            }
	        }
	    }
	    public  void sort(int arr[]){
	        int len=arr.length;
	        for (int i=0;i<len;i++) {
	            adjust(arr, len - 1 - i);
	            swap(arr, 0, len - i - 1);
	        }
	    }
	}




3.最小堆

	public class MinHeap extends Heap {
	    public MinHeap(){
	        heap=new int[len];
	    }
	    public MinHeap(int len){
	        this.len=len;
	        heap=new int[len];
	    }
	    public MinHeap(int len,int capacity){
	        this.len=len;
	        this.capacity=capacity;
	        heap=new int[len];
	    }
	    public MinHeap(int [] arr){
	        len=arr.length;
	        heap=new int[len];
	        for (int i=0;i<len;i++) {
	            insert(arr[i]);
	        }
	    }
	    public void insert(int num)  {
	        if (isFull()){
	            len=(int) (len*capacity);
	            int tem[] =new int[len];
	            for (int i=0;i<size;i++)
	                tem[i]=heap[i];
	            heap=tem;
	        }
	        int i = size;//指向插入元素后堆中的最后一个元素的位置
	        for(;i>0 && heap[(i-1)/2]>num;i=(i-1)/2){
	            heap[i] = heap[(i-1)/2];
	        }
	        heap[i] = num;
	        size++;
	    }
	    public  void adjust(int heap[] ,int end){
	        for(int i=(end-1)/2;i>=0;i--){
	            int k=i;
	            while(k*2+1<=end){
	                int j=2*k+1;
	                if(j<end){
	                    if(heap[j]>heap[j+1]){
	                        j++;
	                    }
	                }
	                if(heap[k]>heap[j]){
	                    swap(heap,k,j);
	                    k=j;
	                }else{
	                    break;
	                }
	            }
	        }
	    }
	    public void sort(){
	        sort(heap);
	    }
	    public  void sort(int arr[]){
	        int len=arr.length;
	        for (int i=0;i<len;i++) {
	            adjust(arr, len - 1 - i);
	            swap(arr, 0, len - i - 1);
	        }
	        int i=0,end=arr.length-1;
	        while (i<end){
	            swap(arr,i,end);
	            i++;end--;
	        }
	
	    }
	}