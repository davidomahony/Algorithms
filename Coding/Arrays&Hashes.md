# Arrays And Hashes

The goal of this document is to look at common live coding questions to try and identify a pattern for solving these problems along with identifying what we should learn from a specific problem. We will start with easy problems to hard.

## Problems

### Contains Duplicate

Leet code link --> https://leetcode.com/problems/contains-duplicate/

```c#
    public bool ContainsDuplicate(int[] nums) 
    {
        if (nums == null || nums.Length == 0)
            return false;

        HashSet<int> set = new HashSet<int>();
        foreach (var itm in nums)
        {
            if (set.Contains(itm)) 
                return true;
            else 
                set.Add(itm);
        }

        return false;
    }
```

This is a pretty basic problem with the aim of getting used to iterating through an array and solving the problem with various data structures. In this case a hash set is ideal, with a hash set you can not have keys with the same value.

#### Time and space complexity
We iterate once through the given array so assuming the duplicate is at the very end we would have to go through all elements once. As we add more elements this grows, meaning it cant be O(1) as its not constant. Leaving us with O(n) for the loop. But inside the look we call two hashset operations this is completed using O(1)

So Time complexity = O(n)

For the space complexity the only fields we add is the hashset for identifying duplicates, in the worst case where the last element is the duplicate we would have an input array and hashset more or less equal resulting in a linear space complexity.

So Space complexity = O(n)


#### Points to note about hashsets
When a new item is added to a hashset a hash is generated using a has function. This then decides what bucket to place the new object in. If the hash function is bad and every object ends up in the same bucket this can result in a time complexity of O(n).

*If the hash code of two objects are equal this does not prove these objects are identical. This is true only if the hashcode and the equals functions confirms equality, then can we assume both objects are identical.*

### Valid Anagrams

Another relatively basic problem better to ask more junior developers as its shows use of basic data structures such as arrays or dictionarys. There is also some slight "catchs". we will go through two relatively basic solutions.

https://leetcode.com/problems/valid-anagram


```c#
    public bool IsAnagram(string s, string t) 
    {
        if (s.Length != t.Length)
            return false;

        var freq = new Dictionary<char, int>();
        foreach (var c in s)
        {
            if (freq.TryGetValue(c, out int res))
                freq[c] = res + 1;
            else 
                freq.Add(c, 1);
        }

        foreach (var c in t)
        {
            if (freq.TryGetValue(c, out int res))
                freq[c] = res - 1;
            else 
                return false;
        }

        return freq.All(itm => itm.Value == 0);
    }
```

Once again we make use of a Dictionary to keep count of how often each character occurs. First we go through the first string populating our frequency dictionary. Second we iterate through the second array decrementing the count of the frequency. Finally we ensure all counts are 0 and return true based on this result.

*One potential catch here is not keeping count of the characters if so you will miss cases where a word has duplicate letters*

#### Time & Space
The main function contains two loops iterating through both arrays giving us two O(s) + O(t) inside each loop we do either one or two hashset operations both of O(1) resulting in O(s)*O(1)*O(1) which = O(s) the same can be said for O(t) giving us O(s) + O(t) which we change to O(n) out of ease

Time complexity = O(n)

As we only create a dictionary which can be equal to the size of the array or some what less depending on repeating characters we get a space complexity of O(n)

Space Complexity = O(n)



### Two Sum

Leetcode link --> https://leetcode.com/problems/two-sum

Two sum is one of the first array questions that poses a problem which is not immediately obvious. Normally people consider the greedy approach. This is effectively a "Get out of jail card" depending on the level of the interview this will be a passing score for me if you can accept identify the time and space results. 

As a result we will not step through the greedy approach. In order to complete this in one pass we need to have a way to identify the difference between a certain item and the target. Therefore we add each value to a dictionary as the index as the value. With each value we iterate ove we check the dictionary for the difference. If it exists then we have our two results. One trap people fall into here is they forget about the indices.

```c#
    public int[] TwoSum(int[] nums, int target) 
    {
        Dictionary<int, int> vals = new Dictionary<int, int>();
        for(int i  = 0 ; i < nums.Length; i++)
        {
            int diff = target - nums[i];
            if (vals.TryGetValue(diff, out int index))
                return new int[]{i, index};
            else
                vals.TryAdd(nums[i], i);
        }
        return default;
    }
```

#### Time & Space
The main function contains one loop iterating through the nums array, we then make use of a hashset for potentially two more operations O(n).O(1).O(1) which give us O(n)

Time complexity = O(n)

As we only create a dictionary which can be equal to the size of the array or some what less depending on repeating characters we get a space complexity of O(n)

Space Complexity = O(n)

*Note this problem is the first example where we show the use of a hashset can be used to achieve linear time complexity*

### Group Anagrams

Leet code link --> https://leetcode.com/problems/group-anagrams

Once again another array question where we need a hashmap to keep track of the various anagrams. The best way to do this is store each value in alphabetical in order in as a key in the dictionary. Then on each iteration we sort the string alphabetically and check if a key exists. If so we add the new word to the list of anagrams

| Anagram key | List of words for this anagram


```c#
    public IList<IList<string>> GroupAnagrams(string[] strs) 
    {
        Dictionary<string, IList<string>> inputs = new Dictionary<string, IList<string>>();
        foreach (var itm in strs)
        {
            var array = itm.ToArray();
            Array.Sort(array);
            string sorted = new string(array);
            if (inputs.TryGetValue(sorted, out IList<string> an))
                an.Add(itm);
            else
                inputs.Add(sorted, new List<string>(){itm});
        }

        return inputs.Select(x => x.Value).ToList();
    }
```

#### Time and Space complexity
Time complexity uses a loop for each element O(n) then we sory a smaller array which is not considered as there in theory should be small. But if these arrays were larges then N this could prooe costly. But for now it will just be considered constant O(1) + 2 O(1) for the hash set operations.

Time complexity: O(n)

Space complexity we has one dictionary which will contain N elements and worse case N keys result in O(n) space.

Space complexity: O(n)

### Top K Frequent Elements

This question is a pretty common as its relatively straight forward but requires a little bit of thinking and can lead to some nice questions on space and time complexity. Straight forward answer add integers as a key and increment the count of the value when you encounter them. Then reorder the array returning the two highest values


```c#

    public int[] TopKFrequent(int[] nums, int k) 
    {
        Dictionary<int, int> count = new Dictionary<int, int>();
        foreach (var num in nums)
        {
            if (count.TryGetValue(num, out int result))
                count[num] = result + 1;
            else
                count.Add(num, 1);
        }

        return count.OrderByDescending(x => x.Value)
                .Select(x => x.Key)
                .Take(k)
                .ToArray();
    }

```

#### Time and Space Complexity

We iterate over all the elements in nums giving us O(n) then we order the dictionary based on the values the average sorting complexity is O(n log n) with a worst case of O(n^2) resulting in O(n) + O(nlogn)

Time complexity: O(nlogn)

Space complexity is pretty much a dictionary for each element, so worst case 2 O(n) where we have no repeating elements.

Space complexity: O(n)

### Product Of Array Except Self


