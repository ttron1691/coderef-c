# coderef-c

# C Programming Language Reference Card

## Basic Syntax Elements

### Program Structure
```c
#include <stdio.h>  // Include standard library headers

int main() {
    // Program code goes here
    return 0;       // Return value to operating system
}
```

### Data Types
| Type | Description | Format Specifier | Size (typical) |
|------|-------------|------------------|----------------|
| `int` | Integer | `%d` | 4 bytes |
| `float` | Single-precision floating-point | `%f` | 4 bytes |
| `double` | Double-precision floating-point | `%lf` | 8 bytes |
| `char` | Character (single) | `%c` | 1 byte |
| `_Bool` (C99) | Boolean (true/false) | `%d` | 1 byte |
| `size_t` | Unsigned integer for sizes | `%zu` | 4/8 bytes |

#### Type Modifiers
- `short` - smaller integer (typically 2 bytes)
- `long` - larger integer (typically 4-8 bytes)
- `long long` - even larger integer (typically 8 bytes)
- `unsigned` - non-negative numbers only (doubles positive range)
- `signed` - allows negative numbers (default for numeric types)

### Variable Declaration
```c
int count = 0;                   // Declaration with initialization
const double PI = 3.14159;       // Constant (value cannot change)
static char buffer[100];         // Static duration (persists between function calls)
extern int global_var;           // Reference to variable defined elsewhere
```

### Operators
#### Arithmetic
- `+` (addition)
- `-` (subtraction)
- `*` (multiplication)
- `/` (division)
- `%` (modulo/remainder)
- `++` (increment)
- `--` (decrement)

#### Comparison
- `==` (equal to)
- `!=` (not equal to)
- `>` (greater than)
- `<` (less than)
- `>=` (greater than or equal to)
- `<=` (less than or equal to)

#### Logical
- `&&` (logical AND)
- `||` (logical OR)
- `!` (logical NOT)

#### Bitwise
- `&` (bitwise AND)
- `|` (bitwise OR)
- `^` (bitwise XOR)
- `~` (bitwise complement)
- `<<` (left shift)
- `>>` (right shift)

#### Assignment
- `=` (simple assignment)
- `+=`, `-=`, `*=`, `/=`, `%=` (compound assignment)
- `&=`, `|=`, `^=`, `<<=`, `>>=` (bitwise compound assignment)

## Control Structures

### Conditionals
```c
// If statement
if (condition) {
    // Code executed if condition is true
} else if (another_condition) {
    // Code executed if another_condition is true
} else {
    // Code executed if all conditions are false
}

// Switch statement
switch (expression) {
    case constant1:
        // Code executed if expression == constant1
        break;
    case constant2:
        // Code executed if expression == constant2
        break;
    default:
        // Code executed if no match is found
}
```

### Loops
```c
// For loop
for (initialization; condition; increment) {
    // Code executed while condition is true
}

// While loop
while (condition) {
    // Code executed while condition is true
}

// Do-while loop
do {
    // Code executed at least once, then while condition is true
} while (condition);
```

### Control Flow
```c
continue;    // Skip to next iteration of the enclosing loop
break;       // Exit the enclosing loop or switch statement
return expr; // Exit the current function, optionally returning a value
goto label;  // Jump to the labeled statement (use sparingly)
```

## Functions

### Function Definition
```c
return_type function_name(parameter_type param1, parameter_type param2) {
    // Function body
    return value;  // Optional if return_type is void
}
```

### Function Declaration (Prototype)
```c
return_type function_name(parameter_type param1, parameter_type param2);
```

### Function Pointers
```c
return_type (*pointer_name)(parameter_types);  // Declaration
pointer_name = &function_name;                 // Assignment
result = (*pointer_name)(arguments);           // Call
```

### Variable Arguments
```c
#include <stdarg.h>

void function(int fixed_arg, ...) {
    va_list args;
    va_start(args, fixed_arg);
    
    int value = va_arg(args, int);  // Get next argument as int
    
    va_end(args);
}
```

