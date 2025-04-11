### 1. Write a Lex program that detects relational and logical operators

```c
%{
#include <stdio.h>
%}
%%
"<="    { printf("Relational Operator: <=\n"); }
">="    { printf("Relational Operator: >=\n"); }
"=="    { printf("Relational Operator: ==\n"); }
"!="    { printf("Relational Operator: !=\n"); }
"<"     { printf("Relational Operator: <\n"); }
">"     { printf("Relational Operator: >\n"); }

"&&"    { printf("Logical Operator: &&\n"); }
"||"    { printf("Logical Operator: ||\n"); }
"!"     { printf("Logical Operator: !\n"); }

.|\n    { /* ignore other characters */ }
%%

int main() {
    yylex();
    return 0;
}
int yywrap() {
    return 1;
}
```
### **Compilation & Execution**
```bash
lex pattern.l
gcc lex.yy.c -o lex.out -ll
./lex.out < input.txt
```

---

### 2. First and follow 

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h> // Include this for isupper
#define MAX 10

char first[MAX], follow[MAX];

void findFirst(char prod[], char result[]) {
    if (!isupper(prod[3])) {
        result[0] = prod[3]; // Terminal directly in FIRST
        result[1] = '\0';
    }
}

void findFollow(char start, char prod[], char result[]) {
    if (prod[0] == start && prod[4] != '\0') {
        result[0] = prod[4]; // FOLLOW derived from next symbol
        result[1] = '\0';
    } else {
        result[0] = '$'; // Default FOLLOW for start symbol
        result[1] = '\0';
    }
}

int main() {
    char production[] = "A->bC";
    char start = 'A';

    findFirst(production, first);
    findFollow(start, production, follow);

    printf("First(%c) = {%s}\n", start, first);
    printf("Follow(%c) = {%s}\n", start, follow);

    return 0;
}

```

**Output**
```
First(A) = {b}
Follow(A) = {C}
```
---
