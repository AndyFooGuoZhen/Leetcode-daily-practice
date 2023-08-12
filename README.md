# Leetcode-daily-practice
Used for uploading notes for leetcode questions

# Arrays 

## 1. Contains duplicate
- Use set to keep track of duplicates
- if element is not inside, add it to set
- return true if element is inside of set 
- O(n) time


## 2. Valid anagram (check if 2 strings have characters of the same count)
- Use 2 hashmaps for keeping track counts of each element from 2 strings
- return true if both hashmaps are the same, else return false
- O(n) time

## 3. Two sum ( check if two elements in the list add up to target)
- Use hashmap for keeping track of elements
- if target - current element is in hashmap, return index of diff and index of current element
- else add element into hashmap, with index of the element as the value
- O(n) time

## 4. Group anagrams ( group strings with the same anagrams)
- Create a hashmap, where the value is a list type , use collections.defaultdict(list) for this
- Iterate through each string in list, while iterating use count = [0] * 26 to create a list holding 26 elements of 0
- for each string, iterate through each character and use ord() to get ascii value of character, essentially we are coutning the number of a specific character for each string
- convert the list into tuple form at the end, and add it to hashmap via append ( hashMap[tuple(count)].append(current string) ) 
- m be no of strings, n be longest length of a string, time = O(mn)
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/5f56bf04-b514-4221-b710-80f512546684">



## 5. Top k frequent elements
- Use bucket sort, index represent count of the element
- create a hashmap, and a list containing len(nums) + 1 empty lists ( list index at 3 means count of element = 3)
- iterate through number array and keep update count of elements in hashmap
- iterate through hashmap and append elements according to count into the empty lists
- iterate list from reverse and append elements from sublist into result list until length of k is reached
- O(n) time

## 6. Product of array except itself
- Given an array of integers , compute an answer array where each element is the product of arrray except itself
- Catch : Must do it in O(n), can't use division
- EX: Input : [2,3,4,5] , Output : [60, 40, 30, 24]
- Solution : Use prefix and postfix, prefix : product of elements before curr element, postfix: product of elements after curr element
- Do it in 2 pass, first iteration loop through array and compute prefix array
- Second pass, loop through array in reverse order to compute postfix array
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/f5743b84-1ff4-4a7f-9fe3-da75d375c847">
- To save memory, it can be done directly on the output array
- Note: prefix for 1st element is always 1, postfix for last element is always 1
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/03e99931-4b33-4dff-b176-b1e5ec070aff">
- O(n) time, O(n) memory


# Two pointers

## 1. Valid palindrome
- declare 2 pointers, one on first letter the other on last
- while left <= right, check if both letters match, else return false
- O(n) time

## 2. Two sum (Sorted)
- declare 2 pointers, one on first num, the other on last number
- compute sum, if sum is smaller, move left pointer to right, else move right pointer to left
- if i > j, return false, else return [i,j]
- O(n) time

## 3. Three Sum *****
- Start by sorting the num list O(nlogn)
- iterate through the list, for each iteration check if current is same as previous, if its the same , use continue to go to next number in list,
- declare left and right pointer, left pointing at current index + 1, right pointing at last number
- perform two sum , check if current + left + right is = 0
- if < 0, move left ptr to right, else if > 0, move right ptr to left, else = 0 move letf ptr to right, append to result and check while left < right and if nums[left] == nums[left + 1], move left ptr to right again
- O(n^2) time
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/6bfba150-64ee-4319-acc6-de62b1458db6">

## 4. Container with most water
- Given an array of heights, compute the max area that can be achieved by constructing a container using heights from array
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/4122a2a6-cac8-4d94-ba17-786207f47101">
- Solution: Use 2 pointer solution, 1 pointer at beginning , 1 at the end
- While leftPtr < rightPtr, compute area, if area is > than prev max, udpate max
- Then, check if leftPtr >= rightPtr, if true, shift rightPtr to left, else shift leftPtr to right (maximizing heights)
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/06ef2557-c1fe-4c68-b63f-d6ad366d18d8">
- Runs in O(n) time

# Sliding windows

## 1. Best time to buy stock
- Define a min and profit variable
- Iterate through the list, is the current is less than min, set that as new min
- Then calculate current - min and compare it to previous assigned profit, if new profit is larger, reassign profit
- O(n) time

## 2. Longest substring without repeating characters
- Define a set and left ptr
- Traverse the string by each character, if character not in set, calculate length by taking right ptr - left ptr + 1
- if character in set, start removing characters from left ptr until character no longer in set
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/14de8489-509c-45fd-9d84-4e7efd5acb18">
- O(n) time

## 3. Longest repeating character with replacement
- Define a countHashmap, left ptr and length
- Traverse the string by each character, for each character, increment its count using hashmap
- then in a while loop, check if current window size - max count of a charcater in hashmap > k
- if so, decrement count of character at left ptr in hashmap and move leftptr to the right
- calculate length of window and compare it to previous recorded max window length
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/237af54a-645a-4442-a1b1-330d6bbfb7d3">
- O(n) time

