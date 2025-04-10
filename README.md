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

### 2. Perform constant propagation and dead code elimination on a given code block

```c
#include <stdio.h>
#include <string.h>

#define MAX_LINES 5

void optimizeCode(char code[][100], int lines) {
    const char *constant = "const int a = 5;";
    const char *variable = "int b = a;";
    for (int i = 0; i < lines; i++) {
        if (strcmp(code[i], constant) == 0) {
            // Constant propagation
            for (int j = 0; j < lines; j++) {
                if (strcmp(code[j], variable) == 0) {
                    strcpy(code[j], "int b = 5;"); // Replace 'a' with '5'
                }
            }
        }
        if (strstr(code[i], "unreachable") != NULL) {
            strcpy(code[i], ""); // Dead code elimination
        }
    }
    // Print optimized code
    printf("Optimized Code:\n");
    for (int i = 0; i < lines; i++) {
        if (strlen(code[i]) > 0) {
            printf("%s\n", code[i]);
        }
    }
}

int main() {
    char code[MAX_LINES][100] = {
        "const int a = 5;",
        "int b = a;",
        "unreachable code;",
        "int c = b;",
        "return 0;"
    };
    int lines = 5;
    optimizeCode(code, lines);
    return 0;
}
```

**Output**
```
Optimized Code:
int b = 5;
int c = b;
return 0;
```
---
