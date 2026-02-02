# Sorting based Key
    - To eliminate the order of the string, sort the string - Time complexity 0(n log n)

# Frequency based key
Until now I have used it in Group Anagrams
    - Build a fixed-size frequency array of 26 letters (a–z)
    - Each index represents a character count
    - index 0 → 'a', index 1 → 'b', ..., index 25 → 'z'
    - Convert the frequency array into a string key using separators
    - Example: "eat" → "1#0#0#0#1#...#1#"
    - All anagrams produce the same frequency key

    
    for(int number: cnt){
                key.append(to_string(number));
                key.append("#");
            }
     - This is how you create a key for an anagram. This is called frequency key

# Encoding and decoding the strings
**Encoding**
When given a list of strings (e.g. ["Hello", "World", "#22Its"]) and we need to send it as a single string (e.g. over a network), we encode it by attaching metadata.

- Each string is prefixed with its length
- A separator (commonly :) is used between metadata and payload
- Final encoded string is a concatenation of all such chunks
- Example: ["Hello", "World", "#22Its"] → "5:Hello5:World6:#22Its"

**Decoding**
While decoding, we parse the encoded string from left to right using an index pointer.

For each chunk:
1. Read characters until : → this gives the length L
2. Convert length to integer
3. Read the next L characters as the string
4. Add it to the result list
5. Move the pointer forward and repeat

Key idea
- We never split on the payload
- Payload boundaries are determined only by the length
- This avoids ambiguity even if payload contains : or digits