## 4. Permutation in string *****
- Given strings s1 and s2, return True if s2 contains a permutation of s1
- Example: s1 = "ab" , s2 = "cba", ans = true
- Solution: If s1 is longer than s2, just return false
- Use [0] and ord to keep track of letter count, set leftPtr = 0
- Depending on len of s1, we will have sliding window of len s1 
- After recording letter count for s1 and s2 (traversing len of s1), we slide the window of len(s1) to the right
- At each iteration check if letter count array matches, if so, return true, else reduce letter count of s2 at leftPtr and increase letter count at end of window, window always remain the side of len s1
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/a9fbe90b-2ee0-4cde-bbd7-bd26be817a5c">
- Runs in O(26 * len(S2)) time
- More optimal solution, instead of comparing two arrays via countS1 == countS2 everytime, use a match variable
- In detail, if two arrays match, match = 26, if so , return true
- Neetcode's approach updates the match variable everytime a new letter is added to the window
- Resulting in O(26 + len(S2)) time


# Stacks

## 1. Min stack
- In constructor, define list acting as a stack and a second list to keep track of min after each push is done
- When pushing new element to stack, check if element to be pushed is the min, if so , append that into min stack list
- When popping, pop element from list and min list
- When getting min of stack, return [-1] of min stack
- O(1) time

## 2. Generate parenthesis ( Given number n, the number of parenthesis, compute all possible well formed parenthesis
- Case 1: if openParenthesis == close == n, append it to result
- Case 2: if open parenthesis is < n, append it to current parenthesis string and recursively call method again, make sure to pop ( after calling method before going to second if case)
- Case 3; if close < open parenthesis, append close parenthesis to parenthesis string and recursively call method again ( make sure to pop, ensure close parenthesis is consistent)
- Tip , use "".join(list) to convert elements in list to one string before appending it to result list
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/d9350b87-1844-4ddf-b979-6ce6070bd852">

## 3. Daily temperatures
- Given an array of temperatures, return an array containing the no of days needed to wait for increase
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/a6564c57-40f3-4c36-b4fe-c4b2301770fd">
- Solution : Use a stack to keep track of temperatures and their index
- Iterate throught the temperatures, if current temperature is > than tempereature on top of stack, update index for temperature on top of stack with diff in indices, continue doing so until current < temperature on top of stack or nothing in stack
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/da7ad668-41d1-4e33-90f5-c36ee7d17de2">
- Runs in O(n) time



# Binary search

## 1. Koko eating bananas
- Monkey can want to eat n piles of bananas in h hours. ( h must be >= n, h cannot be less than n because at most, 1 pile is finished in 1 hour.) Length of piles <= h.
- Try to find k ( no of bananas from piles per hour) that monkey can eat at without rushing it. Monkey wants to space out eating bananas in h hours. Find minimum k that koko can eat finish its piles of bananas in h hours.
- Example : Suppose we have the pile [3,6,7,11] and h = 8
- Brute force approach, start at k = 1, and check if koko can finish eating all piles of bananas in h = 8, increment k if fail to do so 
- Intuition: use max number from pile , EX: 11, using this we know that each pile can be eaten in 1 hour, but k is not minimum
- Brute force + intuition : we try values from 1 to 11 for k , giving us time complexity of O(max(piles) * length(piles))
- Better solution, using modified version of binary search , resulting in O(len(piles) log (max piles))
- Calculate if bananas can be eaten in h hours by iterating through the piles and use math.ceil 
<img width="400" alt="SCR-20230522-tynu" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/f54a41e3-cac2-430f-9d0b-9cbf4769fe4e">

## 2. Minimum in sorted rotated array
- Suppose a sorted array would be : [1,2,3,4,5]
- With rotation n = 1, array = [5,1,2,3,4]
- With rotation n = 2, array = [4,5,1,2,3]
- in while loop , compare min of prev min with nums[mid]
- Use binary search with a tweak, if nums[mid] is > num[right], min is probably on the right, set low = mid + 1
- Else , high = mid -1
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/6ac969d3-22dc-4863-9a4d-fb09767d8621">
- O(logn) time

## Search in rotated sorted array *****
- Suppose we have rotated sorted array : [4,5,6,7,0,1,2], we want to find the index of target in rotated sorted array
- Solution : if mid doesnt match target, check if mid is in first sorted portion or second
- First portion : nums[mid] >= nums[left]
- Case 1a) if target is larger than nums[mid], target is at second portion
- Case 1b) if target is smaller than nums[left], target is at second portion
- Case 2) Else, target is in first portion
- Second portion
- Case 1a) if target is > nums[right], target is at first portion
- Case 1b) if target is < nums[mid], target is at first portion
- Else, target is in second portion
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/b6914422-d6e4-4d04-9ceb-8e1480d4e628">
- Runs in O(logn) time


# Linked List

## 1. Reversing Linked list
- Suppose we are given the head of the list
- Define prev and curr variable where prev points to null and curr points to head
- While curr is not null, record curr.next into temp variable
- then curr.next points to prev, prev would then be pointing at curr and we move the curr pointer to the next by assigning it to temp variable
- return prev at the end
- O(n) time

