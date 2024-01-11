# Two Pointers

### Valid Palindrome

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


### 3 Sum 


### Container With Most Water


