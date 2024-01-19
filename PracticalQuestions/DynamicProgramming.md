# Dynamic Programming


## Problems


### Climbing Stairs

```c#

    public int ClimbStairs(int n) 
    {
        if (n == 1)
            return 1;

        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;

        for (int i = 3; i <=n; i++)
        {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }

```

### Robber


```c#

    public int Rob(int[] nums) 
    {
        if (nums.Length == 1) return nums[0];
        
        var dp = new int[nums.Length];

        dp[0] = nums[0];
        dp[1] = Math.Max(dp[0], nums[1]);

        for (int i  = 2 ; i < nums.Length; i++)
        {
            dp[i] = Math.Max(dp[i - 2] + nums[i], dp[i - 1]);
        }

        return dp[dp.Length - 1];
    }

```