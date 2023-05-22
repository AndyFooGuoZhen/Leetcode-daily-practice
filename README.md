# Leetcode-daily-practice
Used for uploading notes for leetcode questions

# Arrays 

## 1. Contains duplicate
- Use set to keep track of duplicates
- if element is not inside, add it to set
- return true if element is inside of set

## 2. Valid anagram (check if 2 strings have characters of the same count)
- Use 2 hashmaps for keeping track counts of each element from 2 strings
- return true if both hashmaps are the same, else return false

## 3. Two sum ( check if two elements in the list add up to target)
- Use hashmap for keeping track of elements
- if target - current element is in hashmap, return index of diff and index of current element
- else add element into hashmap, with index of the element as the value

## 4. Group anagrams ( group strings with the same anagrams)
- Create a hashmap, where the value is a list type , use collections.defaultdict(list) for this
- Iterate through each string in list, while iterating use count = [0] * 26 to create a list holding 26 elements of 0
- for each string, iterate through each character and use ord() to get ascii value of character, essentially we are coutning the number of a specific character for each string
- convert the list into tuple form at the end, and add it to hashmap via append ( hashMap[tuple(count)].append(current string) ) 

## 5. Top k frequent elements
- Use bucket sort, index represent count of the element
- create a hashmap, and a list containing len(nums) + 1 empty lists ( list index at 3 means count of element = 3)
- iterate through number array and keep update count of elements in hashmap
- iterate through hashmap and append elements according to count into the empty lists
- iterate list from reverse and append elements from sublist into result list until length of k is reached


# Two pointers

## 1. Valid palindrome
- declare 2 pointers, one on first letter the other on last
- while left <= right, check if both letters match, else return false

## 2. Two sum (Sorted)
- declare 2 pointers, one on first num, the other on last number
- compute sum, if sum is smaller, move left pointer to right, else move right pointer to left
- if i > j, return false, else return [i,j]

## 3. Three Sum
- Start by sorting the num list O(nlogn)
- iterate through the list, for each iteration check if current is same as previous, if its the same , use continue to go to next number in list,
- declare left and right pointer, left pointing at current index + 1, right pointing at last number
- perform two sum , check if current + left + right is = 0
- if < 0, move left ptr to right, else if > 0, move right ptr to left, else = 0 move letf ptr to right, append to result and check while left < right and if nums[left] == nums[left + 1], move left ptr to right again

# Sliding windows

## 1. Best time to buy stock
- Define a min and profit variable
- Iterate through the list, is the current is less than min, set that as new min
- Then calculate current - min and compare it to previous assigned profit, if new profit is larger, reassign profit

## 2. Longest substring without repeating characters
- Define a set and left ptr
- Traverse the string by each character, if character not in set, calculate length by taking right ptr - left ptr + 1
- if character in set, remove start removing characters from left prt until character no longer in set

## 3. Longest repeating character with replacemebt
- Define a countHashmap, left ptr and length
- Traverse the string by each character, for each character, increment its count using hashmap
- then in a while loop, check if current window size - max count of a charcater in hashmap > k
- if so, decrement count of character at left ptr in hashmap and move leftptr to the right
- calculate length of window and compare it to previous recorded max window length
