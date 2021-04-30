# minimum-remove-to-make-valid-parentheses
# leetcode 1249

class Solution {
    fun minRemoveToMakeValid(s: String): String {
        
        var stack = mutableListOf<Int>()

        var arr = s.toCharArray()
        
        for(index in arr.indices){
            
            if(s[index] == '(') stack.add(index)  
            else if(s[index]==')'){
                
                // [valid case] we have an equivalant '(' for current ')'
                // so '(' does not nned to be replaced with #
                // so remove it from stack
                if(stack.size>0) stack.removeAt(stack.size-1)
                
                // no equivalant ) for current (
                // so mark it for removal
                else arr[index]  ='#'
            }
            
        }
        
        // mark everything left in stack for removal [replacement]
        for(i in stack) arr[i]='#'
        
        var res : StringBuilder = StringBuilder()
        for(c in arr) if (c!='#') res.append(c)
        
        return res.toString()
    }
}

/* Python sersion:

class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        stack = []
        s = list(s)
        for i in range(len(s)):
            if s[i] == "(": stack.append(i)
            elif s[i] == ")":
                if stack: stack.pop()
                else: s[i] = ""
        for i in stack:
            s[i] = ""
        return "".join(s)
    
from: https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/discuss/1073038/Python-or-Fast-and-Easy-or-Beats-98
*/
