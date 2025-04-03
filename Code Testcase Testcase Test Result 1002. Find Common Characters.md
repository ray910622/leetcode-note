## Initial Solution
1. Use 26 characters hashmap to count letter frequencies for each word
2. For 26 characters, find the minimum frequency of each letter, store in `minCommon`.
3. Append each character to the result `minCommon` times.
   - Convert the character to a tring before appending.

```cpp
class Solution {
public:
    vector<string> commonChars(vector<string>& words) {
        vector<vector<int>> hashmap(26, vector<int>(words.size(), 0));
        vector<string> res;
        for (int k = 0; k < words.size(); k++)
            for (int i = 0; i < words[k].size(); i++) 
                hashmap[words[k][i] - 'a'][k]++;

        for (int i = 0; i < 26; i++) {
            int minCommon = INT_MAX;
            for (int j = 0; j < words.size(); j++) 
                minCommon = min(minCommon, hashmap[i][j]);
            
            while (minCommon--) 
                res.push_back(string(1, 'a' + i));
        }
        return res;
    }
};
```
## Note
- Time Complexity: `O(nm)`, where `n` is the length of the word, `m` is the numbers of words.
- We can use 1D array to store hashmap instead of 2D.

## Second Solution
1. For each word in `words`, count the frequency of each letters, store in `freq[26]`
2. Update the minimum frequency of each character in `minHash`.
3. For each character `a` to `z`, append it to the result `minHash[c]` times.


```cpp
class Solution {
public:
    vector<string> commonChars(vector<string>& words) {
        vector<string> res;
        vector<int> minHash(26, INT_MAX);
        for (string s : words) {
            vector<int> freq(26, 0);
            for (char c : s)
                freq[c - 'a']++;
            for (int k = 0; k < 26; k++)
                minHash[k] = min(minHash[k], freq[k]);
        }

        for (int k = 0; k < 26; k++) {
            if (minHash[k] > 0) {
                res.insert(res.end(), minHash[k], string(1, 'a' + k));
            }
        }
        return res;
    }
};
```


> 2025.04.03
