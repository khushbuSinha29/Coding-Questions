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
TC-O(N), SC-O(N)

## Q3. Split the circular linked list in 2 halves 

#### Approach1

```
 void splitList(circular_LinkedList list)
        {
             //DO NOT REMOVE THESE 3 LINES
             Node head=list.head;
             Node head1=null;
             Node head2=null;
             
             //Modify these head1 and head2 here, head is the starting point of our original linked list.    
             
             
             //DO NOT REMOVE THESE 2 LINES
             list.head1=head1;
             list.head2=head2;
             
             if(head == null){
                 return;
             }
             
             Node curr= head;
             Node prev= null;
             int c=0;
             int totalNodes=0;
             while(curr.next!=head){
                 totalNodes++;
                 curr = curr.next;
             }
             int pod = 0;
             totalNodes++;
            //  checking for point of division of the node
             if(totalNodes % 2 == 0){
                 pod = totalNodes /2;
             }else{
                 pod = (totalNodes /2) + 1;
             }
             
             curr = head;
             head1 = head;
             
            //  for the 1st half 
             while(curr.next != head && c< pod){
                 prev = curr;
                 curr = curr.next;
                 c++;
             }
             prev.next = head;
             
             head2 = curr;
             
            //  for the 2nd half
             while(curr.next!=head){
                 curr = curr.next;
             }
             
             curr.next = head2;
       
            Node temp = head1;
// System.out.print("First half: ");
do {
    System.out.print(temp.data + " ");
    temp = temp.next;
} while (temp != head1);

System.out.println();

temp = head2;
// System.out.print("Second half: ");
do {
    System.out.print(temp.data + " ");
    temp = temp.next;
} while (temp != head2);
             
	 }
```
TC- O(n), SC- O(1)

#### Approach2:

```
 void splitList()
    {
        Node slow_ptr = head;
        Node fast_ptr = head;
 
        if (head == null) {
            return;
        }
 
        /* If there are odd nodes in the circular list then
         fast_ptr->next becomes head and for even nodes
         fast_ptr->next->next becomes head */
        while (fast_ptr.next != head
               && fast_ptr.next.next != head) {
            fast_ptr = fast_ptr.next.next;
            slow_ptr = slow_ptr.next;
        }
 
        /* If there are even elements in list then move
         * fast_ptr */
        if (fast_ptr.next.next == head) {
            fast_ptr = fast_ptr.next;
        }
 
        /* Set the head pointer of first half */
        head1 = head;
 
        /* Set the head pointer of second half */
        if (head.next != head) {
            head2 = slow_ptr.next;
        }
        /* Make second half circular */
        fast_ptr.next = slow_ptr.next;
 
        /* Make first half circular */
        slow_ptr.next = head;
    }
```

TC-O(N), SC-O(1)

## Q4: Given a list of 0 , 1 and 2 sort it.

####Approach 1:
```
class Solution
{
    static Node insertToTail(Node tail, Node curr){
        tail.next = curr;
        tail = curr;
        return curr;
    }
    //Function to sort a linked list of 0s, 1s and 2s.
    static Node segregate(Node head)
    {
       Node zeroHead = new Node(-1);
       Node zeroTail = zeroHead;
       Node oneHead = new Node(-1);
       Node oneTail = oneHead;
       Node twoHead = new Node(-1);
       Node twoTail = twoHead;
       
       Node curr = head;
    //   creating 3 seperate list. 
       while(curr != null){
           int val = curr.data;
           if(val == 0){
            zeroTail =  insertToTail(zeroTail, curr);
            // zeroTail.next = curr;
            // zeroTail = curr;
           }
           else if(val == 1){
             oneTail =  insertToTail(oneTail, curr);
            // oneTail.next = curr;
            // oneTail = curr;
           }else{
             twoTail = insertToTail(twoTail, curr);
            // twoTail.next = curr;
            // twoTail = curr;
           }
           curr = curr.next;
       }
       
    //   merge 2 list 
    if(oneHead.next != null ){
    //1s exist 
        zeroTail.next = oneHead.next;       
        
    } 
    else{
        zeroTail.next = twoHead.next;
    }
    oneTail.next = twoHead.next;
    twoTail.next = null;
    head = zeroHead.next;
    // System.out.println(head.data);
    return head;
}    
}

```

#### Approach 2:
We will be creating 3 seperate list for 0, 1 and 2. And later will merge all of them.
```
class Solution
{
    static void insertToTail(Node tail, Node curr){
        tail.next = curr;
        tail = curr;
    }
    //Function to sort a linked list of 0s, 1s and 2s.
    static Node segregate(Node head)
    {
       Node zeroHead = new Node(-1);
       Node zeroTail = zeroHead;
       Node oneHead = new Node(-1);
       Node oneTail = oneHead;
       Node twoHead = new Node(-1);
       Node twoTail = twoHead;
       
       Node curr = head;
    //   creating 3 seperate list. 
       while(curr != null){
           int val = curr.data;
           if(val == 0){
            //   insertToTail(zeroTail, curr);
            /*The reason why insertToTail(oneTail, curr); was not working properly is that Java is a pass-by-value language. This means that when we pass a variable to a function, a copy of the variable is made and any changes made to the variable inside the function are made on the copy, not the original variable.

In the insertToTail function, you are passing tail as a parameter. However, when you assign a new value to tail inside the function, here only modifying the copy of the tail variable that was created when the function was called. This has no effect on the original tail variable in the segregate function.*/

            zeroTail.next = curr;
            zeroTail = curr;
           }
           else if(val == 1){
            //   insertToTail(oneTail, curr);
            oneTail.next = curr;
            oneTail = curr;
           }else{
            //   insertToTail(twoTail, curr);
            twoTail.next = curr;
            twoTail = curr;
           }
           curr = curr.next;
       }
       
    //   merge 2 list 
    if(oneHead.next != null ){
    //1s exist 
        zeroTail.next = oneHead.next;       
        
    } 
    else{
        zeroTail.next = twoHead.next;
    }
    oneTail.next = twoHead.next;
    twoTail.next = null;
    head = zeroHead.next;
    // System.out.println(head.data);
    return head;
}
    
}
```
To make the above insertToTail function work

```
class Solution
{
    static Node insertToTail(Node tail, Node curr){
        tail.next = curr;
        tail = curr;
        return curr;
    }
    //Function to sort a linked list of 0s, 1s and 2s.
    static Node segregate(Node head)
    {
       Node zeroHead = new Node(-1);
       Node zeroTail = zeroHead;
       Node oneHead = new Node(-1);
       Node oneTail = oneHead;
       Node twoHead = new Node(-1);
       Node twoTail = twoHead;
       
       Node curr = head;
    //   creating 3 seperate list. 
       while(curr != null){
           int val = curr.data;
           if(val == 0){
            zeroTail =  insertToTail(zeroTail, curr);
            // zeroTail.next = curr;
            // zeroTail = curr;
           }
           else if(val == 1){
             oneTail =  insertToTail(oneTail, curr);
            // oneTail.next = curr;
            // oneTail = curr;
           }else{
             twoTail = insertToTail(twoTail, curr);
            // twoTail.next = curr;
            // twoTail = curr;
           }
           curr = curr.next;
       }
       
    //   merge 2 list 
    if(oneHead.next != null ){
    //1s exist 
        zeroTail.next = oneHead.next;       
        
    } 
    else{
        zeroTail.next = twoHead.next;
    }
    oneTail.next = twoHead.next;
    twoTail.next = null;
    head = zeroHead.next;
    // System.out.println(head.data);
    return head;
}
    
}

```