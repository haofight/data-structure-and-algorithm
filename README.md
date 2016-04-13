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
