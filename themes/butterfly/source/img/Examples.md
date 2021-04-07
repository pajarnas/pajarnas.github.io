Examples: 

1. [Leetcode]Destination City

2. [Leetcode]Next Greater Element I

3. [Leetcode]Number of Longest Increasing Subsequence

4. ```
   Question: 
   	Get minimum number of days of points you need to meet the goal
   Description:
    	points array reprents the points you can get each day
    	goals array is NOT sorted
    	get minimum number of days of points you need to meet the goal correspondingly
   
   input: 
        int[] points = {100, 300, 400, 500, 600}
        int[] goals = {400,200,700,900,1400}
   
   output: 
        int[] meetGoal = {2, 2, 3, 4, 5}
   
   explanation: 
   	for each element from goal array
           to reach 400, you need at least 100(day 1) + 300 (day 2), which returns 2
           to reach 200, same reason as above
           to reach 700, you need at least 100(day 1) + 300(day 2) + 400(day 3), which returns 3
           to reach 900, you need to have all points 100(day 1) + 300(day 2) + 400(day 3) + 500(day 4), which returns 4
           to reach 1400, you need to have all points 100(day 1) + 300(day 2) + 400(day 3) + 500(day 4) + 600(day 5), which returns 5
   
   Note: 
   	you cannot jump days, even though on day 3 you can score 400 points, you still need to get day 1 and day 2's points first     before get day 3's point
   
   required time complexity: 
   	O(NlogN) or better.
   ```

   

5. [leetcode] Longest Palindromic Substring
 URL: https://leetcode.com/problems/longest-palindromic-substring/

答案格式: 以第五题为例, 

        class Solution {
            public String longestPalindrome(String s) {
    
                    int len = s.length();
                    if(len <=0) return s;
    
                    boolean[][] dp = new boolean[len][len];
    
                    int x = 0;
                    int y = 0;
    
                    for(int g=0;g < len ; g++) {
                        for(int i=0, j= g; j < len ; i++, j++ ) {
                            if(g==0) {
                                dp[i][j] = true;
                            } else if (g==1) {
                                dp[i][j] =  (s.charAt(i) == s.charAt(j));
                            } else {
                                dp[i][j] =  (s.charAt(i) == s.charAt(j)) && dp[i+1][j-1];
                            }
    
                            if(dp[i][j] && j-i > y-x) {
                                x=i;
                                y=j;
    
                            }
                        }
                    }
                    return s.substring(x,y+1);
    
        }
}