# Custom libc

A static C library with implementations of common memory, string, character, and conversion functions, plus file-descriptor output helpers and a generic singly linked list.

The library uses the `ft_` prefix and builds as `libft.a`. All declarations are available through `libft.h`.

## Build and use

Requires `make`, a C compiler, and the `ar` archiver on a Unix-like system.

```bash
make
```

The default build includes every function, including linked-list utilities.

Save this example as `main.c`:

```c
#include "libft.h"

int main(void)
{
    char *message;

    message = ft_strjoin("Hello, ", "world!");
    if (!message)
        return (1);
    ft_putendl_fd(message, 1);
    free(message);
    return (0);
}
```

Compile and run from the repository root:

```bash
cc -Wall -Wextra -Werror main.c -I. -L. -lft -o program
./program
```

`make clean` removes object files, `make fclean` also removes the library, and `make re` rebuilds it.

## Function groups

| Group | Functions |
| --- | --- |
| Character checks | `ft_isalpha`, `ft_isdigit`, `ft_isalnum`, `ft_isascii`, `ft_isprint` |
| Character conversion | `ft_tolower`, `ft_toupper` |
| Memory | `ft_memset`, `ft_bzero`, `ft_memcpy`, `ft_memmove`, `ft_memchr`, `ft_memcmp`, `ft_calloc` |
| String length, copying, and search | `ft_strlen`, `ft_strlcpy`, `ft_strlcat`, `ft_strchr`, `ft_strrchr`, `ft_strncmp`, `ft_strnstr` |
| String allocation and transformation | `ft_strdup`, `ft_substr`, `ft_strjoin`, `ft_strtrim`, `ft_split`, `ft_strmapi`, `ft_striteri` |
| Numeric conversion | `ft_atoi`, `ft_itoa` |
| File-descriptor output | `ft_putchar_fd`, `ft_putstr_fd`, `ft_putendl_fd`, `ft_putnbr_fd` |
| List creation and insertion | `ft_lstnew`, `ft_lstadd_front`, `ft_lstadd_back` |
| List inspection and transformation | `ft_lstsize`, `ft_lstlast`, `ft_lstiter`, `ft_lstmap` |
| List cleanup | `ft_lstdelone`, `ft_lstclear` |

## Implementation

Each function is implemented in its own source file. The Makefile compiles those files into object files and archives them into `libft.a`.

### Memory and strings

Memory operations work byte by byte. `ft_memmove` chooses the copy direction to preserve data when source and destination overlap. `ft_calloc` checks the requested allocation size for multiplication overflow, allocates memory, and clears it.

String helpers distinguish between operations on caller-provided storage and operations that allocate new strings. For example, `ft_striteri` modifies a string through a callback, while `ft_strmapi` allocates a transformed copy.

`ft_split` counts tokens, allocates a null-terminated array, and allocates each token separately. If a token allocation fails, it frees the tokens already created and the array before returning `NULL`.

### Generic linked lists

Each `t_list` node contains a `void *content` pointer and a `next` pointer. List operations are independent of the payload type.

`ft_lstnew` stores the supplied content pointer without copying the payload. Callbacks define how content is processed and released:

- `ft_lstiter` applies a callback to each existing payload.
- `ft_lstmap` applies a callback and builds a new list from the returned payloads.
- `ft_lstdelone` and `ft_lstclear` call the supplied destructor before freeing nodes.

If node allocation fails during `ft_lstmap`, the current transformed payload and the partially constructed list are released through the destructor callback. `ft_lstclear` sets the caller's list pointer to `NULL` after cleanup.

## Memory ownership and API scope

- Callers must free allocations returned by `ft_calloc`, `ft_strdup`, `ft_substr`, `ft_strjoin`, `ft_strtrim`, `ft_itoa`, and `ft_strmapi`.
- For `ft_split`, free each token and then the returned array.
- A list's destructor must match the ownership of its contents. Node allocation alone does not transfer or duplicate the underlying data.
- String and memory functions require valid pointers and suitable buffer sizes unless the individual implementation explicitly handles otherwise.
- `ft_atoi` converts the numeric prefix after optional whitespace and a sign; it does not provide overflow checking or an error-reporting interface.
- The library implements the listed functions and utilities, not a complete replacement for the system C library.

## Project background

Developed by **acoromin** as **Libft**, part of the 42 curriculum.

Reference material included *The C Programming Language* by Kernighan and Ritchie, system manual pages, and the original project documentation.

AI tools supported clarification of pointers, linked lists, memory management, and debugging approaches.
