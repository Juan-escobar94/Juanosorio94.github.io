---
title: Compilers introduction 
date: "2021-02-06T21:44:24.950Z"
description: "Post about what I learn while studying compiler construction lecture at TU Dresden"
categories: [code]
comments: true
---




## The Goal of the Compiler

The goal of a compiler is just to take a source code as an input and translate it into
a target machine code (e.g. x86 Assembly), which is not even yet the object code that 
gets executed on the cpu. After compiling, the assembler and the linker take care of 
that task.

## Compiler phases

In order to achieve its goal, compilers have been designed into phases, One great benefit
about doing this is that we get a lot of modularity. We can create new compilers
by interchanging reusable modules.


### Phase 1: Lexical Analysis

the first phase when a program is fed to a compiler is
analysing the stream of characters and groupping them 
into meaningful sequences called lexemes. 

for each of the lexemes, the lexical analyzer produces tokens as
outputs (passed further down to the next step: syntax analysis),
roupping them as (token name, attribute value), where the
token name is an abstract symbol that is used during syntax analysis,
the attribute value points to an entry in the symbol table for this
token. Information from the symbol table entry is needed for semantic
analysis and code generation.

Some tokens do not need attribute values to identify them inside
the symbol table, e.g. the equals sign in an assignment. the variable,
however, could produce something like (id, 2), the equals sign (=, \_)

### Syntax Analysis

The syntax analysis, also known as parsing, is the second phase of the
compiler in which it uses the output from the first phase (tokens)
to create a tree like intermediate representation that corresponds to 
the grammatical structure of the token stream. 


### Semantic Analysis

The semantic analyzer takes the output from the previous step and also
the information from the symbol table (this is present in all steps), 
and checks against the language definition for semantic consistency.

Type information is also gathered and stored inside the symbol table
or inside the syntax tree. Type checking is also part of the semantic
analysis, where the compiler checks that each operator has matching 
operands.

### Intermediate Code Generation

### Code Optimization

### Code Generation 


## Symbol Table Management

The compiler records variable names found in the source program and
collects information about various attributes of each name -for instance,
information about the allocated storeage for a name, its type, scope,
and in case of procedures, number and types of arguments, the method of 
passing the arguments, and the type returned.

## Compiler Construction Tools

1. Parser generators: produce syntax analyzers from a 
grammatical description of a language.
2. Scanner generators: produce lexical analyzers from a regular-expression
description of the tokens of a language.
3. Syntax-directed translation engines: produce a collection of routines
for walking a parse tree and generating intermediate code.
4. Code-generators generators: produce code generators from a collection
of rules for translating each operation of the intermediate language into
the the machine language for a target machine.
5. Data-flow analysis engines: facilitate the gathering of information
about how values are transmitted from one part of a program to each other
part. Data-flow analysis is a key part of code optimization.
6. Compiler-construction toolkits that provide an integrated set of 
routines for constructing various phases of a compiler.



## Context Free Grammars

Used to specify the syntax of a language, a context free grammar has four
components:

1. A set of terminal symbols, also referred as tokens, they are the
elementary symbols of the language defined by the grammar.
2. A set of nonterminals, sometimes called "syntactic variables",
each nonterminal represents a set of string of terminals.
3. A set of productions, where each one consists of a nonterminal, called
the head or left side of the production, an arrow and a sequence of
terminals and/or nonterminals, called the body or right side of the
production
4. A designation of one of the nonterminals as the start symbol.


## Parsing

Parsing is the problem of taking a string of terminals and figuring out how
to derive it from the start symbol of the grammar and if it cannot be 
derived from the start symbol of the grammar, then reporting syntax errors
within the string.

## Ambiguity

A grammar can have more than one parsing tree generating a given string of 
terminals, such a grammar is said to be ambiguous. To show that a grammar
is ambiguous, it suffices to find a terminal string that can yield more than
one parsing tree.

## Associtivity of operators

When an operand in a mathematical expression sits in the middle, e.g. 5 in 
4 - 5 + 6, we need to stick to a convention to help us decide the outcome
of the math expression. In most programming languages, the four common
mathematical operators are *left associative* meaning that an operand within
to plus signs for example belongs to the operator on the left.

Operators like exponentiation are right associative, as well as the the 
assignment operator we see in languages like C.

Parse trees for left associative grammars grow (nest) towards the left,
while in right associative grammars, they grow (nest) towards the right.

a great hint is given, by which which of the non terminal symbols can be
expanded (most likely in some kind of a recursive fashion) for a given 
production. If its the one on the right, there is a high likelihood it is
a right associative grammar.

Operators can also have precedence. We say an operator has higher precendence
than another operator if it takes it operands before the one with the lower
precedence does (* takes for example its operands before + does).


excerpt from book about grammars that implement precedence level:
We can generalize this idea to any number of n precedence levels.
We need n+1 nonterminals. The first (highest precedence) can never be torn
apart. Typically, the production bodies for this nonterminal are only single
operands and parenthesized expressions.


## Syntax directed translation

Syntax directed translation is done by attaching rules or program fragments
to productions in a grammar. 
