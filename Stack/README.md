##Q1. Implement 2 stacks in an Array
There is only one array and we need to implement 2 stack operation in a single array

```

/* Structure of the class is
class TwoStack
{
	int size;
	int top1,top2;
	int arr[] = new int[100];

	TwoStack()
	{
		size = 100;
		top1 = -1;
		top2 = size;
	}
}*/

class Stacks
{
    //Function to push an integer into the stack1.
    void push1(int x, TwoStack sq)
    {
        if(sq.top2 - sq.top1 > 1){
            sq.top1++;
            sq.arr[sq.top1] = x;
        }
        // else{
        //     System.out.ptintln("Stack Overflow");
        // }
        
    }

    //Function to push an integer into the stack2.
    void push2(int x, TwoStack sq)
    {
        if(sq.top2 - sq.top1 >1){
            sq.top2--;
            sq.arr[sq.top2] = x;
            
        }
        // }else{
        //     System.out.println("Stack overflow");
        // }

    }

    //Function to remove an element from top of the stack1.
    int pop1(TwoStack sq)
    {
        if(sq.top1>-1){
        int val = sq.arr[sq.top1];
        sq.top1--;
            return val;
        }else{
            return -1;
        }
        
    }

    //Function to remove an element from top of the stack2.
    int pop2(TwoStack sq)
    {
        if(sq.top2<sq.size){
            int val = sq.arr[sq.top2];
            sq.top2++;
            return val;
        }
        else{
            return -1;
        }
        
    }
}
```
## Q2. Reverse a string using stack

```
class Solution {
    
    public String reverse(String S){
        //code here
        Stack<Character> s = new Stack<>();
        String newString = "";
        int len = S.length();
        for(int i=0;i<len;i++){
            char ch = S.charAt(i);
            s.push(ch);
        }
        
        while(!s.empty()){
            char c = s.pop();
            newString = newString + c;
            // s.pop();
            
        }
        return newString;
    }

}
```
TC - O(N), SC- O(N)

##Q3. Delete middle element of a stack
```
class Solution
{
    //Function to delete middle element of a stack.
    public void solve(Stack<Integer>s, int size, int count){
        if(count == size/2){
            s.pop();
            return;
        }
        int num = s.peek();
        s.pop();
        
        // recursive call
        solve(s, size, count+1);
        s.push(num);
    }
    public void deleteMid(Stack<Integer>s,int sizeOfStack){
        // code here
        int count = 0;
        solve(s, sizeOfStack, count);
    } 
}

```
## Q4. Valid Parentheses

Approach 1 : using stack

```
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack<>();

        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            // if opening bracket, push in the stack
            if(ch=='(' || ch=='[' || ch=='{'){
                st.push(ch);

            }else{
                // if closing bracket, pop from the stack

                if(st.isEmpty()){
                    return false;
                }
            char top = st.peek();
            if((ch==')' && top == '(') || (ch==']' && top=='[') || (ch=='}' && top=='{')){
                st.pop();
            }else{
                return false;
            }
            }
        }
        if(!st.isEmpty()){
            return false;
        }
            return true;
    }
}
```
TC- O(N), SC-O(N)

Approach 2 - Without using stack
Taking a character array to store the open parantheses and maintaining count for that while return we decrement the counter and check for the closed parantheses.

```
class Solution {
    public boolean isValid(String s) {

        char charArray[] = new char[s.length()];
        int count=-1;
        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            if(ch=='(' || ch=='[' || ch=='{'){
                charArray[++count]=ch;
            }else{
                if(count>=0 && ((charArray[count]=='(' && ch==')') || (charArray[count]=='[' && ch==']') || (charArray[count]=='{' && ch=='}'))){
                    --count;
                }else{
                    return false;
                }
            }
        }
        return count==-1;
        
    }
}
```
TC-O(N), SC-O(N)

## Q5. Insert an element at the bottom of the stack

```
class Solution
{
    //Function to delete middle element of a stack.
    public void solve(Stack<Integer>s, int x){
        if(s.isEmpty()){
            s.pop();
            return;
        }
        int num = s.peek();
        s.pop();
        
        // recursive call
        solve(s, x);
        s.push(num);
    }
    public void pushBottom(Stack<Integer>s,int x){
        
        solve(s, x);
    } 
}
```
TC- O(N), SC-O(1)

## Q6. Reverse a stack

```
class Solution
{ 
    static void insertAtBottom(Stack<Integer> s, int n){
        if(s.isEmpty()){
            s.push(n);
            return;
        }
        int num = s.pop();
        insertAtBottom(s, n);
        s.push(num);
    }
    static void reverse(Stack<Integer> s)
    {
        if(s.isEmpty()){
            return;
        }
        int num = s.pop();
        
        reverse(s);
        insertAtBottom(s, num);
    }
}
```
TC - O(N2), SC-O(N)