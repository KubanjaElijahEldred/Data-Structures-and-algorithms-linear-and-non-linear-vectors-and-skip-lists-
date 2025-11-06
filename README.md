# Linear and Non-Linear Data Structures in C

A comprehensive implementation of **Vector** (linear) and **Skip List** (non-linear) data structures with clean interfaces and complete demonstrations.

## 📚 Overview

This project implements two fundamental data structures:

### 1. **Vector** (Linear Data Structure)
- Dynamic array implementation with automatic resizing
- Provides constant-time random access: **O(1)**
- Amortized constant-time append: **O(1)***
- Generic storage using void pointers

### 2. **Skip List** (Non-Linear Data Structure)
- Probabilistic data structure with multiple levels
- Logarithmic time complexity for search/insert/delete: **O(log n)*** average
- Self-balancing through randomization
- Maintains sorted order automatically

## 🗂️ Project Structure

```
linear and non linear/
├── vector.h           # Vector interface definition
├── vector.c           # Vector implementation
├── skiplist.h         # Skip List interface definition
├── skiplist.c         # Skip List implementation
├── main.c             # Demonstration program
├── Makefile           # Build configuration
└── README.md          # This file
```

## 🔧 Compilation

### Prerequisites
- GCC compiler (or any C11-compatible compiler)
- Make utility (optional, but recommended)

### Build Instructions

**Using Make:**
```bash
make                 # Build the program
make run             # Build and run
make clean           # Remove build artifacts
make rebuild         # Clean and rebuild
make help            # Show available targets
```

**Manual Compilation:**
```bash
gcc -Wall -Wextra -std=c11 -O2 -o data_structures main.c vector.c skiplist.c
./data_structures
```

## 📖 API Reference

### Vector API

```c
// Create and destroy
Vector* vector_create(size_t initial_capacity);
void vector_destroy(Vector *vec);

// Core operations
bool vector_append(Vector *vec, void *value);           // O(1)*
bool vector_insert(Vector *vec, size_t index, void *value);  // O(n)
void* vector_remove(Vector *vec, size_t index);         // O(n)
void* vector_get(const Vector *vec, size_t index);      // O(1)
bool vector_set(Vector *vec, size_t index, void *value); // O(1)

// Utility functions
size_t vector_size(const Vector *vec);
size_t vector_capacity(const Vector *vec);
bool vector_is_empty(const Vector *vec);
void vector_clear(Vector *vec);
void vector_print(const Vector *vec, void (*print_func)(void*));
```

### Skip List API

```c
// Create and destroy
SkipList* skiplist_create(int max_level);
void skiplist_destroy(SkipList *list);

// Core operations
bool skiplist_insert(SkipList *list, int key, void *value);  // O(log n)*
void* skiplist_search(const SkipList *list, int key);        // O(log n)*
bool skiplist_delete(SkipList *list, int key);               // O(log n)*
bool skiplist_contains(const SkipList *list, int key);       // O(log n)*

// Utility functions
size_t skiplist_size(const SkipList *list);
bool skiplist_is_empty(const SkipList *list);
void skiplist_clear(SkipList *list);
int skiplist_get_max_level(const SkipList *list);
int skiplist_get_level(const SkipList *list);
void skiplist_print(const SkipList *list, void (*print_func)(void*));
void skiplist_print_structure(const SkipList *list);
```

## 💡 Usage Examples

### Vector Example

```c
#include "vector.h"

// Create vector
Vector *vec = vector_create(10);

// Add elements
int *val = malloc(sizeof(int));
*val = 42;
vector_append(vec, val);

// Access elements
int *item = (int*)vector_get(vec, 0);
printf("Value: %d\n", *item);

// Clean up
for (size_t i = 0; i < vector_size(vec); i++) {
    free(vector_get(vec, i));
}
vector_destroy(vec);
```

### Skip List Example

```c
#include "skiplist.h"

// Create skip list
SkipList *list = skiplist_create(MAX_LEVEL);

// Insert key-value pairs
skiplist_insert(list, 42, "Answer");
skiplist_insert(list, 7, "Lucky");
skiplist_insert(list, 23, "Jordan");

// Search
char *result = (char*)skiplist_search(list, 42);
printf("Found: %s\n", result);  // Output: Found: Answer

// Delete
skiplist_delete(list, 7);

// Clean up
skiplist_destroy(list);
```

## 📊 Time Complexity Comparison

| Operation | Vector | Skip List |
|-----------|--------|-----------|
| Access    | O(1)   | N/A       |
| Search    | O(n)   | O(log n)* |
| Insert    | O(n)   | O(log n)* |
| Delete    | O(n)   | O(log n)* |
| Append    | O(1)*  | N/A       |

*Amortized or average case

## 🎯 Key Features

### Vector
- ✅ Dynamic resizing with growth factor of 2
- ✅ Generic storage via void pointers
- ✅ Cache-friendly sequential memory layout
- ✅ Index bounds checking
- ✅ Memory-efficient for sequential access

### Skip List
- ✅ Probabilistic balancing (p = 0.5)
- ✅ Multiple levels (max 16 by default)
- ✅ Logarithmic operations on average
- ✅ Maintains sorted order
- ✅ No complex tree rotations needed

## 🔍 When to Use

**Use Vector when:**
- Random access by index is primary operation
- Memory locality and cache performance are important
- Data is accessed sequentially
- Predictable performance is needed

**Use Skip List when:**
- Data needs to remain sorted
- Frequent searches in sorted data
- Insert/delete operations are common
- Simpler implementation than balanced trees is preferred

## 🧪 Running the Demo

The `main.c` file includes comprehensive demonstrations:

```bash
make run
```

This will show:
1. Vector operations with detailed output
2. Skip List operations including structure visualization
3. Time complexity comparison
4. Memory management examples

## 📝 Memory Management

Both data structures use manual memory management:
- **Vector**: Stores pointers to user-allocated data
- **Skip List**: Stores pointers to user-allocated values

**Important**: Users are responsible for:
- Allocating data before insertion
- Freeing data after removal or before destroying the structure

## 🔬 Technical Details

### Vector Implementation
- Initial capacity: 16 elements
- Growth factor: 2x when capacity exceeded
- Uses `realloc` for efficient resizing
- Uses `memmove` for element shifting

### Skip List Implementation
- Maximum level: 16 (configurable via MAX_LEVEL)
- Probability factor: 0.5
- Random level generation using standard C `rand()`
- Header node with all levels initialized

## 🤝 Contributing

Feel free to extend these implementations with:
- Additional operations (e.g., vector_find, skiplist_range_query)
- Iterator support
- Custom comparison functions
- Thread-safety mechanisms

## 📜 License

This is an educational implementation. Use freely for learning and projects.

## 👨‍💻 Author

Created as a demonstration of linear and non-linear data structures in C.

---

**Note**: This implementation prioritizes clarity and educational value. For production use, consider additional error handling, thread safety, and optimization.
