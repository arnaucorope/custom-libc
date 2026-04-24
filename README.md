*This project has been created as part of the 42 curriculum by acoromin.*

---

# Libft

## 📌 Description

Libft is a custom C library that reimplements essential functions from the standard C library, along with additional utilities.

The goal of this project is to build a deep understanding of:

* Memory management (`malloc`, `free`)
* Pointer manipulation
* String processing
* Data structures, especially linked lists

This library serves as a foundational toolkit that will be reused and extended in future 42 projects.

---

## ⚙️ Instructions

### Compilation

To compile the library:

```bash
make
```

This will generate:

```bash
libft.a
```

---

### Cleaning

```bash
make clean    # remove object files
make fclean   # remove object files and library
make re       # recompile everything
```

---

### Usage

Include the header in your project:

```c
#include "libft.h"
```

Compile your program with:

```bash
gcc main.c -L. -lft -o program
```

---

## 📚 Library Overview

The library is organized into functional groups:

### 🔹 Character Functions

Character checks and transformations:

* `ft_isalpha`, `ft_isdigit`, `ft_isalnum`, `ft_isascii`, `ft_isprint`
* `ft_tolower`, `ft_toupper`

---

### 🔹 Memory Functions

Low-level memory manipulation:

* `ft_memset`, `ft_bzero`, `ft_memcpy`, `ft_memmove`
* `ft_memchr`, `ft_memcmp`, `ft_calloc`

---

### 🔹 String Functions

String manipulation and creation:

* `ft_strlen`, `ft_strdup`, `ft_strlcpy`, `ft_strlcat`
* `ft_strchr`, `ft_strrchr`, `ft_strncmp`, `ft_strnstr`
* `ft_substr`, `ft_strjoin`, `ft_strtrim`, `ft_split`
* `ft_strmapi`, `ft_striteri`

---

### 🔹 Conversion Functions

* `ft_atoi`
* `ft_itoa`

---

### 🔹 File Descriptor Output

* `ft_putchar_fd`
* `ft_putstr_fd`
* `ft_putendl_fd`
* `ft_putnbr_fd`

---

### 🔹 Linked List Functions

Generic singly linked list implementation using `void *`:

* Creation: `ft_lstnew`
* Insertion: `ft_lstadd_front`, `ft_lstadd_back`
* Iteration: `ft_lstiter`, `ft_lstmap`
* Utilities: `ft_lstsize`, `ft_lstlast`
* Memory management: `ft_lstdelone`, `ft_lstclear`

These functions allow flexible handling of dynamic data structures.

---

## 🧠 Technical Notes

Functions like `ft_split` and `ft_lstmap` require:

* Careful memory allocation and deallocation
* Handling edge cases (NULL pointers, empty strings)
* Understanding of dynamic data structures

In particular, `ft_lstmap` demonstrates advanced concepts such as:

* Transforming data while preserving structure
* Error handling with partial allocations
* Proper cleanup to avoid memory leaks

---

## 📖 Resources

* *The C Programming Language* – Kernighan & Ritchie
* Manual pages (`man malloc`, `man free`, `man write`)
* Official 42 subject documentation

---

## 🤖 AI Usage

AI tools were used to:

* Clarify complex concepts (pointers, linked lists, memory management)
* Assist in reasoning and debugging approaches

All code was written, tested, and fully understood by the author.

---

## 🧩 Project Importance

This project is fundamental within the 42 curriculum, as it builds the base required for:

* `ft_printf`
* `get_next_line`
* `push_swap`

It reinforces low-level programming skills essential for mastering C.

