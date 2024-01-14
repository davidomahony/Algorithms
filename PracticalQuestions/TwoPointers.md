# Two Pointers

### Valid Palindrome

This is a commonly asked question, people tend to solve it recursively or with a loop and two pointers. The main catch here is to make sure the preprocessing steps are done before we step into the actual logic.

Leet code Link: https://leetcode.com/problems/valid-palindrome/

```c#

    public bool IsPalindrome(string s) 
    {
        if (string.IsNullOrEmpty(s))
        {
            return false;
        }

        char[] characters = s.ToLower().Where(c => char.IsLetter(c) || char.IsDigit(c)).ToArray();
        if (characters.Length == 1)
        {
            return true;
        }

        return RecursiveAnagram(characters, 0, characters.Length - 1);
    }

    public bool RecursiveAnagram(char[] array, int left, int right)
    {
        if(left > right)
            return true;

        if (array[left] != array[right])
            return false;

        return RecursiveAnagram(array, left + 1, right - 1);
    }

```

#### Time & space complexity

In the preprocessing stage we step through everything once to lower it and ensure it is a valid character. So here we have an O(n) next we performs a recursive check wichc effectively goes two elements at a time. So roughly O(n) + O(n/2) which is O(n)

Time complexity = O(n)

For the space complexity because of how strings are handled in C# the string operation we do to make sure its all lower case with character will result in an O(n) space complexity as the rest is done in place from there using pointers.

Space complexity = O(n)

### 3 Sum 

### Finish
## This
### One

### Container With The Most Water

This question is relatively simple once you see the answer, but in an interview situation people have trouble trying to make the connection of when to move the pointers. The simple answer is you always want to keep track of the largest height. WHich ever height is shorter increment.

Leet code link: https://leetcode.com/problems/container-with-most-water/

```c#

    public int MaxArea(int[] height) 
    {
        int maxArea = 0;
        int left = 0;
        int right = height.Length -1;
        while (left < right)
        {
            maxArea = Math.Max(maxArea, 
                (Math.Min(height[left], height[right])) * (right - left));

            if (height[left] < height[right])
                left++;
            else 
                right--;
        }

        return maxArea;
    }

```

#### Time & Space complexity
As the two highest walls could be the last two heights we could end up stepping through each height giving us a time of O(n) inside this loop we perform basic calulations which is O(1). Therefor O(n).O(1) results in O(n)

Time Complexity = O(n)

Space complexity for this solution is pretty good as we only create thre integers which remains constant regardless of how large the input array is.

Space complexity = O(1)