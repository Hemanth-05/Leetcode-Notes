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