## 2. Merging two sorted linked list (Works like mergesort)
- Suppose we are given two sorted linked list and we want to merge them
- Define a list object (dummy = ListNode()), and assign a variable to the list object created (tail = dummy)
- Case 1 : while list1 and list2 is not empty, compare the values of first element of both list, set tail.next = smaller value of the two list, move pointer of the seleted list using list1 = list1.next and move pointer of tail = tail.next
- Case 2: if list1 not empty, append list1 to tail.next
- Case 3: else if list2 not empty, append list2 to tail.next
- return dummy.next
- O(len(list1) + len(list2))
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/df22dd68-1f3a-4551-8b15-76188d4d5623">


## 3. Reorder list *****
- Reorder the list such that the list would be of this order 
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/f5ee3d24-346e-455a-88d4-3cf872b222f0">
- Intuition: Break linked list in half, reverse second half of linked list, begin merging both lists by alternating between the 2 halfs
- Break problem into 2 portions : 1) find halfway point of the linkedlist 2) Begin merging process
- 1) use fast and slow pointer to determine half of the linked list
- 2) Reverse second half of list, same method as Q1 from linked list question above
- 3) Merge both list via altering ( Use 2 temp variables to record next of head and next of reversed second list)

<img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/258e7170-3ce2-4ac8-93cf-6e75676077e8">

## 4. Remove nth node from end of list
- Intuition: Reverse linked list , remove, and reverse it again ( this uses a lot of memory and time)
- Better solution: Use 2 pointers with n as spacing
- Start with head, make seccond pointer n spacing apart, shoft both pointers to right until right pointer is null
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/40dd53dd-fc39-4663-b11f-cb15f6cbdbfe">
- Problem, we can identify the nth node from end of list, but no way of removing it since we dont have pointer to previous node
- Modified solution, introduce dummy node, set left pointer as this
- Then , set right pointer to head, use while loop to travers linked list until spacing of n is achieved
- Use another while loop for right pointer, traverse linked list amd move both left and right pointers until right pointer is null
- Once right pointer is null (end of list), set left.next = left.next.next
- return dummy.next
 - <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/1b0d4089-ae22-4646-b7c3-56a4a6d08100">
 - O(n) time

## 5. Copying linked list with random poiters
- Supose we have a linked list , the only catch is that the nodes of the list has a random pointer to another node
- Copying linked list is easy, but assigning random pointers to a node not created would be a problem
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/bb693366-1a8a-4e2f-96e7-acd2150fcb8d">
- Solution: Two pass solution using hashmap
- Pass 1: Use hashmap to iterate through list, record key as original node and value as a copy
- Pass 2: Iterate from head, set next of hashMap[oldCurr].next = hashMap[oldCurr.next], hashMap[oldCurr].random = hashMap[oldCurr.random]
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/f6bdde81-33e9-4cc4-8507-4e196e224174">

## 6. Adding two numbers
- Suppose we have two linked list
- Normal sum example: 129 + 139 = 268
- Linked list is reversed for better representation of problem : L1 = 9->2->1 , L2 = 9->3->1 , target solution = 8->6->2
- Solution: traverse both lists, compute sum, if sum > 9: set carry = 1, for next sum add the carry
- Solution would be similar to merging both linked list 
- Case 1: Both L1 and L2 have elements
- Edge Case 1 : L1 longer than L2
- Edge Case 2 : L2 longer than L1
- Edge Case 3 : Last addition includes a carry over, so an additional node needs to be added to the end 
- O(len(l1) + len(l2)) time

## 7. Cycle in linked list
- Suppose we have a linked list, we want to know if linked list contains cycle or not
- Personal approach : Use hashmap, traverse the linkedlist, if node in hashmap , return true, else record key as node and value as index position, return false at the end
- This approach takes O(n) time
- Drawback: Space complexity is O(n)
- Better solution: Floyd's tortoise and hare solution
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/a4748e6b-2814-4347-a5ce-a4b7beddd42e">
- slow and fast pointer works something like finding the half of the linked list
- Using the image above, it is always true that the slow and fast pointer will meet if cycle exists
- Suppose distance between fast and slow is 10, when slow moves , d = 10 + 1 = 11, when fast moves, d = 10 + 1 - 2 = 9
- By extrapolating this result, d will decrease until d = 0
- Slow pointer and fast pointer starts at the beginning, move slow pointer by 1 node at a time, fast pointer 2 nodes at a time
- The slow and fast pointer will eventually meet if cycle exists
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/bc6cd73d-b9a8-4233-9192-f22ef8621e1f">



