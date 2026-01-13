## Contains Duplicate

**When to use**
- Detect duplicates
- Check if an element was seen before
- Need fast existence check

**Data Structure**
- `unordered_set`

**Key Method**
- `count(x)`
  - returns `1` → if `x` exists in the set
  - returns `0` → if `x` does NOT exist

**Core Idea**
- Iterate through array
- Check if element already exists
- Insert if not seen

**Template**
```cpp
unordered_set<int> st;
for (int x : nums) {
    if (st.count(x)) return true;
    st.insert(x);
}
return false;
```

## Two Sum

**When to use**
- Find two elements that add up to a target
- Need indices, not values

**Data Structure**
- `unordered_map<int, int>` (value → index)

**Key Method**
- `mp.find(need) != mp.end()`

**Core Idea**
- For each element x at index i:
  - compute need = target - x
  - if need exists in map → return indices
  - otherwise store x with its index
- Check before inserting to avoid using the same element twice

**Why not set?**
- Because indices are required

**Time / Space**
- O(n) / O(n)

## Valid Anagram

**When to use**
- Check if two strings contain the same characters
- Order does NOT matter
- Frequency of characters matters

**Key Observation**
- Anagrams must have the same length
- Each character must appear the same number of times in both strings

**Data Structure**
- `unordered_map<char, int>` (character → frequency)

**Core Idea**
- If lengths differ → not an anagram
- Count frequency of characters in first string
- For second string:
  - if character not found → false
  - decrement frequency
  - if frequency goes below zero → false

**Why this works**
- Ensures same characters with same counts
- Prevents subset/superset cases

**Time / Space**
- Time: O(n)
- Space: O(1) (bounded by alphabet size)