## Data Structures

### Arrays
```c
int numbers[10];             // Declaration
int values[] = {1, 2, 3, 4}; // Declaration with initialization
numbers[0] = 42;             // Assignment to element
```

### Strings
```c
char str[10] = "Hello";      // String as character array
char *ptr = "World";         // String as pointer to literal
#include <string.h>          // String handling functions
strlen(str);                 // String length
strcpy(dest, src);           // Copy string
strcat(dest, src);           // Concatenate strings
strcmp(s1, s2);              // Compare strings
```

### Structures
```c
struct Person {
    char name[50];
    int age;
    float height;
};  // Define structure

struct Person john = {"John", 30, 6.1};  // Initialize
printf("%s is %d years old\n", john.name, john.age);  // Access members
```

### Unions
```c
union Data {
    int i;
    float f;
    char str[20];
};  // Define union

union Data data;
data.i = 10;  // Now only data.i contains valid data
```

### Enumerations
```c
enum Days {MON=1, TUE, WED, THU, FRI, SAT, SUN};  // Define enum
enum Days today = WED;  // Initialize enum variable
```

### Typedef
```c
typedef unsigned long ulong;  // Create type alias
typedef struct Person Person; // Create alias for structure
```

## Memory Management

### Pointers
```c
int *p;                // Declare pointer
int value = 42;
p = &value;            // Assign address to pointer
*p = 100;              // Dereference pointer (change value)
printf("%d", *p);      // Access value through pointer

// Pointer arithmetic
int arr[5] = {10, 20, 30, 40, 50};
int *ptr = arr;        // Points to arr[0]
printf("%d", *(ptr+2)); // Accesses arr[2]
```

### Dynamic Memory
```c
#include <stdlib.h>

// Allocate single item
int *p = (int *)malloc(sizeof(int));
if (p != NULL) {
    *p = 10;
    free(p);  // Release memory when done
}

// Allocate array
int *arr = (int *)malloc(10 * sizeof(int));
// or with calloc (initializes to zero)
int *arr2 = (int *)calloc(10, sizeof(int));
// Resize allocation
arr = (int *)realloc(arr, 20 * sizeof(int));
```

### Memory Functions
```c
#include <string.h>

memcpy(dest, src, n);   // Copy n bytes from src to dest
memmove(dest, src, n);  // Like memcpy but safe for overlapping regions
memset(ptr, value, n);  // Fill n bytes with specified value
memcmp(ptr1, ptr2, n);  // Compare n bytes
```

## Input/Output

### Standard I/O
```c
#include <stdio.h>

// Output
printf("Hello, %s. You are %d years old.\n", name, age);
putchar('A');    // Write single character
puts("string");  // Write string with newline

// Input
scanf("%d %s", &number, string);
char c = getchar();     // Read single character
fgets(string, size, stdin);  // Read line (safer than gets)
```

### File I/O
```c
FILE *fp;
fp = fopen("file.txt", "r");  // Open file for reading
if (fp != NULL) {
    char buffer[100];
    while (fgets(buffer, sizeof(buffer), fp) != NULL) {
        // Process line
    }
    fclose(fp);  // Close file
}

FILE *out = fopen("output.txt", "w");  // Open for writing
if (out != NULL) {
    fprintf(out, "Hello, %s\n", name);
    fclose(out);
}
```

### File Access Modes
- `"r"` - read
- `"w"` - write (create/truncate)
- `"a"` - append
- `"r+"` - read/update
- `"w+"` - read/write (create/truncate)
- `"a+"` - read/append
- Add `b` for binary mode (e.g., `"rb"`)

## Preprocessor Directives

### Include Files
```c
#include <stdio.h>      // System headers
#include "myheader.h"   // User-defined headers
```

