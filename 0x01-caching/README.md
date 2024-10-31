# 0x01. Caching
'Backend' 'Python'

## Description
This project implements different caching algorithms in Python. It explores various cache replacement policies including FIFO, LIFO, LRU, MRU, and basic dictionary caching.

## Learning Objectives
After completing this project, you should be able to explain:

- What a caching system is
- Different caching replacement policies:
  - FIFO (First-In-First-Out)
  - LIFO (Last-In-First-Out)
  - LRU (Least Recently Used)
  - MRU (Most Recently Used)
- The purpose and limitations of caching systems

## Requirements

### Python Scripts
- Python 3.7 on Ubuntu 18.04 LTS
- Pycodestyle style (version 2.5)
- All files must be executable
- All modules, classes, and functions must be documented

### Project Structure
The project consists of multiple Python classes that inherit from `BaseCaching`:

```python
class BaseCaching():
    """ Base caching class with maximum items constant """
    MAX_ITEMS = 4

    def __init__(self):
        """ Initialize cache dictionary """
        self.cache_data = {}
```

## Tasks

### 0. Basic Dictionary Cache
- File: `0-basic_cache.py`
- Class: `BasicCache`
- Features:
  - No limit on number of items
  - Methods:
    - `put(key, item)`: Add item to cache
    - `get(key)`: Retrieve item from cache

### 1. FIFO Cache
- File: `1-fifo_cache.py`
- Class: `FIFOCache`
- Features:
  - Maximum items limit
  - First-In-First-Out replacement policy
  - Prints "DISCARD: {key}" when removing item

### 2. LIFO Cache
- File: `2-lifo_cache.py`
- Class: `LIFOCache`
- Features:
  - Maximum items limit
  - Last-In-First-Out replacement policy
  - Prints "DISCARD: {key}" when removing item

### 3. LRU Cache
- File: `3-lru_cache.py`
- Class: `LRUCache`
- Features:
  - Maximum items limit
  - Least Recently Used replacement policy
  - Prints "DISCARD: {key}" when removing item

### 4. MRU Cache
- File: `4-mru_cache.py`
- Class: `MRUCache`
- Features:
  - Maximum items limit
  - Most Recently Used replacement policy
  - Prints "DISCARD: {key}" when removing item

## Usage Examples

### Basic Cache
```python
my_cache = BasicCache()
my_cache.put("A", "Hello")
my_cache.put("B", "World")
print(my_cache.get("A"))  # Output: Hello
```

### FIFO Cache
```python
my_cache = FIFOCache()
my_cache.put("A", "Hello")
my_cache.put("B", "World")
my_cache.put("C", "Holberton")
my_cache.put("D", "School")
my_cache.put("E", "Battery")  # Will discard "A"
```

## Documentation
- All files include proper docstrings
- Documentation can be checked using:
```bash
python3 -c 'print(__import__("my_module").__doc__)'
python3 -c 'print(__import__("my_module").MyClass.__doc__)'
```

## Repository Information
- GitHub Repository: alx-backend
- Directory: 0x01-caching

## License
Copyright © 2024 ALX, All rights reserved.
