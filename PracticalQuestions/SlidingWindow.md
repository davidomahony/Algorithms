

## Sliding Window

### Problems


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