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

    ```C++
    for(int number: cnt){
                key.append(to_string(number));
                key.append("#");
            }
    ``` - This is how you create a key for an anagram. This is called frequency key