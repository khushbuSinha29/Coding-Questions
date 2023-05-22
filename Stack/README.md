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

## Q7: Sort a stack

```
class GfG{
    public void insertSorted(Stack<Integer> s, int val){
        if(s.isEmpty() || (!s.isEmpty() && s.peek()<val)){
            s.push(val);
            return;
        }
        int num = s.pop();
        insertSorted(s,val);
        s.push(num);
        
    }
	public Stack<Integer> sort(Stack<Integer> s)
	{
		//add code here.
		if(s.isEmpty()){
		    return s;
		}
		int val = s.pop();
		
		sort(s);
		
		insertSorted(s, val);
		return s;
	}
}
```
TC- O(N2), SC-O(N)

## Q8: Expression contain redundant brackets or not

```
class Solution {
    public static int checkRedundancy(String s) {
        // code here
        Stack<Character> st = new Stack<>();
        
        for(int i=0;i<s.length();i++){
            char ch = s.charAt(i);
            //if contain ( or operator then add it to the stack
            if(ch=='(' || ch=='+'|| ch=='-'||ch=='*'||ch=='/'){
                st.push(ch);
            }
            else if(ch==')'){
                // if contain ) then first check if the top has opening bracket if it has then this is redundant for cases like ((b)) but if there is operator then pop the value until you find the ( and then pop the ( again so that we will be checkign the next set. 

                char topCharacter = st.peek();
                if(topCharacter=='('){
                    return 1;
                }else{
                    while(st.peek()!='('){
                        st.pop();
                    }
                    st.pop();
                }
            }
            
        }
        if(st.isEmpty()){
                return 0;
            }
            else{
                return 1;
            }
    }
}       
```
TC- O(N), SC-O(N)

## Q9: minimum cost to make string valid 

```
int findMinimumCost(String str){
    //odd condition 
    if(str.length()%2 == 1){
        return -1;
    }
    Stack<Character> st = new Stack<>();

    for(int i=0;i<str.length(); i++){
        char ch= str.charAt(i);
        if(ch=='{'){
            s.push(ch);
        }else{
            //ch is closed brace
            if(!st.isEmpty() && s.top() = '('){
                s.pop();
            }
            else{
                s.push(ch);
            }
        }
    }
    //stack contain invalid expression
    int a=0, b=0;
    while(!st.isEmpty()){
        if(st.top == '('){
            b++;
        }else{
            a++;
        }
        s.pop();
    }
    int ans = (a+1)/2 + (b+1)/2;
    return ans;
}
```

## Q10. Next smallest element

Approach 1:

```
class Solution {
	public static int[] help_classmate(int arr[], int n) 
	{ 
	    int newArr[] = new int[n];
	    boolean hasMin = false;
	    int k=0;
	   // outer loop for keeping track of each element
	    for(int i=0;i<n-1;i++){
	        int min = -1;
	       // inner loop for checking for the smallest no.
	        for(int j=i+1;j<n;j++){
	            if(arr[j]<arr[i]){
	                min = arr[j];
	                hasMin = true;
	                break;
	            }
	        }
	        if(hasMin){
	            newArr[k++] = min;
	        }
	        else{
	            newArr[k++] = -1;
	        }
	        hasMin=false;
	    }
	    newArr[n-1] = -1;
	    return newArr;
	} 
}

```
TC - O(N2) , SC - O(N)

Approach 2: using stack

```
class Solution {
	public static int[] help_classmate(int arr[], int n) 
	{ 
	    // Your code goes here
	    int ans[] = new int[n];
	    Stack<Integer> s = new Stack<>();
	    s.push(-1);
	    for(int i=n-1;i>=0;i--){
	        int curr = arr[i];
	        while(s.peek()>= curr){
	            s.pop();
	        }
	        ans[i] = s.peek();
	        s.push(curr);
	    }
	    return ans;
	} 
}
```
TC - O(N), SC - O(N)

## Q11. Largest rectangle in histogram

```
class Solution {
    public int[] nextSmallestElement(int[] arr, int n){
         int ans[] = new int[n];
	    Stack<Integer> s = new Stack<>();
	    s.push(-1);
	    for(int i=n-1;i>=0;i--){
	        int curr = arr[i];
	        while(s.peek()!= -1 && arr[s.peek()]>= curr){
	            s.pop();
	        }
	        ans[i] = s.peek();
	        s.push(i);
	    }
	    return ans;
    }

    public int[] prevSmallestElement(int[] arr, int n){
          int ans[] = new int[n];
	    Stack<Integer> s = new Stack<>();
	    s.push(-1);
	    for(int i=0;i<n;i++){
	        int curr = arr[i];
	        while(s.peek()!= -1 && arr[s.peek()]>= curr){
	            s.pop();
	        }
	        ans[i] = s.peek();
	        s.push(i);
	    }
	    return ans;
    }
    public int largestRectangleArea(int[] heights) {

        int n = heights.length;
        int next[] = new int[n];
        next = nextSmallestElement(heights, n);
        int prev[] = new int[n];
        prev = prevSmallestElement(heights, n);
        int area = Integer.MIN_VALUE;
        for(int i=0;i<n;i++){
            int l = heights[i];
            if(next[i] == -1){
                next[i] = n;
            }
            int b = next[i] - prev[i] - 1;
            int newArea = l*b;
            area = Math.max(area, newArea);
        } 
        return area;
    }
}

```
TC - O(N), SC-O(N)

