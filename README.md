class Solution {
    public int minDistance(String word1, String word2) {
        // Use the shorter string for the DP array
        if (word1.length() < word2.length()) {
            String temp = word1;
            word1 = word2;
            word2 = temp;
        }

        int m = word1.length();
        int n = word2.length();

        int[] dp = new int[n + 1];

        // Convert empty string to word2
        for (int j = 0; j <= n; j++) {
            dp[j] = j;
        }

        for (int i = 1; i <= m; i++) {
            int prev = dp[0];
            dp[0] = i;

            for (int j = 1; j <= n; j++) {
                int temp = dp[j];

                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[j] = prev;
                } else {
                    dp[j] = 1 + Math.min(
                        prev,                  // Replace
                        Math.min(dp[j],       // Delete
                                 dp[j - 1])   // Insert
                    );
                }

                prev = temp;
            }
        }

        return dp[n];
    }
}
