# data-structure-and-algorithm
基本数据结构与算法


import java.util.ArrayList;
import java.util.Scanner;
/**
 * 构造Huffman树
 * @author Administrator
 *
 */
public class HuffmanTree {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		ArrayList<Node> arr = new ArrayList<Node>();
		Scanner scan = new Scanner(System.in);
		while(scan.hasNextInt()){
			arr.add(new Node(scan.nextInt()));

		}
		HuffmanTree ht = new HuffmanTree(arr);
		ht.printHuffmanTree();
		scan.close();
		
	}

	
	
	/**
	 * 定义节点
	 * @author Administrator
	 *
	 */
	private static class Node implements Comparable{
		Node(int element){
			this(element,null,null,null);
		}
		
		Node(int element,Node parent,Node left,Node right){
			this.element = element;
			this.parent = parent;
			this.left = left;
			this.right = right;

		}
		
		int element;
		Node parent;
		Node left;
		Node right;
		/**
		 * @Override
		 * @param t
		 * @return
		 */
		public int compareTo(Object t){
			return this.element - ((Node)t).element;
		}
	}
	
	private Node root = null;
	
	public HuffmanTree(ArrayList<Node> arr){
		int count = arr.size();
		while(count>1){
			Node left = null;
			Node right = null;
			Node parent = null;
			int i=0,j=0,p=0,q=0;
		 // 找出节点链表中最小的两个节点
	     for(i=0,left=arr.get(0);i<count;i++){
	    	 if((arr.get(i).compareTo(left))<0){
	    		 left = arr.get(i);
	    		 p = i;
	    	 }
	     } 
	     arr.remove(p);
	     
	     for(j=0,right=arr.get(0);j<count-1;j++){
	    	 if(arr.get(j).compareTo(right)<0){
	    		 right = arr.get(j);
	    		 q = j;
	    	 }
	     }
	     arr.remove(q);
	    
	     int pelement = left.element+right.element;
	     parent = new Node(pelement);
	     left.parent = parent;
	     right.parent = parent;
	     parent.left = left;
	     parent.right = right;
	     arr.add(parent);
	     count--;
	     if(count==1)
	    	 root = parent;
		}
		
	}
	
	public boolean isEmpty(){
		return root == null;
	}
	
	public void printHuffmanTree(){
		if(isEmpty())
			System.out.println("Empty Tree");
		else
			printHuffmanTree(root);
	}
	
	private void printHuffmanTree(Node t){
		if(t!=null){
			System.out.println(t.element);
			printHuffmanTree(t.left);
			printHuffmanTree(t.right);
		}
	}
	
	

}
