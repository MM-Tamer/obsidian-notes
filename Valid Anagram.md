

## 1.📝 Problem Info
- **Title:** Valid Anagram  
- **Link:**  [Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)
- **Difficulty:** <u style="color:green">Easy</u> / Medium / Hard  
- **Date Solved:**  Apr 18, 2025 

---

## 2. 📖 Problem Summary
_Given two strings return `true` if the two are anagrams (meaning that they both contain the same combination of letters)._

---

## 3. 📦 Input & Output
- **Input:**  `String s, String t `
- **Output:**  `boolean`
- **Constraints:**
	- `1 <= s.length, t.length <= 5 * 104`
	- `s` and `t` consist of lowercase English letters.

---

## 4. 💡 Initial Thoughts / Plan
_Write your thought process before coding._

- Edge cases to consider:  
	- strings are of different lengths
	- one or more empty strings
	- 
- Potential approaches (e.g., brute force, two pointers, DFS):  
- Key data structures / algorithms:  
	- sorting
	- hash maps

---

## 5. 🔧 Solution(s) Tried

### Approach #1
- **Strategy:**  sorting the strings and then comparing
- **Time Complexity:**  O(nlogn)
- **Space Complexity:**  O(n)
- **Outcome:** ✅ / ❌  
- **Notes (bugs, wrong assumptions, etc.):**

---

### Approach #2 *(if any)*  
- **Strategy:**  using a frequency map or a hash map
- **Time Complexity:**  O(n)
- **Space Complexity:**  O(n)
- **Outcome:** ✅ / ❌  
- **Notes:**

---

## 6. ✅ Final Accepted Solution

```java
class Solution {

    public boolean isAnagram(String s, String t) {

        if(s.length() != t.length())

            return false;

        HashMap<Character, Integer> hashMap = new HashMap<Character, Integer>();

        HashMap<Character, Integer> hashMap2 = new HashMap<Character, Integer>();

        for(int i = 0; i < s.length(); i++){

            hashMap.put( s.charAt(i), hashMap.getOrDefault(s.charAt(i) , 0) + 1);

            hashMap2.put(t.charAt(i), hashMap2.getOrDefault(t.charAt(i) , 0) + 1);

        }

        System.out.println(hashMap2);

        return hashMap.equals(hashMap2);

    }

}
```

- **Time Complexity:**  O(n)
- **Space Complexity:**  O(n)
- **Why this works:**  it creates two hashmaps containing each string character as a key and the number of occurrences as values  and compares the two hash maps, if they're equal, then they must be anagrams

---

## 7. 📌 Lessons Learned

- New techniques or patterns:  hashing is an efficient strategy to compare objects in constant time.
- Mistakes made:   
- Concepts to revisit:  

---

## 8. 🔁 Next Steps / Similar Problems

- **Review this later?** Yes / No  
- **Similar problems:**  
  - [ ]  
  - [ ]  