## 8. Duplicate number in linked list
- Given an array of numbers with length n + 1 where intergers in the array are bounded by the range [1,n] (n is inclusive)
- Find the duplicate number, using constant space solution ( hashset, map cannot be used)
- Solution: Look at elements in array as pointers 
- An array of [1,3,4,2,2] have linked list representation as 1->3->2->4->2 
- Note that node 1 will not be in the cycle as element 0 does not exist (if elelement 0 exists, pointer 0 would point to 1)
- Then perform Floyd's algorithm until slow and fast pointer meet
- Then assign another pointer at head, shift both new pointer and slow pointer until they meet, that would be the start of the cycle ( duplicated number)
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/00369251-a1e2-47e3-9b8a-3131e5a616c0">
- Since a cycle will always exist, while loop condition always True instead of using while fast or fast.next:

# Trees
## 1. Inverting Binary tree
- Given a tree where each parent has 2 children , invert the tree
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/78583f91-a56e-4551-a478-3d8c661ac56a">
- Intuition: Have a queue, visit the root, append root\/parent to queue, while queue still has element, pop from queue, swap the left and right element of the tree, append the left and right node of the tree and repeat
- Drawback: Solution uses queue , more memory
- Better solution : recursive solution via DFS
- If root is empty, return none, else swap left and right node, and call self.invert(root.left) and self.invert(root.right) and return root

## 2. Max depth of tree
- Given a tree, return the max depth of tree
- Recursive DFS solution, if root is None, return 0
- Else, self.maxDepth on root.left and root.right, compare and see which is bigger, then return 1 + max(depth(left) , depth(right))
- Iterative BFS solution, traverse level by level, increment depth by 1 each time
- Iterative DFS solution, using stacks

## 3. Diameter of a Binary tree
- Given a tree, find the longest diameter of the tree (max length of path from one node to other node)
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/438aeb72-8b2d-43df-9118-f0a8e2ea9fef">
- Tree above has diameter of tree
- Basics for tree : Height = starting from bottom , the node with the highest depth has height of 0 ; null nodes have height of -1
- Solution intuition : Have a max variable, traverse tree from leaf nodes, height of the node = 1 + max(height(left), height(right)), update max if needed
- Diameter = height(left) + height(right) + 2 , we need to add 2 as we the current node's height is one level above the left and right children 
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/6e217f84-6910-46ab-b2e8-c494b2449bb8">
- Tip: Use global list so that dfs function can access it globally
- O(n) time

## 4. Balanced binary tree
- Given a binary tree, return true if tree is height balanced
- Height balanced definition: Given a node, compare height of left and right subtrees, if height difference > 1, its not height balanced (Do this for every node)
- Solution intuition: Solution works similarly to diameter of binary tree, perform recursive dfs to get height of left and right, return false if diff > 1, return false if otherwise
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/68005da0-75d5-4e7a-8127-561a4ed670ae">
- There might be otherways to return false once a false is detected, either via throwing exception or check for boolean type
- O(n) time

## 5. Same tree
- Given the root of 2 binary tree, return true if both trees are the same
- Solution: If both roots are null, return True , else if both roots have same value and not null, perform checking for left subtree and right subtree for both roots, if both left and right returns true, they are the same
- Perform checking via recursive solution
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/678b3684-46aa-4cf9-a282-389317c8927d">
- O(n) time where n is number of nodes of the tree


## 6. isSubtree
- Given root of 2 binary tree, return true if second tree is a subtree of the first tree
- Solution: Case 1) Check if second root is null, if so, return true  
- Case 2) If first is null and second is not null, return false
- Case 3) if first and second root is not null, if they are the same tree (use same tee algorithm from above) , return true
- Case 4) Check if second tree is subtree of root.left or secodn tree is subtree of root.right
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/537c55be-5d97-4bb3-b930-ee3b2bf08b4c">

## 7. Lowest common ancestor of a binary search tree
- Binary search tree : Left nodes are smaller than parent node, right nodes larger
- Given the root of a tree and two nodes p and q, find the lowest common ancestor of p and q
- Facts : A node is an ancestor of itself
- Fact2: Root of the tree is ancestor for all nodes in the tree
- Solution intuition : Case 1) If both p and q have values larger than the curr ancestor , curr ancestor = curr.right
- Case 2 ) if both p and q smaller than current ancestor, curr ancestor = curr.left
- Case 3) if p is less than curr and q is more than curr, ancestor remains the same
- Case 3a) if p or q is the ancestor, return that as ancestor
- Case 3) and 3a) falls in the else case
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/54b86a8d-bf8d-4029-9467-a9df64b008c1">
- O(log n ) time, we dont traverse both sides of the tree, only visit one half of tree, level by level (Traverse height of tree)

## 8. Binary tree level order traversal
- Facts: Dequeue is a double ended queue, allows popping and insertion from front and back
- Given a binary tree, return a list for nodes in level order 
- Solution : Use BFS traversal, on each level create a tempList and append that list once the level is fully traversed
- Use a queue to insert nodes, pop from the left and add left and right children to the end of list
- Intuition : Once a queue is empty (current len(queue) = 0), the nodes in that level is fully traversed
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/ba030921-916e-407a-8613-c734b0e0ffb8">
- O(n) time

## 9. Binary tree right side view
- Solution similar to level order traversal
- Just return last element of temp list before appending to result list
- O(n) time