### Macro Definitions
```c
#define PI 3.14159
#define SQUARE(x) ((x) * (x))
#define DEBUG_MODE
```

### Conditional Compilation
```c
#ifdef DEBUG_MODE
    printf("Debug: value = %d\n", x);
#endif

#ifndef BUFFER_SIZE
    #define BUFFER_SIZE 1024
#endif

#if CONDITION
    // Code when condition is true
#elif ANOTHER_CONDITION
    // Code when another_condition is true
#else
    // Code when conditions are false
#endif
```

## Advanced Features

### Bit Fields
```c
struct Flags {
    unsigned int ready:1;    // 1 bit
    unsigned int active:1;   // 1 bit
    unsigned int status:4;   // 4 bits
};
```

### Inline Assembly
```c
#include <stdio.h>

int main() {
    int result;
    __asm__ (
        "movl $10, %0"
        : "=r" (result)
    );
    printf("%d\n", result);
    return 0;
}
```

### Function Attributes (GCC)
```c
__attribute__((noreturn)) void fatal_error();
__attribute__((deprecated)) void old_function();
__attribute__((always_inline)) inline int fast_func();
```

### Thread-Local Storage (C11)
```c
#include <threads.h>
thread_local int counter = 0;
```

### Atomic Operations (C11)
```c
#include <stdatomic.h>
atomic_int counter = ATOMIC_VAR_INIT(0);
atomic_fetch_add(&counter, 1);
```

## Best Practices

### Defensive Programming
- Always check return values from functions that can fail
- Validate input parameters
- Use assert() to validate assumptions:
  ```c
  #include <assert.h>
  assert(ptr != NULL);
  ```
- Add proper error handling for all operations

### Memory Management
- Always free memory that you allocate
- Check for NULL after malloc/calloc/realloc
- Use tools like Valgrind to detect memory leaks
- Consider using smart pointer alternatives for C

### Code Organization
- Use header guards to prevent multiple inclusion:
  ```c
  #ifndef MY_HEADER_H
  #define MY_HEADER_H
  // Header content
  #endif
  ```
- Keep related functions and data in the same module
- Create coherent interfaces in header files

### Safety & Security
- Use bounds checking when accessing arrays
- Prefer `fgets()` over `gets()`
- Use `snprintf()` instead of `sprintf()`
- Avoid dangerous functions:
  - `strcpy()` → `strncpy()`
  - `strcat()` → `strncat()`
  - `gets()` → `fgets()`

### Performance
- Profile before optimizing
- Optimize algorithms before code
- Consider cache locality for data structures
- Minimize heap allocations in performance-critical code

### Portability
- Use fixed-width integer types from `<stdint.h>`:
  - `int8_t`, `uint8_t`, `int32_t`, `uint32_t`, etc.
- Don't assume endianness
- Check for compiler-specific features with `#ifdef`
- Avoid platform-specific assumptions

## Common Standard Libraries

### C Standard Library
- `<stdio.h>` - Input/output
- `<stdlib.h>` - General utilities
- `<string.h>` - String handling
- `<math.h>` - Mathematical functions
- `<time.h>` - Date and time
- `<ctype.h>` - Character classification
- `<assert.h>` - Diagnostics
- `<limits.h>` - Size limits
- `<float.h>` - Floating-point limits
- `<errno.h>` - Error codes
- `<signal.h>` - Signal handling
- `<setjmp.h>` - Non-local jumps
- `<locale.h>` - Localization
- `<stdarg.h>` - Variable arguments
- `<stdbool.h>` - Boolean type (C99)
- `<stdint.h>` - Fixed-width integer types (C99)
- `<complex.h>` - Complex numbers (C99)
- `<fenv.h>` - Floating-point environment (C99)
- `<inttypes.h>` - Format conversion of integer types (C99)
- `<tgmath.h>` - Type-generic math (C99)
- `<threads.h>` - Threading (C11)
- `<stdatomic.h>` - Atomic operations (C11)

