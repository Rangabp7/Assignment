# Assignment
package com.Assignment;

public class Infrastructure {
	public static int maxRank(int n, int[][] cables) {
		int[] labCount = new int[n];
		boolean[][] directlyConnected = new boolean[n][n];

		// count the number of cables connected to each lab
		for (int[] cable : cables) {
			int lab1 = cable[0];
			int lab2 = cable[1];

			labCount[lab1]++;
			labCount[lab2]++;

			directlyConnected[lab1][lab2] = true;
			directlyConnected[lab2][lab1] = true;
		}

		int maxRank = 0;

		// calculate the network rank of each pair of labs
		for (int i = 0; i < n; i++) {
			for (int j = i + 1; j < n; j++) {
				int networkRank = labCount[i] + labCount[j];

				if (directlyConnected[i][j]) {
					networkRank--;
				}

				if (networkRank > maxRank) {
					maxRank = networkRank;
				}
			}
		}

		return maxRank;
	}

}
package com.Assignment;

import java.util.Scanner;

public class InfrastructureApp {
	public static void main(String[] args) {
		System.out.println("Please enter a number of labs");
		Scanner scan=new Scanner(System.in);
		int n=scan.nextInt();

		System.out.println("Enter array length");
		//Creating 2D array by taking input from the user
		int [][]cables=new int	[scan.nextInt()][scan.nextInt()];
		for(int i=0;i<=cables.length-1;i++)
		{
			for(int j=0;j<=cables[i].length-1;j++)
			{
				System.out.println("Enter a Element");
				cables[i][j]=scan.nextInt();
			}
		}
		//Display array contents
		System.out.println("Display array are");
		for(int i=0;i<=cables.length-1;i++)
		{
			for(int j=0;j<=cables[i].length-1;j++)
			{
				System.out.print(cables[i][j] + " ");
			}
			System.out.println();
		}
		int maxRank = Infrastructure.maxRank(n, cables);
		System.out.println("Maximum Rank is "+maxRank);
	}
}
Output:

Example 1:
input:n=4 and cables={{0,1},{0,3},{1,2},{1,3}};
output:Maximum Rank is 4

Example 2:
input:n=4 and cables={{0,1},{0,3},{1,2}};
output:Maximum Rank is 3

For Example 1:
Please enter a number of labs
4
Enter array length
4
2
Enter a Element
0
Enter a Element
1
Enter a Element
0
Enter a Element
3
Enter a Element
1
Enter a Element
2
Enter a Element
1
Enter a Element
3
Display array are
0 1 
0 3 
1 2 
1 3 
Maximum Rank is 4

for Example 2:
Please enter a number of labs
4
Enter array length
3
2
Enter a Element
0
Enter a Element
1
Enter a Element
0
Enter a Element
3
Enter a Element
1
Enter a Element
2
Display array are
0 1 
0 3 
1 2 
Maximum Rank is 3

