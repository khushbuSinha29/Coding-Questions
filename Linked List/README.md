## Q1. Remaove Duplicates from Sorted Linked list 

### Approach 1: Took two pointers curr and next. If the values are equal we will just move the next pointer and when the value are differnt, then we are moving the curr pointer as well in order to remove the duplicate.
```
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode curr = head;
        ListNode next;
        if(head==null){
            return head;
        }
        if(curr.next == null){
            return head;
        }
         next = curr.next;

        while(next != null){

        if(curr.val == next.val){
            next = next.next;
        }
        if(next!=null && curr.val != next.val){
            curr.next = next;
            curr = next;
            next = next.next;
        }
        if(next == null && curr.next !=null){
            curr.next =  null;
        }
        }
        return head;
        
    }
}
```
Here Time Complexity - O(n)
    Space complexity - O(1)

### Approach 2: 
```
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
    if(head == null){
        return null;
    }

    ListNode curr = head;

    while(curr != null){
        if((curr.next != null) && curr.val == curr.next.val){
            curr.next = curr.next.next;
        }
        else{
            curr = curr.next;
        }
    }
    return head;
        
    }
}
```

TC - O(N)
SC - O(1)

## Q2. Remove duplicates from unsorted linked list.

```
class Solution
{
    //Function to remove duplicates from unsorted linked list.
    public Node removeDuplicates(Node head) 
    {
         // Your code here
         if(head==null){
             return null;
         }
         Node temp = head;
         
         int maxnum=-1;
        //  Finding the maximum number in the linked list
         while(temp!=null){
             if(temp.data>maxnum){
                 maxnum= temp.data;
             }
             temp = temp.next;
         }
         
        
         int hashArr[] = new int[maxnum+1];
         temp = head;
         Node prev = null;
         
        //  Checking for the values in the arr. If the val is not present in the array
        // we increment the value of arr and move the pointers. If the value already came before
        // then in that case we move the current pointer to next and previous pointer to the curr pointer.
         while(temp!=null){
             if(hashArr[temp.data]==0){
                 hashArr[temp.data]++;
                 prev = temp;
                 temp = temp.next;
             }else{
                 temp = temp.next;
                 prev.next = temp;
             }
         }
         return head;
    }
}
```