## 10. Count good nodes in binary tree
- Given the root of the binary tree, return the number of good nodes
- Good nodes : Starting from the root to node X, there are no nodes greater than X
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/9c6364db-df38-459d-837e-b22b6dee5896">
- Solution: Use Dfs traversal, at each level if node is larger than maxVal, increment count and set new max = currNode.val
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/93c912b5-b677-4842-965e-dcedf7e275cd">
- Runs in O(n) time

## 11. Validate binary search tree
- Fact: Every node on the right of node of BST is larger that root, every node on the left smaller than root
- Wrong intuition : Use BFS, at every level , check if node is less than parent if it's on the left and more than parent if it's on the right
- Explanation: would miss out edge cases ( where node 4 is less than 7, but should be more than 5) 
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/343353ab-94dd-421b-9801-8240485661ec">
- Solution: Use DFS, set left and right boundaries at each recursive traversal, check if node.val between left and right boundaries
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/1cd07cb3-9bf0-4461-b539-cccedd381c38">
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/6f60f8e5-2705-4ced-83bf-d4816edd48c6">
- TIP : Use float("-inf") for negative infinity and florat("inf") for infinity

## 12. Kth smallest element in BST
- Given a binary tree, return the kth smallest element
- Solution: Perform DFS with small tweaks
- Only after the visiting the root, perform DFS on root.left , then append the root to the array
- This way, the nodes in the tree will be sorted
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/0c19d875-fcfe-4f71-b60a-bc7a4c41323f">
- O(n) time

# Tries
Definition : Prefix tree used to store strings efficiently 

## 1. Implement Trie
- Goal : Implement insert, search and startswith operation
- Why use a Trie instead of hashMap for string storage? Ans: Trie allows efficient searching for strings.
- Concept, starting from the root node, if we were to insert a string "apple"
- We check if the children of root has the node with letter "a", if so, traverse down the children of "a" node , else create node wth "a"
- Blue nodes are marked as end nodes, used to tell if a word exists when using search operation
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/766df19b-4f30-475c-9c01-0ea31c0bc020">
- If we need to insert the word "ape", we can reuse nodes instead of creating entirely new ones
- If we use hashMap for startsWith, we may need to traverse the whole hashMap , giving O(n) time
- But using Trie, we can traverse the beginning nodes to check for matching starting letters in O(26) == O(1) time
- Solution : FIrst implement a Trie Node class that uses hashMap for tracking children and another property called end for marking end of the word
- Then, implement insert function : Traversing letter by letter of input and starting from the root, if letter is in children of root, call children of the root, else create a TrieNode as value with key as the letter 
- Search function, traverse from root, return False if letter no in children , else return TrieNode.end at the last letter
- Startswith function, return False if letter no in children , else continue traversal until the end and return True
- Search and startswith is very similar
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/7bc5861a-2593-4c38-90d8-ce7761efafe2">

## 2. Design add and search words data structure
- Similar to trie question, the only catch would be tweaked search algorithm
- In a given string, "." would represent any string
- In a trie, if "apple" exists, "..ple" would be a viable string and should return true
- Solution for search, if a . is met, traverse all of it's children recursively to check if the string that matches the remaining portion after "." exists.
- Code for adding == insert , base code essestially the same as Q1
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/e564cbcc-be5d-4624-b6c2-38c657445d70">

# Heaps and priority queues

## 1. Kth largest element in a stream
- Build a class that returns the kth largest element of the input
- The add operation would add element into the stream while returning the kth element into the stream
- Example interaction : 
- KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
- kthLargest.add(3);   // return 4
- kthLargest.add(5);   // return 5
- Slow solution : Sort the array in O(nlogn) time, return list[len(list) - k]
- Better solution : Use min heap implementation
- Build a heap of size k, add element and pop element while maintaining heap size of k, return heap[0] for kth largest element
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/44a21609-69b6-4c2e-8ed4-06f4f9600d02">
- Note : Overall time complexity is O(n) due to heapify (build heap operation), popping from heap takes O(log n) with heapify

## 2. Last stone weight
- Given an array of stones with weight[i], for each turn smash two stones with the largest weights 
- When smashed, resulting stone would have weight of X - Y
- Solution : Use Max heap implementation
- At each iteration ( while MaxHeap has more than 1 stone), smash two of the largest stones, get the reamining stone of weight x - y and add it back to the max heap
- TIP: Use heapq.heapify method, but convert all weights in array to negative value (Since max heap implementation for heapq doesnt exists)
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/22c46e0b-603a-415e-b481-d3cfac4ecb89">
- Runs in O(n) time

## 3. K closest Points to origin
- Given an array of coordinates, return the k closest points to origin
- Solution : Use minheap to sort out the calculated distance for the points, and return k number of points
- TIP : heapq.heapify works with 2d lists as well , EX: [[3,4,2],[2,4,3]] -> [[2,4,3],[3,4,2]]
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/7e648a0a-7796-4251-b10c-89998c208dde">
- Runs in O(n) time

