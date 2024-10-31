# 0x00. Pagination

This project implements various pagination techniques for handling large datasets, with a focus on backend implementation using Python.

## Description

This project explores different pagination methods including:
- Simple pagination with page and page_size parameters
- Hypermedia pagination with metadata
- Deletion-resilient pagination

## Resources

- [REST API Design: Pagination](https://www.moesif.com/blog/technical/api-design/REST-API-Design-Filtering-Sorting-and-Pagination/#pagination)
- [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

## Learning Objectives

After completing this project, you should be able to:

- Implement pagination using simple page and page_size parameters
- Create pagination with hypermedia metadata
- Build deletion-resilient pagination systems

## Requirements

### General

- All files interpreted/compiled on Ubuntu 18.04 LTS using Python 3.7
- All files should end with a new line
- First line of all files should be `#!/usr/bin/env python3`
- Code should use pycodestyle (version 2.5.*)
- All modules should have documentation
- All functions should have documentation
- All functions and coroutines must be type-annotated

### Project Setup

The project uses a dataset from `Popular_Baby_Names.csv` for demonstration purposes.

## Tasks

### 0. Simple Helper Function
**File:** `0-simple_helper_function.py`

Implement a function `index_range` that takes two integer arguments `page` and `page_size`:
- Returns a tuple of size two containing start and end indexes
- Page numbers are 1-indexed

Example:
```python
res = index_range(1, 7)
print(type(res))  # <class 'tuple'>
print(res)        # (0, 7)
```

**Test File (`0-main.py`):**
```python
#!/usr/bin/env python3
"""
Main file for testing simple helper function
"""

index_range = __import__('0-simple_helper_function').index_range

res = index_range(1, 7)
print(type(res))
print(res)

res = index_range(page=3, page_size=15)
print(type(res))
print(res)
```

### 1. Simple Pagination
**File:** `1-simple_pagination.py`

Implement a `Server` class with:
- Dataset loading from CSV
- `get_page` method for basic pagination
- Input validation using assertions

**Test File (`1-main.py`):**
```python
#!/usr/bin/env python3
"""
Main file for testing simple pagination
"""

Server = __import__('1-simple_pagination').Server

server = Server()

try:
    should_err = server.get_page(-10, 2)
except AssertionError:
    print("AssertionError raised with negative values")

try:
    should_err = server.get_page(0, 0)
except AssertionError:
    print("AssertionError raised with 0")

try:
    should_err = server.get_page(2, 'Bob')
except AssertionError:
    print("AssertionError raised when page and/or page_size are not ints")

print(server.get_page(1, 3))
print(server.get_page(3, 2))
print(server.get_page(3000, 100))
```

### 2. Hypermedia Pagination
**File:** `2-hypermedia_pagination.py`

Extend the `Server` class with:
- `get_hyper` method returning dictionary with:
  - page_size: length of dataset page
  - page: current page number
  - data: dataset page
  - next_page: number of next page
  - prev_page: number of previous page
  - total_pages: total number of pages

**Test File (`2-main.py`):**
```python
#!/usr/bin/env python3
"""
Main file for testing hypermedia pagination
"""

Server = __import__('2-hypermedia_pagination').Server

server = Server()

print(server.get_hyper(1, 2))
print("---")
print(server.get_hyper(2, 2))
print("---")
print(server.get_hyper(100, 3))
print("---")
print(server.get_hyper(3000, 100))
```

### 3. Deletion-resilient Hypermedia Pagination
**File:** `3-hypermedia_del_pagination.py`

Implement deletion-resilient pagination:
- Handle cases where rows are deleted between queries
- Ensure users don't miss items when changing pages
- Return appropriate index information

**Test File (`3-main.py`):**
```python
#!/usr/bin/env python3
"""
Main file for testing deletion-resilient hypermedia pagination
"""

Server = __import__('3-hypermedia_del_pagination').Server

server = Server()

server.indexed_dataset()

try:
    server.get_hyper_index(300000, 100)
except AssertionError:
    print("AssertionError raised when out of range")        

index = 3
page_size = 2

print("Nb items: {}".format(len(server._Server__indexed_dataset)))

# 1- request first index
res = server.get_hyper_index(index, page_size)
print(res)

# 2- request next index
print(server.get_hyper_index(res.get('next_index'), page_size))

# 3- remove the first index
del server._Server__indexed_dataset[res.get('index')]
print("Nb items: {}".format(len(server._Server__indexed_dataset)))

# 4- request again the initial index -> first data retrieved is not the same as the first request
print(server.get_hyper_index(index, page_size))

# 5- request again initial next index -> same data page as the request 2-
print(server.get_hyper_index(res.get('next_index'), page_size))
```

## Testing

Each task comes with a corresponding main file for testing. To test a specific task:

1. Make sure the implementation file and test file are in the same directory
2. Make the test file executable: `chmod +x <test_file.py>`
3. Run the test: `./<test_file.py>`

Expected outputs are provided in the task descriptions.

## Usage

Example usage for simple pagination:

```python
server = Server()
server.get_page(1, 3)  # Returns first 3 items
server.get_page(3, 2)  # Returns items 5-6
```

Example usage for hypermedia pagination:

```python
server = Server()
server.get_hyper(1, 2)  # Returns page 1 with size 2 and metadata
```

## Author
Nyemba Martin

## License
Copyright © 2024 ALX, All rights reserved.
