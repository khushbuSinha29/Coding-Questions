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

