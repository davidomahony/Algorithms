

## Sliding Window

### Problems

#### Maxprofit

```c#

    public int MaxProfit(int[] prices) 
    {
        int minPrice = int.MaxValue;
        int maxProfit = 0;

        for (int i = 0 ; i < prices.Length; i++)
        {
            if (prices[i] < minPrice)
                minPrice = prices[i];
            else if ((prices[i] - minPrice) > maxProfit)
                maxProfit = prices[i] - minPrice;
        }

        return maxProfit;
    }

```

#### Longest string without a repeating character

```c#

    public int LengthOfLongestSubstring(string s) 
    {
        int max = 0;
        HashSet<char> track = new HashSet<char>();
        var array = s.ToArray();
        for (int i = 0 ; i < s.Length; i++)
        {
            int count = 0;
            while ((count + i) < s.Length && !track.Contains(array[count + i]) )
            {
                track.Add(array[count + i]);
                count++;
            }

            max = Math.Max(max, track.Count);
            track.Clear();
        }

        return max;
    }

```