# Get_Next_Line (42)

> A line-by-line file reading function in **C**. `get_next_line()` returns the next line from a given file descriptor, including the trailing newline when present.

---

## 🚀 Purpose

Provide a robust utility to read **one line at a time** from a file descriptor (regular files, stdin, pipes), handling partial reads and buffering.

---

## ✨ Features

* Reads **one line per call** from a file descriptor
* Preserves the **remainder** between calls (buffered reading)
* Works with **files** and **standard input**
* Implemented in **C** with a configurable `BUFFER_SIZE`

---

## 🔧 Build

Build the project with the included Makefile:

```bash
make          # builds the library or objects used by get_next_line
make clean    # removes object files
make fclean   # removes objects and built artifacts
make re       # rebuild
```

Depending on your repository structure, the build will generate an object archive or object files you can link against your own program.

---

## ▶️ Usage

Typical function signatures (as per the 42 subject):

```c
char    *get_next_line(int fd);
```

**Example (reading from a file):**

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include "get_next_line.h"

int main(void)
{
    int   fd = open("file.txt", O_RDONLY);
    char *line;

    if (fd < 0) return 1;
    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return 0;
}
```

Compile and run:

```bash
gcc -Wall -Wextra -Werror main.c get_next_line.c get_next_line_utils.c -I . -o gnl_demo
./gnl_demo
```

**Read from stdin:**

```bash
./gnl_demo < file.txt
```

> Adjust the compile line to match your exact file names present in this repository.

---

## 📁 Project structure

```
get_next_line/
├─ get_next_line.c
├─ get_next_line.h
├─ get_next_line_utils.c
└─ Makefile
```

---

## 🧠 Implementation notes (fact-based)

* Uses an **internal stash/reminder** to keep unread data between calls
* Uses `read()` in chunks of size `BUFFER_SIZE`
* Returns a **malloc’ed string** (caller must `free()` it)
* Returns `NULL` on **EOF** or **error**

---

## 🧼 Code style

* Complies with **42 Norminette**
* No memory leaks expected (allocated lines must be freed by the caller)

---

## 👤 Author

* Swann — @xSwann
