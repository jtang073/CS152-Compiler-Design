# CS 152 Compiler Design Project
Jason Tang (jtang073)
Spring 2020

# Phase 1: Lexical Analyzer
For this first part of the class project, you will use the flex tool to generate a lexical analyzer for a high-level source code language called "MINI-L". The lexical analyzer should take as input a MINI-L program, parse it, and output the sequence of lexical tokens associated with the program.

# Phase 2: Parser Generation
In this phase of the class project, you will create a parser using the bison tool that will check to see whether the identified sequence of tokens adheres to the specified grammer of MINI-L. The output of your parser will be the list of productions used during the parsing process. If any syntax errors are encountered during parsing, your parser should emit appropriate error messages. Additionally, you will be required to submit the grammar for MINI-: that you will need to write before you can use bison.

**Grammar:**

`program -> functions`

`functions -> function functions | (epsilon)`

`function -> FUNCTION Ident SMICOLON BEGINPARAMS declarations ENDPARAMS BEGINLOCALS declarations ENDLOCALS BEGINBODY statements ENDBODY`

`declarations -> declaration SEMICOLON declarations | (epsilon)`

`declaration -> identifiers COLON INTEGER | identifiers COLON ARRAY L_SWAURE_BRACKET NUMBER R_SQUARE_BRACKET OF INTEGER`

`identifiers -> Ident | Ident COMMA identifiers`

`Ident -> IDENT`

`statements -> statement SEMICOLON statements | statement SEMICOLON`

`statement -> svar | sif | swhile | sdo | sfor | sread | swrite | scontinue | sreturn`

`svar -> var ASSIGN expression`

`sif -> IF bool_expr THEN statements ENDIF`

`swhile -> WHILE bool_expr BEGINLOOP statements ENDLOOP`

`sdo -> DO BEGINLOOP statements ENDLOOP WHILE bool_expr`

`sfor -> FOR var ASSIGN NUMBER SEMICOLON bool_expr SEMICOLON var ASSIGN expression BEGINLOOP statements ENDLOOP`

`varLoop -> COMMA var varLoop | (epsilon)`

`sread -> READ var varLoop`

`swrite -> WRITE var varLoop`

`scontinue -> CONTINUE`

`sreturn -> RETURN expression`

`bool_expr -> relation_exprs | bool_expr OR relation_exprs`

`relation_exprs -> relation_expr | relation_exprs AND relation_expr`

`relation_expr -> NOT ece | ece | TRUE | FALSE | LPAREN bool_expr RPAREN`

`ece -> expression comp expression`

`comp -> EQ | NEQ | LET | GT | LTE | GTE`

`expression -> multi_expr addSubExpr`

`addSubExpr -> ADD expression | SUB expression | (epsilon)`

`multi_expr -> term | term MULT multi_expr | term DIV multi_expr | term MOD multi_expr`

`term -> SUB var | var | SUB NUMBER | NUMBER | LPAREN expression RPAREN| Ident LPAREN expression expressionLoop RPAREN`

`expressionLoop -> COMMA expression expressionLoop | (epsilon)`

`var -> Ident | Ident L_SQUARE_BRACKET expression R_SQUARE_BRACKET L_SQAURE BRACKET expression R_SQUARE_BRACKET | Ident L_SQUARE_BRACKET expression R_SQUARE_BRACKET`

# Phase 3: Code Generation
You will need to modify your bison specification file from the previous phase of the class project so that it no longer outputs the list of productions taken during parsing.

Implement the code generator. This will most likely require some enhancements to your bison specification file. You may also want to create additional implementation files. The requirements for your implementation are as follows.

You do not need to do anything special to handle lexical or syntax errors in this phase of the class project. If any lexical or syntax errors are encountered, your compiler should emit appropriate error message(s) and terminate the same way as was done in previous phases.

You need to check for semantic errors in the inputted MINI-L program. During code generation, if any semantic errors are encountered, then appropriate error messages should be emitted and no other output should be produced (i.e., no code should be generated).

If no semantic errors are encountered, then the appropriate MIL intermediate code should be generated and written to stdout.

When generating the intermediate code, be careful that you do not accidentally create a temporary variable with the same name as one of the variables specified in the original MINI-L program.

Compile everything together into a single executable. The particular commands needed to compile your code generator will depend on the implementation files you create.

Use the mil_run MIL interpreter to test your implementation. For each program written in MINI-L source code, compile it down to MIL code using your implementation. Then invoke the MIL code using mil_run to verify that the compiled program behaves as expected.


[INC] Only works for fibonacci.min file (which was supplied).

**How to compile:**
1. `make`
2. `cat fibonacci.min | ./my_compiler`
3. `./mil_run CODE.mil < AnyFileName.txt`
4. Results will be outputted to the terminal.

This was the result of a full 24hr session right before the due date.