## 4. Kth largest element in an array
- Given an array of integers, return the kth largest number
- Note : Kth largest element does not mean the kth distinct solution
- Solution : Use min heap implementation, only thing would be making sure no repeated numbers are in the minHeap (use a set instead)
- <img width="518" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/fc958d89-6a40-4314-a230-93aaaec5f715">
- Runs in O(n) time, with O(n) space complexity

## 5. Task scheduler
- Given an array of characters where each character represent a task, an a nonnegative integer n that represents the minimum unit of wait time between the same tasks
- Goal : Find the minimum unit of time needed to schedule all the tasks
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/f0f5c880-8057-4994-905f-d5bfb50fa46b">
- Explanation : After task A is completed , a minimum cycle of 2 units will need to be met in order for next task A to be performed again
- Solution : Use a maxHeap implementaiton and queue, first count the occurence of each tasks, start with tasks with most occurence
- Then, decrement remaining task , increment time , and append task with their next available time to a queue
- If tasks in queue is ready, append it back to maxHeap
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/f99bca20-ee51-44ed-994e-ede41585f0d1">
- Runs in O(n) time

# Backtracking

TIP : something to do with incrementing at each level, no repeating inputs in results
Patterns : Uses dfs recursion, either increment i or not in recursion dfs(), End at i == len(of array) 

## 1. Subsets
- Given an array of numbers, generate all possible subsets
- Solution : Use DFS and popping of stack
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/57dd016f-9af6-4890-b220-0f9f5b933c79">
- At each level either add nums[i] and continue dfs, or remove nums[i] and continue dfs
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/05495dcb-f69d-4a5d-97e3-ecc5eb90aae7">
- Runs in O(2^n) time, all possible combinations of elements in array

## 2. Combination sum
- Given an array of numbers, generate all combinations of numbers that sum to target
- Solution : Use backtracking, at each level either add current number , or dont add other number
- Example : [2,3,6,7], target = 7
- <img width="700" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/855f1ecd-8449-4ea1-8fc1-df97750e1320">
- At each level , append to result if sum == tartget, check if sum > target or i == len( input), if so, return, else continue dfs backtracking
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/ce09b67f-11e4-408a-87e1-f94faa1d958c">

## 3. Permutations
- Given an array of distinct numbers, generate all possible permutations of the numbers
- Solution : Use backtracking, at each level add number that has not been used before
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/3f33703d-8248-40c2-8c59-cf92fe8ad7ee">
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/7e8cda0b-f7ec-43af-bbbd-6f45079b9382">
- More optimized solution with less memory, break down to smallest unit of permutation, then add it to the back of a larger unit of permutation
- Example for nums:[2,3]
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/ce4d3b82-8887-472b-b178-300a926dd9ef">
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/f4b70847-e1f7-4405-91cf-b783b6de907b">

## 4. Subsets 2
- Given an array of integers, some of which may be duplicated, return all possible subsets without duplications
- Same logic as before , the only catch would be to prevent duplications in subset generation
- Issue with subset 1 implementation
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/a6751ef6-17d2-4874-87c1-d7ef58dcd2de">
- Solution: To prevent duplicates, after popping, check if i+1 is the same as i, if so, increment i until diff number is found
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/21e13e3c-3762-4208-8083-7c993192ce83">
- Resulting solution would look like this for [1,2,2,3]
- <img width="500" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/872c9e82-a29e-487c-9fe0-156d3707eae5">

## 5. Combination Sum 2
- Given an array of integers where some integers may be duplicated, generate a list of lists summing up to the target
- NOTE: Each element in the input array can only be used once
- Duplicated solutions may arise
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/dcd53c04-f5e8-413c-811e-962da71b7176">
- Solution: Similar to combination sum 1, but each element can only be used once , so dfs(i, ....) is not possible, only used dfs(i+1)
- To prevent duplicated solutions, perform while loop checking after popping, similar to the solution for subsets 2
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/3e498718-417b-4ff3-85e7-3bc3b35b055a">
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/a20dce01-e2a9-49dc-92bd-e712a528f841">
- Sorting takes O(nlogn) , but overtaken by backtracking operation that takes O(2^n) timed\

## 6. Wordsearch
- Given a board ( 2d array of alphabets), return true if word exists in the grid, else false
- We can traverse the board either vertically of horizontally
- Solution: Brute force / backtracking approach, visit and generate path that leads to the word
- Construct a recursive dfs function that generate a path leading to our word
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/650ccf9b-f476-4a88-907c-9bbc12563161">

## 7. Palindrome partirioning
- Given a string, generate all possible palindrome partitioning
- <img width="300" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/86bfdffb-109e-48cc-8692-a9bf21b36f06">
- Solution: Use backtracking coupled with a palindrome checking function
- Graph visualization
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/be60ccfe-0b24-4c44-b2f6-a3c5a708956d">
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/0de7356a-cc12-456f-afd8-9bf6ce6d055f">

# Graphs

