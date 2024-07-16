  
#Python/len 
### 58. Length of Last Word
https://leetcode.com/problems/length-of-last-word/

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        reversed = s[::-1]
        all_words = reversed.split()
        return len(all_words[0])

```

### 709. To Lower Case
https://leetcode.com/problems/to-lower-case/

#Python/String

```python
class Solution:
    def toLowerCase(self, s: str) -> str:
        return s.lower()
```