Notes

## 1. 📝 Problem Info
- **Title:** Group Anagram  
- **Link:**  [Group Anagram](https://leetcode.com/problems/contains-duplicate/)
- **Difficulty:**  Easy / <u style="color:yellow">Medium</u> / Hard  
- **Date Solved:**  May 7, 2025 

---

## 2. 📖 Problem Summary
_Given an array of strings group anagrams together_

---

## 3. 📦 Input & Output
- **Input:**  `String[] strs`
- **Output:**  `List<List<String>>`
- **Constraints:**  
	- - `1 <= strs.length <= 104`
	- `0 <= strs[i].length <= 100`
	- `strs[i]` consists of lowercase English letters.

---

## 4. 💡 Initial Thoughts / Plan
_Write your thought process before coding._

- Edge cases to consider:  
	- Empty Array
- Potential approaches (e.g., brute force, two pointers, DFS):  
- Key data structures / algorithms:  
	- hash map
	- 

---

## 5. 🔧 Solution(s) Tried

### Approach #1
- **Strategy:**  Create a list of hash maps which stores the frequency of each character for each string and iterate over the array of strings to populate the list. Then loop over the string list with a nested loop and match 
- **Time Complexity:**  O( N^2 )
- **Space Complexity:**  O( N )
- **Outcome:** ✅ / ❌  
- **Notes (bugs, wrong assumptions, etc.):**
	- duplicate strings that have in the output

---

### Approach #2 *(if any)*  
- **Strategy:** create a hash map with the character frequency hash map as the key and the list of strings associated with the frequency map as value. loop over the string array, if the key is not found add the key and initialize a list and add the string to it.
- **Time Complexity:**  O( k * n )
- **Space Complexity:**  O()
- **Outcome:** ✅ / ❌  
- **Notes:**

---

### Approach #3 *(if any)*  
- **Strategy:** same as approach #2 with one exception the map's key is a frequency string rather than hash map since comparing strings would be much more efficient than comparing complex objects such as hash maps. since the accepted characters are lowercase english letters  
- **Time Complexity:**  O( k * n )
- **Space Complexity:**  O()
- **Outcome:** ✅ / ❌  
- **Notes:**

---

## 6. ✅ Final Accepted Solution

```java
class Solution {

    public List<List<String>> groupAnagrams(String[] strs) {

        List<List<String>> anagramList = new ArrayList<>();

        if(strs.length == 1){
            anagramList.add(Arrays.asList(strs));
            return anagramList;
        }

        List<Map<Character, Integer>> mapList = new ArrayList<>();

        Map<Map<Character, Integer>, List<String>> map = new HashMap<>();
        for(String str : strs){

            Map<Character, Integer> charMap = createMap(str);

            if(map.get(charMap) == null){
                map.put(charMap, new ArrayList<String>());
            }
            map.get(charMap).add(str);
        }
        System.out.println(map.values());

/*         for(String str : strs){

            mapList.add(createMap(str));

        }

  

        Set<Integer> alreadyMatched = new HashSet<>();

        for(int i = 0 ; i < mapList.size(); i++){

            if(alreadyMatched.contains(i))

                continue;

            List<String> subAnagramList = new ArrayList<>();

            subAnagramList.add(strs[i]);

            anagramList.add(subAnagramList);

            alreadyMatched.add(i);

            for(int j = i + 1 ; j < mapList.size() ; j++){

                if(mapList.get(i).equals(mapList.get(j)))

                {

                    subAnagramList.add(strs[j]);

                    alreadyMatched.add(j);

                }

            }

        } */

        return new ArrayList<>(map.values());

    }

    public HashMap<Character, Integer> createMap(String str){

            HashMap<Character, Integer> resultMap = new HashMap<Character, Integer>();

            for(char c : str.toCharArray())

            {

                resultMap.put(c, resultMap.getOrDefault(c, 0) + 1);

            }

  

        return resultMap;

        }

}
```

- **Time Complexity:**  O( n * k ) n: number of strings, k: average string length
- **Space Complexity:**  O( n )
- **Why this works:**  

---

## 7. 📌 Lessons Learned

- New techniques or patterns:  
	- frequency strings
	- hash-based collections can contain non primitive data types.
- Mistakes made:  
	- created a hash map with the wrong type and ended up needing an auxiliary data structure (hash set) which used extra space and resulted in quadratic time complexity.
- Concepts to revisit:  

---

## 8. 🔁 Next Steps / Similar Problems

- **Review this later?** Yes / No  
- **Similar problems:**  
  - [ ]  
  - [ ]  
************