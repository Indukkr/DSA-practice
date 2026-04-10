# Group Anagrams

## 🧠 Problem
Given an array of strings, group all anagrams together.

---

## 🧠 Brute Force Approach

### Idea
- Compare every pair of strings
- Check if they are anagrams (by sorting or frequency)
- Group accordingly

### Complexity
- Time: O(n^2 * k log k)
- Space: O(n)

### Drawback
- Very inefficient due to repeated comparisons

---

## 🧠 Approach 1: Sorting (Most Intuitive)

### Idea
- Sort each string
- Use sorted string as key
- All anagrams will have same sorted form

### Steps
1. Initialize:
   ```java
   Map<String, List<String>> map = new HashMap<>();
   ```
2. For each string:
   - Convert to char array
   - Sort it
   - Convert back to string → key
   - Add original string to map

3. Return:
   ```java
   new ArrayList<>(map.values());
   ```

### Example
```
"eat" → "aet"
"tea" → "aet"
```

### Complexity
- Time: O(n * k log k)
- Space: O(n * k)

---

## 🧠 Approach 2: Frequency Count (Optimal)

### Idea
- Count frequency of characters (size 26)
- Build a unique key using all 26 counts
- Use this key in HashMap

---

## 🔑 Key Construction

```java
String key = "";
for(int i = 0; i < 26; i++) {
    key = key + "#" + freq[i];
}
```

### Why use `#`?
- Avoid ambiguity (e.g., "11" vs "1#1")

### Why include all 26?
- Position matters
- Avoid collisions

---

## 🧠 Steps
1. For each string:
   - Create frequency array of size 26
   - Count characters
   - Build key using all 26 values
   - Add string to map

2. Return:
   ```java
   new ArrayList<>(map.values());
   ```

---

## ⚠️ Common Mistakes

- ❌ Not resetting frequency array per string  
- ❌ Skipping zero frequencies  
- ❌ Overwriting key instead of appending  
- ❌ Not using separator (`#`) → collisions  
- ❌ Using `new List<>()` (interface cannot be instantiated)

---

## 🔥 Pattern
- HashMap + Key Normalization

---

## 🎯 Key Insight
- Convert each string into a **unique representation**
- Use it to group similar strings

---

## 🎯 Interview Flow
1. Brute force → compare all pairs  
2. Optimize using sorting  
3. Further optimize using frequency array  
