# data-structure-and-algorithm
基本数据结构与算法


import java.util.Scanner;
import java.util.Arrays;
public class XuanJu {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
        int pnum = 0;//参加选举的人数
        while(scan.hasNextInt()){
        	pnum = scan.nextInt();
        	int[] ticket = new int[pnum];
        	for(int i=0;i<pnum;i++)
        		ticket[i] = scan.nextInt();
        	
        	System.out.println(needTicket(0,ticket));
        	
        	
        }
        
     scan.close();
	}
	
	public static int needTicket(int p,int[] ticket){
		int per = ticket[p];
		int count = 0;
		int tickets = 0;
		//求出数组中票数比需获胜的票数多的人数
		for(int i=0;i<ticket.length;i++){
			if(ticket[i]>per)
				count++;
		}
		
		if(count==0){
			int[] t = new int[ticket.length-1];
			for(int i=0,j=0;i<t.length-1 && j<ticket.length-1;j++){
				if(p!=j){
					t[i++] = ticket[j];
				}
			}
			
			Arrays.sort(t);
			if(per>t[t.length-1]){
				return 0;
			}else if(per==t[t.length-1]){
				tickets = 1;
			}
				
		}else{
		int[] tmp = new int[count+1];
		tmp[0] = per;
		for(int i=0,j=1;i<ticket.length && j<tmp.length;i++){
			if(ticket[i]>per){
				tmp[j++] = ticket[i];
			}	
		}
		
		Arrays.sort(tmp);
		int sum = 0,avg = 0;
		for(int i=0;i<tmp.length;i++){
			sum += tmp[i];
		}
		avg = sum/tmp.length;
		while(per<tmp[tmp.length-1]){
		per += (tmp[tmp.length-1]-avg);
		tickets += (tmp[tmp.length-1]-avg);
		tmp[tmp.length-1] -= (tmp[tmp.length-1]-avg);
		Arrays.sort(tmp,1,tmp.length);
		}
		if(per==tmp[tmp.length-1]){
			per += (tmp[tmp.length-1]-1);
			tickets += 1;
		}
		
		}
		/*
		for(int i=0;i<ticket.length;i++){
    		System.out.print(ticket[i]+" ");
    	}
    	System.out.println();
		*/
		return tickets;
	}

}


/**
 * 判断三子棋输赢
 * 有A，B两个人，A在棋盘画‘X’，B在棋盘画‘0’。开局时A先画，其次是B。
 * 给定任意一个棋局要求判断谁赢，或者下一步该谁走，或者是平局，或者棋局不合理
 */
import java.util.Scanner;
public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		Scanner scan = new Scanner(System.in);
		char[][] ch = new char[3][3];
	    String[] str = new String[3];
	    while(scan.hasNext()){
        for(int i=0;i<3;i++)
	       str[i] = scan.next();
	   
	    

	    for(int p=0;p<3;p++)
	    	for(int q=0;q<3;q++){
	    		ch[p][q] = str[p].charAt(q);
	    	}
	    
	    int anum=0,bnum=0,cnum=0; //anum表示A在棋盘中的棋子数，bnum表示B在棋盘中的棋子数，cnum表示棋盘中空格数
	    for(int p=0;p<3;p++)
	    	for(int q=0;q<3;q++){
	    		if(ch[p][q]=='X'){
	    			anum++;
	    		}else if(ch[p][q]=='0'){
	    			bnum++;
	    		}else{
	    			cnum++;
	    		}
	    	}
	    
	    if(Math.abs(anum-bnum)>1){
	    	System.out.println("输入棋局不合法");     //输入棋局不合法
	    }else{
	    	if(anum>bnum){
	    		if(isWon('X',ch)){
	    			System.out.println("x won");   //A赢
	    		}else if(cnum==0){
	    			System.out.println("dow");     //平局
	    		}else{
	    			System.out.println("0 run");   //下一步B先走
	    		}
	    	}else{
	    		if(isWon('0',ch)){
	    			System.out.println("0 won");  //B赢
	    		}else if(cnum==0){
	    			System.out.println("dow");   //平局
	    		}else{
	    			System.out.println("x run");  //下一步A先走
	    		}
	    		
	    	}
	    	
	    }
	    
	    
	 }		
     scan.close();
	}
	
   /**
    * 判断哪一个赢
    * @param t  表示‘0’或‘X’
    * @param ch 当前棋局
    * @return
    */
	
	public static boolean isWon(char t,char[][] ch){
		for(int i=0;i<3;i++){
			if(ch[i][0]==t &&ch[i][1]==t &&ch[i][2]==t )
				return true;
		}
		
		for(int j=0;j<3;j++){
			if(ch[0][j]==t &&ch[1][j]==t &&ch[2][j]==t )
				return true;
		}
		
		if(ch[0][0]==t &&ch[1][1]==t &&ch[2][2]==t )
			return true;
		
		if(ch[0][2]==t &&ch[1][1]==t &&ch[2][0]==t )
			return true;
		
		return false;
	}

}
