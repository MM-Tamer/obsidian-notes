
## 1. 📝 Problem Info
- **Title:** Contains Duplicate  
- **Link:**  [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
- **Difficulty:** <u style="color:green">Easy</u> / Medium / Hard  
- **Date Solved:**  Apr 17, 2025 20:26

---

## 2. 📖 Problem Summary
_Given an integer array, return `true` if any duplicates exist otherwise return `false` (all elements are unique)._

---

## 3. 📦 Input & Output
- **Input:** `int[] nums`  
- **Output:**  `boolean`
- **Constraints:**  -
	- `1 <= nums.length <= 105`
	- `-109 <= nums[i] <= 109`

****---

## 4. 💡 Initial Thoughts / Plan
_Write your thought process before coding._

- Edge cases to consider:  
	- empty array
- Potential approaches (e.g., brute force, two pointers, DFS):  
	- brute force
	- use hash set
- Key data structures / algorithms:
	- array
	- hash set

---

## 5. 🔧 Solution(s) Tried

### Approach #1
- **Strategy:**  brute force
- **Time Complexity:**  O(n^2)
- **Space Complexity:**  O(1)
- **Outcome:** ❌ Time Limit Exceeded.  
- **Notes (bugs, wrong assumptions, etc.):**

---

### Approach #2 *(if any)*  
- **Strategy:**  hash set
- **Time Complexity:** O(1) 
- **Space Complexity:**  O(n)
- **Outcome:** ✅  
- **Notes:**

---

## 6. ✅ Final Accepted Solution

```java
class Solution {

    public boolean containsDuplicate(int[] nums) {

         HashSet<Integer> hashSet = new HashSet<>();

         for(int i : nums){

            if(hashSet.contains(i))

                return true;

            else

                hashSet.add(i);

         }

         return false;

    }

}
```

- **Time Complexity:**  O(1)
- **Space Complexity:**  O(n)
- **Why this works:**  You can detect the existence of a duplicate due to hash collisions

---

## 7. 📌 Lessons Learned

- New techniques or patterns:  
- Mistakes made:  
- Concepts to revisit:  

---

## 8. 🔁 Next Steps / Similar Problems

- **Review this later?** Yes / No  
- **Similar problems:**  
  - [ ]  
  - [ ]  
