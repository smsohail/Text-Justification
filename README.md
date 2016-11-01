
public class TextJ {

	public String one(String words[], int width){
		int cost[][] = new int[words.length][words.length];
		for(int i=0;i<words.length;i++){
			cost[i][i] = width - words[i].length();
			for(int j=i+1;j<words.length;j++){
				cost[i][j] = cost[i][j-1] - words[j].length() - 1;
			}
		}
		for(int i=0;i<words.length;i++){
			for(int j=0;j<words.length;j++){
				if(cost[i][j]<0)
					cost[i][j] = Integer.MAX_VALUE;
				else
					cost[i][j] = (int)Math.pow(cost[i][j], 2);
			}	
		}
		int mincost[] = new int[words.length];
		int result[] = new int[words.length];
		for(int i=words.length-1;i>=0;i--){
			mincost[i] = cost[i][words.length-1];
            result[i] = words.length;
			for(int j=words.length-1;j>i;j--){
				if(cost[i][j-1] == Integer.MAX_VALUE)
					continue;
				if(mincost[i]>mincost[j]+cost[i][j-1]){
					mincost[i] = mincost[j]+cost[i][j-1];
					result[i] = j;
				}
			}
		}
		int i=0;
		int j;
		System.out.println("Minimum cost is " + mincost[0]);
        System.out.println("\n");
		StringBuilder builder = new StringBuilder();
		do{
			j=result[i];
			for(int k=i;k<j;k++){
				builder.append(words[k]+" ");
			}
			builder.append("\n");
			i=j;
		}while(j<words.length);
		return builder.toString();
	}
	public static void main(String[] args){
		String words[] = {"Tushar","Roy","likes","to","code"};
		TextJ a = new TextJ();
		System.out.println(a.one(words,10));
	}

	}


