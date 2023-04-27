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

## Q5. Merge 2 sorted linked list 
Idea we are using here is we will compare the values of the second list with the first list and if we find a value such that firstlist.val<secondlist.val<firstlist.next.value. Then in that case we insert the value. Else we will move the pointer.

```
class Solution {
    ListNode solve(ListNode list1, ListNode list2){

        // if only one list present in first list
        if(list1.next == null){
            list1.next = list2;
            return list1;
        }

        ListNode curr1 = list1;
        ListNode curr2 = list2;
        ListNode next1 = curr1.next;
        ListNode next2 = curr2.next;

        while(next1 != null && curr2 != null){

            if((curr1.val <= curr2.val) && (curr2.val <= next1.val)){
                // add node in between the 1st node
                curr1.next = curr2;
                next2 = curr2.next;
                curr2.next = next1;

                curr1 = curr2;
                curr2 = next2;
            }else{
                curr1 = next1;
                next1 = next1.next;

                if(next1 == null){
                    curr1.next = curr2;
                    return list1;
                }
            }
        }
        return list1;
    }
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {

        if(list1 == null)
            return list2;
        if(list2 == null)
            return list1;

        if(list1.val <= list2.val){
           return solve(list1, list2);
        }else{
           return solve(list2, list1);
        }
        
    }
}

```

## Q6: Check if the linked list is palindrome or not

Approach 1: Take an extra array, will copy the list data to array and then will check palindrome over array.

```
class Solution {
    public boolean isPalindrome(ListNode head) {

        ListNode temp = head;
        int countNode = 0;
        while(temp != null){
            countNode++;
            temp = temp.next;
        }
        int arr[] = new int[countNode];
        temp=head;
        int i=0;
        // copying values from list to array
        while(temp!=null){
            arr[i]=temp.val;
            i++;
            temp=temp.next;
        }

        // checking for palindrome in array
        i=0;
        int j= arr.length-1;
        while(i<=j){
            if(arr[i] != arr[j]){
                return false;
            }
            i++;
            j--;
        }
        return true;
        
    }
}

```

Approach 2: Here find the mid of the list, then from mid.next to null revese the 2nd half and then check for the values in both the halves, if differ then not palindrome, if same then palindrome.

```
 ListNode getMid(ListNode head){
        ListNode slow = head;
        ListNode fast = head.next;

        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
    ListNode reverse(ListNode temp){
        ListNode curr = temp;
        ListNode next = null;
        ListNode prev = null;

        while(curr != null){
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
    public boolean isPalindrome(ListNode head) {
        
        if(head == null || head.next == null){
            return true;
        }
        // find mid
        ListNode mid = getMid(head);

        // reverse list after mid
        ListNode temp = mid.next;
        mid.next = reverse(temp);

        // check both the halves , 1st from head to mid and 2nd from mid.next to null.
        ListNode head1 = head;
        ListNode head2 = mid.next;

        while(head2 != null){
            if(head1.val != head2.val){
                return false;
            }
            head1 = head1.next;
            head2 = head2.next;
        }
        // repeat step 2 , in order to make the list same.
        temp = mid.next;
        mid.next = reverse(temp);
        
        return true;

    }

```

## Q7 : Add 2 numbers represented by linked list 

```
class Solution{
    static Node reverse(Node head){
        Node prev = null;
        Node curr = head;
        Node next = null;
        
        while(curr!=null){
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
     
        return prev;
        
    }
    //Function to add two numbers represented by linked list.
    static Node addTwoLists(Node first, Node second){
        // code here
        // return head of sum list
        
       first = reverse(first);
       second = reverse(second);
       
       int carry = 0;
       Node temp1 = first;
       Node temp2 = second;
       Node sum = null;
       while(temp1!=null || temp2!=null || carry>0){
           int newVal = carry;
           if(temp1!=null)
                newVal +=temp1.data;
            
            if(temp2!=null)
                newVal +=temp2.data;
                
            carry = newVal/10;
            newVal = newVal%10;
            
            Node newNode = new Node(newVal);
            newNode.next = sum;
            sum = newNode;
            if(temp1!=null)
                temp1 = temp1.next;
            if(temp2!=null)
                temp2 = temp2.next;
       }
        return sum;
    }
}
```

## Q8. Clone a linked list with next and random pointers.

Approach 1: First we copy the linked list without considering the random link and normally cloned it. After that we created a map such that it contains the orignal list and the cloned list mapping like 1--1, 2---2, 3--3 so on. Next  we are traversing through the original list and setting the cloned.random = oldtonewnode[orginal.random], say for setting the 1 node random link clone we can check the original random link and then put that in oldnewnode which has track for every link.

```

class Clone {
    //Function to clone a linked list with next and random pointer.
    void insertAtTail(Node head, Node tail, int d){
        Node newNode = new Node(d);
        if(head == null){
            head = newNode;
            tail = newNode;
            return;
        }else{
            tail.next = newNode;
            tail = newNode;
        }
    }
    Node copyList(Node head) {
        // your code here
        // create a clone list
        Node cloneHead = null;
        Node cloneTail = null;
        Node temp = head;
        
        while(temp != null){
            Node newNode = new Node(temp.data);
            if(cloneHead == null){
                cloneHead = newNode;
                cloneTail = newNode;
            }else{
                cloneTail.next = newNode;
                cloneTail = newNode;
            }
                temp = temp.next;
        }
        
        //step 2: Create a map
        Map<Node, Node> oldToNewNode = new HashMap<Node, Node>();
        Node originalNode = head;
        Node cloneNode = cloneHead;
        while(originalNode != null){
            oldToNewNode.put(originalNode, cloneNode);
            originalNode = originalNode.next;
            cloneNode = cloneNode.next;
        }
        // resetting the pointers
        originalNode = head;
        cloneNode = cloneHead;
        
        //Step 3: mapping the original value and putting the cloned one.
        while(originalNode != null){
            cloneNode.arb = oldToNewNode.get(originalNode.arb);
            originalNode = originalNode.next;
            cloneNode = cloneNode.next;
        }
        return cloneHead;
        
        
    }
}

```
TC- O(N), SC-O(N)