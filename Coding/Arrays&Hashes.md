# Arrays And Hashes

The goal of this document is to look at common live coding questions to try and identify a pattern for solving these problems along with identifying what we should learn from a specific problem. We will start with easy problems to hard.


## Problems

### Contains Duplicate

Leet code link --> https://leetcode.com/problems/contains-duplicate/

```c#
    {
        if (nums == null || nums.Length == 0)
            return false;

        HashSet<int> set = new HashSet<int>();
        foreach (var itm in nums)
        {
            if (set.Contains(itm)) return true;
            else set.Add(itm);
        }

        return false;
    }
```

This is a pretty basic problem with the aim of getting used to iterating through an array and solving the problem with various data structures. In this case a hash set is ideal, with a hash set you can not have keys with the same value. Due to how a hash set operates.

#### Points to note about hashsets and dictionaries

##### Operations

##### Questions