## 1. Number of islands
- Given a 2d matrix, find the number of islands, "1" represent land, and "0" is water
- Goal: Find no of patches of "1"
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/31fc9e98-5707-42c8-a0e9-8881e47b167d">
- Solution traverse each cell in 2d matrix, if cell is "1" and have not been visited yet, increment count by 1 , and perform bfs in all 4 directions of that cell
- <img width="800" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/ad0b422a-218a-4190-b3dd-c7db2c1dd7d7">

## 2. Clone Graph
- Given an undirected graph, return a deep copy of the graph
- Solution: Traverse from the given node, if the given node is in hashMap, ignore, else assign a copy of the given node to hashmap
- Then, traverse its neighbors, if the neighbor is in hashMap, append to currentNode's neighbors, else, perform dfs and append it to currentNode's neighbors
- Solution visualized
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/237af2ab-1ec3-4c62-8558-f175b008b649">
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/1c43ce87-3b28-4b18-a4db-7e2f1788e16c">
- Runs in O(n) time

## 3. Max area of island
- Given a 2d matrix, find the max area of islands, "1" represent land, and "0" is water
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/0c125b38-abac-42c1-abaf-e5358c0eb1fb">
- Solution : Similar to finding no of islands, except we need to keep track of the max area
- BFS solution shown below:
- <img width="800" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/c76aa822-ffda-42d0-a2be-3c54f3876cb2">
- DFS solution uses less memory
- <img width="800" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/5055faa2-f906-45b0-ae62-8bc324d78056">


## 4. Atlantic water flow
- Given a 2d matrix, find the spots on the island that allows rainwater to fall to both the pacific and atlantic ocean
- Brute force solution: Traverse each location, for each location traverse in four directions to check , takes O((M*N)^2) time
- Better solution : Instead of looking at rain water at specific location, look from different perspective
- Look if pacific / Atlantic water can "climb" that location if prevHeight is < next height, pacific water can "climb" to that location
- Uses Dfs approach , runs in O(M*N) time
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/9903b661-eedb-470a-9b85-2f87267fdf66">
- Bfs solution works too, but is slower, consumes more memory
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/1bed19b1-39eb-4016-99b7-f2ebe8e930b5">

## 5. Surrounded regions
- Given a m * n matrix, convert surrounded cells into X
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/87ab8f7f-01ac-4267-9e37-eeede0371795">
- Wrong intuition: traverse each cell in matrix, if cell is 'O', check up down left right direction to see if there are any 'X'
- Explanation, having 'X' in all four direction doesn't mean 'O' cell is surrounded by 'X'
- Solution: Instead of capturing cells that are surrounded, find cells that are unsurrounded , mark them as different letter, and convert all remaining 'O' cells into 'X
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/04c0f41c-9863-47aa-b8e6-b6923d2270cb">
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/51ae4ee5-ebee-4133-9acc-52697fb6b8c9">
- Runs in O(M * N) time

## 6. Rotting oranges
- Given a m * n matrix, find the minimum amount of time such that all oranges in the grid are rotten
- <img width="700" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/57562446-5afa-4a93-8744-fa5033daf1e3">
- Solution : First find oranges that are rotten, perform bfs for each rotten orange simultaneously and add unrotten oranges into queue
- Have a visited set to keep track of oranges that are visited
- If there are unrotten oranges detected via bfs in 4 directions, convert them to rotten, add them to queue
- After one cycle of bfs done, check if there are unrotten oranges in the queue, if so , increment time
- <img width="800" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/06cad9f6-9785-41b4-b472-9241990c6cbb">
- Runs in O(M * N) time

## 7. Walls and Gates
- Given a m * n matrix, Conmpute minimum distance from gates to rooms
- <img width="500" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/1ff98395-0e2c-45eb-8f6b-42047b892f68">
- Soution : Similar to rotating oranges, first find all gates and append to queue, then perform bfs on all gates to rooms, computing the distances to all rooms
- Use visited set to keep track of visited cells
- <img width="850" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/78d9451b-b120-4a8c-9d57-269ab69ec618">
- Runs in O(M * N) time

## 8. Course Schedule
- Given a 2D array, return True if the course schedule is satisfiable
- <img width="300" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/c48e678e-1386-451a-8b29-0f0b6ea5d257">
- <img width="300" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/10fdbf5a-dec0-4be3-9b1d-7e07cc7fa916">
- Suppose we have this example courses = [[0,1], [0,2], [1,3], [1,4], [3,4]]
- Solution: Build a hashmap for each courses with their prerequisites (linked list representation), use dfs to traverse each course, return False if there are cycles detected, else return True
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/c41cf287-ef1b-42cd-8fe0-21b3172fa91c">
- TIP : Use visited set to keep track of current node, used for detecting cycles
- If node[course] = [], return True as the course doesnt have any prerequisite
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/b27252e3-3dda-4731-b0cf-4484c7c96b20">

## 9. Course Schedule 2
- Similar to course schedule 1, but we return the order of courses if it is satisfiable, else we return []
- Solution : Perform dfs on each node, use additional set to keep track of courses added to results
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/89363646-b989-4f4b-839d-feb73558d7ac">
- Runs in O(E + V) time

