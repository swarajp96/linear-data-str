# linear-data-str
linear data structures
#!/usr/bin/env python
# coding: utf-8

# Q1. Write a program to find all pairs of an integer array whose sum is equal to a given number?
# 
# 

# In[50]:


def sum_find(sum,n,array):
    
    count=0
    
    for i in range(0,n):
     
        for j in range(i+1,n):
        
            if array[i] + array[j] == sum:
                count+=1

    return count


array = [8,5,7,6,-1,3,1,4]            
sum = 7
n=len(array)
print(sum_find(n,sum,array))


# Q2. Write a program to reverse an array in place? In place means you cannot create a new array. You have to update the original array.
# 
# 

# In[51]:


def reverse_array(arr):
    arr.reverse()
    return arr
    
#--------------------------Input    
A = [5,10,7,84,5,4,85]   
reverse_array(A)


# Q3. Write a program to check if two strings are a rotation of each other?
# 
# 

# In[52]:


def rotation(str1, str2):
    if len(str1) != len(str2):
        return False
    temp = str1 
    if temp.count(str2)> 0:
        return True
    return False

# ------------------------------Input
str1 = "ABCD"
str2 = "ABCD"
rotation(str1,str2)


# Q4. Write a program to print the first non-repeated character from a string?
# 
# 

# In[53]:


def non_repeated_Char(str1):
    char_order = []
    counts = {}
    for i in str1:
        if i in counts:
            counts[i] += 1
        else:
            counts[i] = 1
            char_order.append(i)
    for c in char_order:
        if counts[c] == 1:
            return c
    return None


#----------------------------- Input

non_repeated_Char('ADADSFGDHDHGQW')


# Q5. Read about the Tower of Hanoi algorithm. Write a program to implement it.
# 
# 

# In[54]:


def TowerOfHanoi(n , from_rod, to_rod, aux_rod):
    if n == 1:
        print("Move disk 1 from rod",from_rod,"to rod",to_rod)
        return
    TowerOfHanoi(n-1, from_rod, aux_rod, to_rod)
    print("Move disk",n,"from rod",from_rod,"to rod",to_rod)
    TowerOfHanoi(n-1, aux_rod, to_rod, from_rod)
n = 2
TowerOfHanoi(n, 'A', 'C', 'B')


# Q6. Read about infix, prefix, and postfix expressions. Write a program to convert postfix to prefix expression.
# 
# 

# In[23]:


def p2p(exp_postfix):
    s=[]
    for i in exp_postfix:
        if i in ['+','-','*','/','^']:
            op1 = s[-1]
            s.pop()
            op2 = s[-1]
            s.pop()
            exp= i+op2+op1
            s.append(exp)
        else:
            s.append(i)
    
    ans = ""
    for i in s:
        ans += i
    return ans

p2p('AB+CD-*')


# Q7. Write a program to convert prefix expression to infix expression.
# 
# 

# In[55]:


def operator(x):
    if x == "+":
        return True
    if x == "-":
        return True
    if x == "*":
        return True
    if x == "/":
        return True
    return False

def prefix_to_infix(exp):
    list1 = []
    i = (len(exp)-1)
    while  i >=0:
        if not operator(exp[i]):
            list1.append(exp[i])
            i -= 1
        else:
            str1 = "(" + list1.pop() + exp[i] + list1.pop() + ")"
            list1.append(str1)
            i -= 1
    return list1.pop()
# -------------------------------Input
prefix = "*-A/BC-/AKL"
prefix_to_infix(prefix)


# Q8. Write a program to check if all the brackets are closed in a given code snippet.
# 

# In[24]:


def check(str):

    stack = []

    for c in str:

        if c in ["{", "(", "["]:

            stack.append(c)

        else:
            if stack.is_empty():

                print("[ERROR] : string not proper")

                return

        c_from_stack = stack.pop()

        if c_from_stack == "{" and c != "}":

            print("[ERROR] : string not proper")

            return

        if c_from_stack == "[" and c != "]":

            print("[ERROR] : string not proper")

            return

        if c_from_stack == "(" and c != ")":

            print("[ERROR] : string not proper")

            return

        if not stack.is_empty():

            print("[ERROR] : string not proper")

        print("All Good !!!")
        
    if stack:
        return False
    return True
    
check('{{[([{}])]')


# Q9. Write a program to reverse a stack.
# 
# 

# In[29]:


def insertAtBottom(stack, item):
    if isEmpty(stack):
        push(stack, item)
    else:
        temp = pop(stack)
        insertAtBottom(stack, item)
        push(stack, temp)


def reverse(stack):
    if not isEmpty(stack):
        temp = pop(stack)
        reverse(stack)
        insertAtBottom(stack, temp)


def createStack():
    stack = []
    return stack

def isEmpty( stack ):
    return len(stack) == 0


def push( stack, item ):
    stack.append( item )


def pop( stack ):


    if(isEmpty( stack )):
        print("Stack Underflow ")
        exit(1)

    return stack.pop()


def prints(stack):
    for i in range(len(stack)-1, -1, -1):
        print(stack[i], end = ' ')
    print()


stack = createStack()
push( stack, str(4) )
push( stack, str(3) )
push( stack, str(2) )
push( stack, str(1) )
print("Original Stack ")
prints(stack)

reverse(stack)

print("Reversed Stack ")
prints(stack)


# Q10. Write a program to find the smallest number using a stack.

# In[31]:





# In[56]:


from collections import deque

class MinStack:
    def __init__(self):
        self.s = deque()
        self.min = None
    def push(self, x):
        if not self.s:
            self.s.append(x)
            self.min = x
        elif x > self.min:
            self.s.append(x)
        else:
            self.s.append(2*x - self.min)
            self.min = x
    def pop(self):
        if not self.s:
            self.print("Stack underflow!!")
        top = self.s[-1]
        if top < self.min:
            self.min = 2*self.min - top
        self.s.pop()
    def minimum(self):
        output = self.min
        return output

#-----------------------------Input
s = MinStack()
s.push(6)
s.push(7)
s.push(5)
s.push(8)
s.push(3)
s.minimum()


# In[ ]:
