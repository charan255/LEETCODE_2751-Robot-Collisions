class Solution:
    def survivedRobotsHealths(self, positions: List[int], healths: List[int], directions: str) -> List[int]:

""" Collision occurs when an element's direction is 'R' and its successor
element (in terms of position) is 'L'.So I added the health of the elements with R
direction into a stack until an element of L direction is found and I add the 
health of element with L direction into another list if the stack is empty"""

        def collision(n):  #This a function which handles Collision

            while stack:     
                if stack[-1][1]>n[1]: #Sorry guyz this is my first repository and I am already 
                    stack[-1][1]-=1   #fed up with giving all these details about the code.
                    return            #Please understand and have luck understanding this code.
                                      #I have no idea what I have written.
                elif stack[-1][1]==n[1]:
                    stack.pop()
                    return
                    
                else:
                    n[1]-=1
                    stack.pop()
            left.append(n)
                
                
        nl=[]
        p, h, d= positions, healths, directions
        
        if d=="R"*len(d) or d=="L"*len(d):
            return h
        
        for i in range(len(p)):
            nl.append([p[i],h[i],d[i],i+1])
        nl.sort()
        stack=[]
        left=[]
        
        for i in range(len(nl)):
            if nl[i][2]=="R":
                stack.append(nl[i])
            else:
                collision(nl[i])
                
        if left==[]:
            stack=sorted(stack,key=lambda x:x[3])
            return [x[1] for x in stack]
        elif stack==[]:
            left=sorted(left,key=lambda x:x[3])
            return [x[1] for x in left]
            
        else:
            if len(left)+len(stack)!=len(p):
                result=sorted(left+stack,key=lambda x:x[3])
                return [x[1] for x in result]
            else:
                return(h)
