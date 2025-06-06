Notes

## 1. 📝 Problem Info
- **Title:** Two Sum  
- **Link:**  [Two Sum](https://leetcode.com/problems/two-sum/description/)
- **Difficulty:** <u style="color:green">Easy</u> / Medium / Hard  
- **Date Solved:**  Apr 18, 2025 

---

## 2. 📖 Problem Summary
_Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

_You can assume there exists only one solution. It is not allowed to use the same element twice, however, duplicates may exist._
_Order is insignificant._

---

## 3. 📦 Input & Output
- **Input:**  `int[] nums, int target`
- **Output:**  `int[] indices`
- **Constraints:**  
	- - `2 <= nums.length <= 104`
	- `-109 <= nums[i] <= 109`
	- `-109 <= target <= 109`
	- **Only one valid answer exists.**

---

## 4. 💡 Initial Thoughts / Plan
_Write your thought process before coding._

- Edge cases to consider:  
	- Array with single element, empty array.
- Potential approaches (e.g., brute force, two pointers, DFS):  
	- brute force with nested loops 
	- 
- Key data structures / algorithms:  
	- hash maps

---

## 5. 🔧 Solution(s) Tried

### Approach #1
- **Strategy:**  brute force with nested loops
- **Time Complexity:**  O(n^2)
- **Space Complexity:**  O(1)
- **Outcome:** ❌  
- **Notes (bugs, wrong assumptions, etc.):**

---

### Approach #2 *(if any)*  
- **Strategy:**  You have the equation _target = element1 + element2_ , the _target_ is known and you can have an active reference to either one of the elements through a loop iteration. You end having one unknown, let it be _element2_, then you would have the equation _element2 = target - element1_. The index of _element1_ is known since it is the value you're searching for by looping through the array but you will need to retain information about _element2_ 's index , since you will store in a hash-based collection, so a hash map is needed where the key is the integer value and the value is the index.
- **Time Complexity:**  O(n)
- **Space Complexity:**  O(n)
- **Outcome:** ✅ 
- **Notes:**

---

## 6. ✅ Final Accepted Solution

```java
# Your working code here

class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap();
        for(int i = 0; i < nums.length; i++){
            int complement = target - nums[i];
            if(map.containsKey(complement))
                return new int[] {i, map.get(complement)};
            map.put(nums[i], i);
        }
        return null;
    }
}

```

- **Time Complexity:**  O(n)
- **Space Complexity:**  O(n)
- **Why this works:**  

---

## 7. 📌 Lessons Learned

- New techniques or patterns:  play around with the equations you're given and determine what's known and unknown.
- Mistakes made:  
- Concepts to revisit:  

---

## 8. 🔁 Next Steps / Similar Problems

- **Review this later?** Yes / No  
- **Similar problems:**  
  - [ ]  
  - [ ]  
