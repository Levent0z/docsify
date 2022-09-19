# Hashing

A `hash function` takes a serializable input ("key") and returns an index into an array. 

- $0 \le index < arraySize$
- Insertion, deletion, search is on average $O(1)$ (unless high `load factor`)
- It should evenly distribute over the size of the array
  
```javascript
function hash(key, hashSize) {
    let hashVal = 0;
    for (const c of key) {
        // Based on "Horner's rule": calculate the polynomial where
        // x=27 (for 26 letters + space) and the coefficients are the values of each letter
        // Use 32 instead of 27 to simplify multiplication 
        hashVal = (hashVal << 5) + c;
    }
    return hashVal % hashSize;
}
```

## Problems

### Problem 1: Collision
Collision happens when two keys map to the same index.

Solution:
- `Open hashing`: Use secondary data structure (e.g. linked lists) to hold colliding entries.
- `Closed hashing`: Use the hash table itself (instead of a secondary data structure)
  - `Linear probing`: Search for subsequent indexes. Cons: causes clustering
  - `Quadratic probing`: Eliminates clustering, but performance degrades when table is half-full
  - `Double hashing`: Apply multiples of a second hash function when probing.
    - $f(i) = i \cdot hash_2(key)$
    - $hash_2$ must never return 0
  
### Problem 2: Table is too full

- Solution: `Rehashing` using bigger hash table size. $O(n)$
- Problem: A lot of items move around (i.e. get new positions) when rehashed. 
- Solution: Use `Consistent Hashing` instead.

### Problem 3: Data is too large

- `Extendible Hashing`
  - Use the first few $n$ bits to create a first-level index
  - Max elements in each second level = total bits - $n$
  - [More on Wikipedia](https://en.wikipedia.org/wiki/Extendible_hashing)


## Consistent Hashing

## Rendezvous Hashing

[More on Wikipedia](https://en.wikipedia.org/wiki/Rendezvous_hashing)