## 10. Redundant Connection
- Given a 2d array of edges, remove an edge such that cycle in a graph no longer exists.
- <img width="450" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/bd45df22-b2a5-4456-9d98-13c6384792ed">
- Solution : Union Find
- For each node n, we associate a rank (no of nodes in graph containing node n) and a parent array, a node's parent is itself initially
- As we traverse through the edges, we check if we can Union/join the two nodes, if the two nodes have the same parent, return false, else, check whose rank is higher and add the node to the graph with higher rank
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/bc276ecd-0cf0-43bf-b1db-ef9b6b762f11">
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/b2c4432e-6278-4738-af17-a385ca46085c">


# 1D dynamic programming
Solving subproblems
  
## 1. Climbing Stairs
- Given n number of stairs , we can take either 1 or 2 step at a time, return the number of possible ways to climb to the top of the stairs
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/b078a854-a33c-41f8-a15e-360d3530e0b1">
- Brute force solution : Use dfs , count no of possible solutions
- Suppose we have n = 5,
- <img width="900" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/2b9ca534-b2d5-490e-893e-d320ea54d30e">
- More efficient solution : Since the subproblems have been solved, we can use some form of cache to store solutions to our subproblems (Memoization), resulting in O(n) solution
- <img width="900" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/75522cd5-e7e2-4ac2-8d5b-005bedbbd673">
- Alternative solution, use bottom-up approach, produce solutions starting from n = 5
- <img width="700" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/a02abf1a-40bd-44a3-a078-2ae17b2f2c97">
- <img width="300" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/1b40d703-9c77-4067-a17c-25fc033049aa">
- Runs in O(n) time

## 2. Min Cost Climbing Stairs
- Given an array of costs where cost[i] indicates the cost to climb stair at level i, return min cost to climb to top of stairs
- Users can start climbing from index 0 or 1, and they can take 1 or 2 steps per time
- Solution : Dynamic programming solution involving the use of min comparison
- <img width="450" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/009314fc-929a-4a8c-86b0-f1ed1679366a">
- Runs in O(n) time

## 3. House Robber
- Given an array of numbers, return max robbed amount given that no two adjacent houses can be robbed
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/1047e9aa-1eea-48c2-b7f3-b7c670cada84">
- Solution : keep track of currMax and max before prev element
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/6037be3d-0b48-4afa-aa54-b3be54407902">
- <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/41fbb697-1fde-4a85-a994-48dd3035669f">
- Runs in O(n) time

## 4. House Robber 2
- Similar to house robber 1, except the array is circular (first element is adjacent to the last)
- Solution: Perform house robber algorithm from 1st to last -1 and from 2nd to last element , then compare and return the larger element
- <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/fa31c22d-9f22-4cf7-af40-56710c3a76ac">
- Runs in O(n) time

## 5. Longest Palindromic substring
- Given a string, return the longest palindromic substring
- Bruteforce solution, for each character i, traverse the string from character i and build longest palindromic substring
- Run time : For each character O(n) * traverse the string from character O(n) * check if it's palindrome O(n) = O(n^3)
- Better solution, for each character, expands outwards in left and right direction, if char[left] == char[right], record as a palindrome
- <img width="500" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/213b39ec-4667-47bd-bae3-c33f5124f67d">
- Runs in O(n^2) time

## 6. Palindromic substrings
- Given a string, return the count of palindromic substrings that can be formed
- Brute force solution: Create an isPalindrome helper, iterate through every letter in every possible combination O(n^3)
- Solution : Use tweaked solution from the longest palindrome substring, increment count when a palindrome condition is satisfied
- <img width="500" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/f719fc02-2e2b-4c2b-8849-369f0f6c32d8">
- Runs in O(n^2) time

 ## 7. Decode ways
 - Given a string, return the number of possible ways to decode the string
 - Let A -> 1, B -> 2 ..... Z -> 26
 - <img width="400" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/90113c8c-de7a-469b-b512-16464c0da109">
 - Solution : For each letter[i], compute ways to encode letters starting from letters[i+1], if letters[i] and letters[i+1] can be encoded, add ways to compute letters[i+2] as well
 - Use cache for dp to reduce time complexity (memoization)
 - <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/5d0a9a86-c5da-4a52-935a-5ff14a40deab">
 - <img width="600" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/4bf995b6-2f79-46c3-a19d-006e0a9aff92">
 - Runs in O(n) time

## 8. Coin Change
- Given an array of coins, return the least no of coins needed to reach the targeted sum (amount)
- Brute force solution, try out each possible combination until sum is reached
- <img width="500" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/7467876a-93d4-4d66-a2ce-c6132d12c902">
- Better solution : Use bottom up approach + caching , at dp level i, store the min number of coins needed to sum to i
- <img width="700" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/3f34c354-f0bd-472f-b6d8-dd1a34d2d7c7">
- <img width="500" alt="image" src="https://github.com/AndyFooGuoZhen/Leetcode-daily-practice/assets/77149531/71e747c3-a3b4-494e-bbc4-8e4e2bba5f49">
- Runs in O( amount * len(input))















 



























