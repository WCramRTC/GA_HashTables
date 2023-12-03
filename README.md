
# Comprehensive Tutorial on Hash Tables

## Introduction

This tutorial provides an in-depth understanding of hash tables, including their creation, operation, and real-world applications, supplemented with examples in C#.

### What is a Hash Table?

A hash table is a data structure that stores key-value pairs. It uses a hash function to compute an index into an array of buckets, from which the desired value can be found.

### C# Example: Creating a Basic Hash Table

**Example: Implementing a Simple Hash Table**
```csharp
public class HashTable<TKey, TValue>
{
    private class KeyValueNode
    {
        public TKey Key;
        public TValue Value;
        public KeyValueNode Next;

        public KeyValueNode(TKey key, TValue value)
        {
            Key = key;
            Value = value;
            Next = null;
        }
    }

    private KeyValueNode[] buckets;

    public HashTable(int size)
    {
        buckets = new KeyValueNode[size];
    }

    private int GetBucketIndex(TKey key)
    {
        int hash = key.GetHashCode();
        int index = hash % buckets.Length;
        return Math.Abs(index);
    }

    public void Add(TKey key, TValue value)
    {
        int bucketIndex = GetBucketIndex(key);
        KeyValueNode newNode = new KeyValueNode(key, value);

        if (buckets[bucketIndex] == null)
        {
            buckets[bucketIndex] = newNode;
        }
        else
        {
            KeyValueNode current = buckets[bucketIndex];
            while (current.Next != null)
            {
                current = current.Next;
            }
            current.Next = newNode;
        }
    }

    public TValue Get(TKey key)
    {
        int bucketIndex = GetBucketIndex(key);
        KeyValueNode current = buckets[bucketIndex];

        while (current != null)
        {
            if (current.Key.Equals(key))
            {
                return current.Value;
            }
            current = current.Next;
        }

        throw new Exception("Key not found");
    }
}
```

### How Does a Hash Table Work?

A hash table uses a hash function to convert keys into array indices. When adding a new key-value pair, the key is hashed, and the value is placed in the corresponding bucket. If two keys hash to the same index, a collision occurs, and the hash table must handle it, typically by chaining (using linked lists) or open addressing.

### Advantages and Disadvantages

- **Advantages:**
  - Fast access: Average time complexity for insertions, deletions, and retrievals is O(1).
  - Efficient: Makes efficient use of memory.

- **Disadvantages:**
  - Collision handling: Requires additional logic.
  - Hash function: The efficiency largely depends on the quality of the hash function.

### Real-World Applications

- Storing and accessing data quickly, such as in database indexing.
- Implementing associative arrays or dictionaries in programming languages.
- Caching frequently accessed data.

### Conclusion

Hash tables are a powerful and efficient way to store and access data based on keys. They are widely used in computer science for tasks that require rapid data retrieval.

### Further Learning
- Explore different collision resolution techniques like linear probing and quadratic probing.
- Implement a hash table with resizing capability to handle more data efficiently.
- Study the implementation of hash tables in various programming languages and frameworks.
