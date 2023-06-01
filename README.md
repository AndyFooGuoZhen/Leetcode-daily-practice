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

## 5. Top k frequent elements
- Use bucket sort, index represent count of the element
- create a hashmap, and a list containing len(nums) + 1 empty lists ( list index at 3 means count of element = 3)
- iterate through number array and keep update count of elements in hashmap
- iterate through hashmap and append elements according to count into the empty lists
- iterate list from reverse and append elements from sublist into result list until length of k is reached
- O(n) time


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

## 3. Three Sum
- Start by sorting the num list O(nlogn)
- iterate through the list, for each iteration check if current is same as previous, if its the same , use continue to go to next number in list,
- declare left and right pointer, left pointing at current index + 1, right pointing at last number
- perform two sum , check if current + left + right is = 0
- if < 0, move left ptr to right, else if > 0, move right ptr to left, else = 0 move letf ptr to right, append to result and check while left < right and if nums[left] == nums[left + 1], move left ptr to right again
- O(n^2) time

# Sliding windows

## 1. Best time to buy stock
- Define a min and profit variable
- Iterate through the list, is the current is less than min, set that as new min
- Then calculate current - min and compare it to previous assigned profit, if new profit is larger, reassign profit
- O(n) time

## 2. Longest substring without repeating characters
- Define a set and left ptr
- Traverse the string by each character, if character not in set, calculate length by taking right ptr - left ptr + 1
- if character in set, remove start removing characters from left prt until character no longer in set
- O(n) time

## 3. Longest repeating character with replacement
- Define a countHashmap, left ptr and length
- Traverse the string by each character, for each character, increment its count using hashmap
- then in a while loop, check if current window size - max count of a charcater in hashmap > k
- if so, decrement count of character at left ptr in hashmap and move leftptr to the right
- calculate length of window and compare it to previous recorded max window length
- O(n) time

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
- O(logn) time

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

## 3. Reorder list
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


## 8. Duplicate number in linked list
- Given an array of numbers with length n + 1 where intergers in the array are bounded by the range [1,n] (n is inclusive)
- Find the duplicate number, using constant space solution ( hashset, map cannot be used)
- Solution: Look at elements in array as pointers 
- An array of [1,3,4,2,2] have linked list representation as 1->3->2->4->2 
- Note that node 1 will not be in the cycle as element 0 does not exist (if elelement 0 exists, pointer 0 would point to 1)
- Then perform Floyd's algorithm until slow and fast pointer meet
- Then assign another pointer at head, shift both new pointer and slow pointer until they meet, that would be the start of the cycle ( duplicated number)
- 


