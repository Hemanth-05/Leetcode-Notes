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

## Top K Frequent Elements
For this we have two approaches: 
- Sorting 0(n log n)
- Bucket 0(n)
)
### Sorting Approach

**When to use**
- Need K most frequent elements
- Simple implementation preferred
- O(n log n) is acceptable

**Core Idea**
- Create a map with elements->frequency
- Convert map to pair: elements->frequency to pair(element, frequency)
- Sort pairs on frequency
- Now retrive top K pairs based on frequency

**Data Structures**
- unordered_map<int,int> → number → frequency
- vector<pair<int,int>> → (number, frequency)

**Why this works**
- Sorting places highest frequencies first
- Top K automatically at front

**Complexity**
Time:  O(n log n)  
Space: O(n)

**Pattern**
Count → Convert → Sort → Take K




### Bucket approach

**When to use**
- Need better than O(n log n)
- Want near linear time
- Frequency range is bounded (≤ n)

**Key Idea**
- Use frequency as an index
- Group numbers by how many times they appear
- Avoid sorting completely

**Data Structures**
- unordered_map<int,int> → number → frequency
- vector<vector<int>> → index = frequency, value = list of numbers

**Steps**
1. In this we first create a map with element->frequency.
2. Create a vector of vectors, basically a list(array). The thinking is that we will keep the frequency as index and whatever the elements we have for that frequency, we place it in that index. If there are multiple, we can make a list, whats why we are using vector of vectors.
3. Once the list is done, its time to traverse the list from last index (Highest frequency) until we get k elements.
4. Once we get k elements, we break out of the loop

**Why this works**
- Direct placement by frequency (no comparisons)
- Highest frequency found first by reverse traversal

**Complexity**
Time:  O(n)
Space: O(n)

**Pattern**
Count → Bucket → Reverse scan → Take K.

## Encode and Decode Strings

**When to use**
- Need to convert a list of strings into a single string
- Data must be transmitted or stored as one string
- Must be decoded back without ambiguity

**Key Observation**
- Using a delimiter between strings is unsafe (strings may contain it)
- Length information removes ambiguity
- Metadata + payload pattern is required

**Data Structure**
- Encoding: `string`
- Decoding: `vector<string>`

**Core Idea**
- Encode each string as:
  - `length : string`
- Concatenate all encoded parts into one string
- While decoding:
  - read digits until `:`
  - convert digits → length `L`
  - read next `L` characters as the string
  - repeat until end

**Example**
["Hello", "World", "3:abc"] → "5:Hello5:World5:3:abc"

**Why this works**
- Length determines payload boundaries
- Payload may contain any characters (`:`, digits, symbols)
- No guessing or splitting needed

**Pattern to Remember**
- Length-prefixed encoding
- Index-based decoding (pointer jumps)

**Time / Space**
- Time: O(n) total characters
- Space: O(n) for encoded string / decoded output

## Product of Array Except Self
- Goal is simple! Build a left product array and build a right product array and then do the product of both.

## Valid Sudoku

**Problem**
Check whether a given 9×9 Sudoku board is valid.
- Digits `1–9` must not repeat in:
  - any **row**
  - any **column**
  - any **3×3 box**
- Empty cells are represented by `'.'` and should be ignored.

**Core Idea**
While scanning the board, we only care whether a digit has been **seen before** in a specific scope (row / column / box).

Since we only need a *presence check*, a **set** is sufficient.

**Row Check**
- Traverse each row one by one.
- Use a set to track digits seen in the current row.
- If a digit already exists in the set → return `false`.
- Clear the set after finishing each row.

**Column Check**
- Traverse each column one by one.
- Similar to rows, use a set for each column.
- If a duplicate is found → return `false`.
- Clear the set after each column.

**3×3 Box Check**
- The board contains **9 boxes**, each of size 3×3.
- Each box starts at indices where:
  - row ∈ `{0, 3, 6}`
  - col ∈ `{0, 3, 6}`
- For every box:
  - start at `(startRow, startCol)`
  - scan the 3×3 area:
    - rows: `startRow → startRow + 2`
    - cols: `startCol → startCol + 2`
  - use a set to track seen digits
  - clear the set after finishing each box

**Important Notes**
- Always **skip `'.'`** (empty cells).
- If any duplicate is found in row, column, or box → return `false`.
- If all checks pass → return `true`.

**Optimization Note**
- Since we only check *existence*, `unordered_set<char>` is preferred over `unordered_map<char, int>`.
- Time Complexity: **O(81)** → effectively constant
- Space Complexity: **O(9)** per check


## Longest Consecutive Sequence
- Main point before starting: Do we need to sort the array to find the longest consecutive sequence? **NO. Not Required!**
- Data Structure we can use: unordered_set

**Core Idea**
- Check if the element we chose is the starting element  
    How do we know if its the starting. For an element x, check if x-1 exists, if it does, skip it. If not, then its the starting element. Once we find the starting, we can go forward.

**Implementation**
- We usually use 2 loops here. Outer loop is to check if the element chosen is starting or not.
- Inner loop is to move forward. We only move forward when we know that its the starting element.

NOTE: Always make sure the outerloop is done on the unordered_set and not the input array/vector. In this way we can eliminate the duplicates and reduce unnecesserly doing duplicate checks. Otherwise we will get **Time Limit Exceeded error**.