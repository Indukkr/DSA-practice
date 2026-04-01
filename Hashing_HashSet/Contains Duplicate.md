1. Brute Force:
- Use nested loops to compare each element with others
- If match found → duplicate exists
- Time: O(n²), Space: O(1)

2. Better Approach (Sorting):
- Sort the array
- Check adjacent elements for equality
- Time: O(n log n), Space: O(1)

3. Optimal Approach (HashSet):
- Store elements in HashSet while traversing
- If element already exists → duplicate found
- Time: O(n), Space: O(n)

Decision:
- Use HashSet for optimal time complexity
- Use sorting when space is restricted

Pattern Trigger:
- "Have I seen this element before?"
