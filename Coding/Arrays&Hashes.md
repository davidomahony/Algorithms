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



