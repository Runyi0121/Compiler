# BMinor Compiler

A compiler for BMinor. It is a strongly-typed language supporting expressions, basic control flow, and recursive functions. Output is x86 assembly compatible with C, allowing use of the C standard libraries.

**Course:** Compilers, Fall 2023  
**Author:** Runyi Shi  
**Language spec:** [dthain.github.io/compilers-fa23/bminor.html](https://dthain.github.io/compilers-fa23/bminor.html)

---

## Build

```bash
cd main
make bminor
```

---

## Compiler Pipeline

The compiler runs in five sequential stages. Each stage can be invoked independently for debugging.

### 1. Scanning

Tokenizes the source file using Flex and regular expression matching.

```bash
./bminor -scan sourcefile.bminor
```

### 2. Parsing

Builds a parse tree from tokens using a Bison context-free grammar.

```bash
./bminor -parse sourcefile.bminor
```

### 3. Printing

Pretty-prints (reformats) the source file based on the parse tree.

```bash
./bminor -print sourcefile.bminor
```

### 4. Name Resolution & Type Checking

Constructs an Abstract Syntax Tree (AST) and verifies that all names are declared and that no type mismatches exist. BMinor uses strict static typing.

```bash
# Name resolution
./bminor -resolve sourcefile.bminor

# Type checking
./bminor -typecheck sourcefile.bminor
```

### 5. Code Generation

If all prior stages pass, emits an x86 assembly file.

```bash
./bminor -codegen sourcefile.bminor sourcefile.s
```

---

## Producing an Executable

Compile the generated assembly with gcc:

```bash
gcc -g sourcefile.s library.c -o myprogram
```

Run it:

```bash
./myprogram
```

