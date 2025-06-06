Notes

## 1. 📝 Problem Info
- **Title:** Top K Frequent Elements  
- **Link:**  [Top K Frequent Elements ](https://leetcode.com/problems/top-k-frequent-elements/description/)
- **Difficulty:** Easy / <u style="color:yellow">Medium</u> / Hard  
- **Date Solved:**  May 26, 2025 

---

## 2. 📖 Problem Summary
_Given an integer array nums and an integer k, return the k most frequent elements. Order is insignificant._

---

## 3. 📦 Input & Output
- **Input:**  `int[] nums, int k`
- **Output:**  `int[k] result`
- **Constraints:**  
	- - `1 <= nums.length <= 105`
	- `-104 <= nums[i] <= 104`
	- `k` is in the range `[1, the number of unique elements in the array]`.
	- It is **guaranteed** that the answer is **unique**.

---

## 4. 💡 Initial Thoughts / Plan
_Write your thought process before coding._

- Edge cases to consider:  
	- array containing single element.
- Potential approaches (e.g., brute force, two pointers, DFS):  
	- 
- Key data structures / algorithms:  
	- hash map
	- min heap
	
---

## 5. 🔧 Solution(s) Tried

### Approach #1
- **Strategy:**  Build a Hash Map of the array where the key is the integer value found in the array and the value is the number of occurrences of the key within the _nums_ array. Then build a min heap of map entries and assign the comparator of the min heap which compares the the frequencies of the map entries and sorts in ascending order  _(since we're building a min-heap)_  
- **Time Complexity:**  O(n + d * logk )
- **Space Complexity:**  O(d), where d is the number of distinct elements in the array
- **Outcome:** ✅ / ❌  
- **Notes (bugs, wrong assumptions, etc.):** 
	- the return type is an array of primitive int and I was using a an arraylist

---

### Approach #2 *(if any)*  
- **Strategy:**  
- **Time Complexity:**  
- **Space Complexity:**  
- **Outcome:** ✅ / ❌  
- **Notes:**

---

## 6. ✅ Final Accepted Solution

```java
class Solution  implements Comparator<int[]>{

    @Override
    public  int compare(int[] e1, int[] e2){
            return Integer.compare(e1[1], e2[1]);
        }

    public int[] topKFrequent(int[] nums, int k) {

        HashMap<Integer, Integer> freqMap = new HashMap();

        for(int val : nums){
            freqMap.put( val, freqMap.getOrDefault(val, 0) + 1 );
        }

        PriorityQueue<int[]> pQueue = new PriorityQueue<>(new Solution());

        //pQueue = freqMap.keys();

        

        ArrayList<Integer> res = new ArrayList();

        //System.out.println(freqMap);

        System.out.println(pQueue);

        for(Map.Entry<Integer, Integer> entry : freqMap.entrySet()) {

            pQueue.offer( new int[]{entry.getKey(), entry.getValue()} );

            if(pQueue.size() > k)

                pQueue.poll();

            // System.out.println(entry);

         }

        while( ! pQueue.isEmpty() ){

            res.add( pQueue.poll()[0] );

        }

  

        return res.stream().mapToInt(Integer::intValue).toArray();

/*         for(int i = 0; i < k; i++){

            if(itr.hasNext())

                res.add(itr.next());

        } */

  
  
  

    }

}
```

- **Time Complexity:**  
- **Space Complexity:**  
- **Why this works:**  

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
