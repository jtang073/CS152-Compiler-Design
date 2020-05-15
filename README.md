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
**TBD**
