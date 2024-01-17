

# Linked Lists

## Problems

### Reverse a linked list

```c#

    public ListNode ReverseList(ListNode head) 
    {
        var curr = head;
        var next = head.next;
        while (curr.next != null)
        {
            next = curr.next.next;;
            curr.next = curr;
        }

        return curr; 
    }

```