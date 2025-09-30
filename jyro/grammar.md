---
layout: default
title: Formal Grammar
parent: Jyro
has_children: false
has_toc: false
permalink: /jyro/grammar/
nav_order: 140
---

```antlr
grammar Jyro;

// -----------------------
// Parser rules
// -----------------------

program
    : statement* EOF
    ;

// ---- Statements ----
statement
    : variableDecl
    | ifStmt
    | switchStmt
    | whileStmt
    | forEachStmt
    | returnStmt
    | breakStmt
    | continueStmt
    | incDecStmt                  // e.g., x++  or  a.b[i]--
    | exprStmt                    // any expression (incl. assignment, call, literals)
    ;

variableDecl
    : VAR Identifier (COLON typeName)? (ASSIGN expression)?
    ;

typeName
    : NUMBER_T
    | STRING_T
    | BOOLEAN_T
    | OBJECT_T
    | ARRAY_T
    ;

exprStmt
    : expression
    ;

incDecStmt
    : assignmentTarget (INCR | DECR)
    ;

// ---- Control Flow ----
ifStmt
    : IF expression THEN statement*
      (ELSE IF expression THEN statement*)*
      (ELSE statement*)?
      END
    ;

switchStmt
    : SWITCH expression DO
        (CASE expression THEN statement*)*
        (DEFAULT statement*)?
      END
    ;

whileStmt
    : WHILE expression DO statement* END
    ;

forEachStmt
    : FOREACH Identifier IN expression DO statement* END
    ;

returnStmt
    : RETURN
    ;

breakStmt
    : BREAK
    ;

continueStmt
    : CONTINUE
    ;

// ---- Expressions (C#-style precedence) ----
// Lowest to highest:
// assignment (right-assoc) < conditional ?: (right-assoc) < or < and < equality < relational < additive < multiplicative < unary < postfix/primary

expression
    : assignmentExpr
    ;

assignmentExpr
    : conditionalExpr                                     #AssignPass
    | assignmentTarget ASSIGN assignmentExpr              #AssignMake
    ;

assignmentTarget
    : Identifier (memberOrIndex)*
    ;

conditionalExpr
    : logicalOrExpr (QMARK conditionalExpr COLON conditionalExpr)?
    ;

logicalOrExpr
    : logicalAndExpr (OR logicalAndExpr)*
    ;

logicalAndExpr
    : equalityExpr (AND equalityExpr)*
    ;

equalityExpr
    : relationalExpr ((EQ | NEQ) relationalExpr)*
    ;

relationalExpr
    : additiveExpr ((LT | LE | GT | GE | IS) additiveExpr)*
    ;

additiveExpr
    : multiplicativeExpr ((ADD | SUB) multiplicativeExpr)*
    ;

multiplicativeExpr
    : unaryExpr ((MUL | DIV | MOD) unaryExpr)*
    ;

unaryExpr
    : (NOT | SUB) unaryExpr
    | postfixExpr
    ;

postfixExpr
    : primaryExpr (postfixSuffix)*
    ;

postfixSuffix
    : LPAREN argList? RPAREN
    | memberOrIndex
    ;

memberOrIndex
    : DOT Identifier
    | LBRACK expression RBRACK
    ;

// ---- Primaries & literals ----
primaryExpr
    : literal
    | Identifier
    | LPAREN expression RPAREN
    | objectLiteral
    | arrayLiteral
    ;

literal
    : numberLiteral
    | stringLiteral
    | TRUE
    | FALSE
    | NULL
    ;

numberLiteral
    : Number
    ;

stringLiteral
    : String
    ;

objectLiteral
    : LBRACE (objectEntry (COMMA objectEntry)*)? RBRACE
    ;

objectEntry
    : (String | LBRACK expression RBRACK) COLON expression
    ;

arrayLiteral
    : LBRACK (expression (COMMA expression)*)? RBRACK
    ;

argList
    : expression (COMMA expression)*
    ;

// -----------------------
// Lexer rules (keywords first)
// -----------------------

// Keywords / operators (case-sensitive)
VAR        : 'var';
IF         : 'if';
THEN       : 'then';
ELSE       : 'else';
END        : 'end';
SWITCH     : 'switch';
DO         : 'do';
CASE       : 'case';
DEFAULT    : 'default';
WHILE      : 'while';
FOREACH    : 'foreach';
IN         : 'in';
RETURN     : 'return';
BREAK      : 'break';
CONTINUE   : 'continue';

TRUE       : 'true';
FALSE      : 'false';
NULL       : 'null';

AND        : 'and';
OR         : 'or';
NOT        : 'not';
IS         : 'is';

// Types
NUMBER_T   : 'number';
STRING_T   : 'string';
BOOLEAN_T  : 'boolean';
OBJECT_T   : 'object';
ARRAY_T    : 'array';

// Punctuation / operators
INCR       : '++';
DECR       : '--';
EQ         : '==';
NEQ        : '!=';
LE         : '<=';
GE         : '>=';
LT         : '<';
GT         : '>';
ADD        : '+';
SUB        : '-';
MUL        : '*';
DIV        : '/';
MOD        : '%';

ASSIGN     : '=';
QMARK      : '?';
COLON      : ':';
COMMA      : ',';
DOT        : '.';
LPAREN     : '(';
RPAREN     : ')';
LBRACE     : '{';
RBRACE     : '}';
LBRACK     : '[';
RBRACK     : ']';

// Identifiers
Identifier : Letter (Letter | Digit | '_')* ;

// Numbers: integers and decimals (no exponent for now; easy to extend)
Number     : Digit+ ('.' Digit+)? ;

// Strings: double-quoted, with standard escapes; no raw multi-line strings
String
    : '"' ( EscapeSeq | ~["\\\r\n] )* '"'
    ;

fragment EscapeSeq
    : '\\' [btnfr"\\/]          // \b \t \n \f \r \" \\ \/
    | '\\' 'u' Hex Hex Hex Hex  // \uXXXX
    ;

fragment Letter : [A-Za-z] ;
fragment Digit  : [0-9] ;
fragment Hex    : [0-9A-Fa-f] ;

// Whitespace & comments (insignificant)
// Newline terminates a comment; comments are skipped.
WS       : [ \t\r\n]+ -> skip ;
COMMENT  : '#' ~[\r\n]* -> skip ;
```