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

## Group Anagrams

**Example**
Input: ["eat","tea","tan","ate","nat","bat"]
Output: [["eat","tea","ate"],["tan","nat"],["bat"]]

**When to use**
- Need to group strings that are anagrams of each other
- Order of characters does NOT matter
- Comparing every pair would be too slow

**Key Insight**
- Comparing all pairs → O(n² · k) ❌
- Instead, give each word a **canonical representation (key)**
- All anagrams share the same key

**Canonical Key**
Two valid ways:
1. **Sorting-based key** - To eliminate the order of the string
   - Sort characters of the word
   - Example: "eat", "tea", "ate" → "aet"

2. **Frequency-based key**
   - Count frequency of each character
   - Same counts → same group
      - Build a fixed-size frequency array of 26 letters (a–z)
      - Each index represents a character count
      - index 0 → 'a', index 1 → 'b', ..., index 25 → 'z'
      - Convert the frequency array into a string key using separators
      - Example: "eat" → "1#0#0#0#1#...#1#"
      - All anagrams produce the same frequency key


**Data Structure**
- `unordered_map<key, vector<string>>`
- Key → identifies the anagram group
- Value → list of words in that group

**Core Idea**
- For each word:
  - compute its key
  - push the word into `mp[key]`
- After processing all words:
  - return all map values (groups)

**Important C++ Trick**
- `mp[key].push_back(word)`
  - creates key if it doesn’t exist
  - appends if it already exists

**Why this works**
- All anagrams map to the same key
- No pairwise comparison needed

**Why Frequency Key is Efficient**
- Avoids sorting each word
- Counting characters takes O(k)
- Fixed alphabet size (26) keeps key construction fast
- Better for longer strings compared to sorting

**C++ Implementation Notes**
- Prefer `array<int, 26>` over `vector<int>` for fixed alphabets
- Use `char - 'a'` to map characters to indices
- Use `const string&` when iterating to avoid copies

**Time / Space**
- Sorting-based key:
  - Time: O(n · k log k)
  - Space: O(n · k)
- Frequency-based key:
  - Time: O(n · k)
  - Space: O(n · k)




