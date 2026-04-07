Problem: Valid Anagram

Approaches:

1. Brute Force:
- Nested loops, track used characters
- Time: O(n^2)

2. Sorting:
- Sort both strings and compare
- Time: O(n log n)

3. Optimal (Frequency Array):
- Use int[26]
- Increment for s, decrement for t
- If freq < 0 → false
- Time: O(n), Space: O(1)

4. HashMap Approach:
- Build frequency map from s
- Traverse t:
  - If key not present → false
  - Decrement count
  - If count == 0 → remove key
- End:
  - If map.isEmpty() → true

Key Insight:
- Problem is about frequency balance, not order

Follow-up:
- Use HashMap when characters are not limited
