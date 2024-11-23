# Ex.No:3
   RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
## Register Number: 212222040146
## Date:
## AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
## PROGRAM

```
/* program name is ex.l */
%{
/* program to recognize a C program */ int COMMENT = 0;
%}

identifier [a-zA-Z][a-zA-Z0-9]*

%%
#.* { printf("\n%s is a PREPROCESSOR DIRECTIVE", yytext); } 
int|float|char|double|while|for|do|if|break|continue|void|switch|case|long|struct|const|typedef|return|else|goto { printf("\n\t%s is a KEYWORD", yytext); }
"/*" { COMMENT = 1; }
"*/" { COMMENT = 0; }
{identifier}\( { if (!COMMENT) printf("\n\nFUNCTION\n\t%s", yytext); }
\{ { if (!COMMENT) printf("\n BLOCK BEGINS"); }
\} { if (!COMMENT) printf("\n BLOCK ENDS"); }
{identifier}(\[[0-9]*\])? { if (!COMMENT) printf("\n %s IDENTIFIER", yytext); }
\".*\" { if (!COMMENT) printf("\n\t%s is a STRING", yytext); }
[0-9]+ { if (!COMMENT) printf("\n\t%s is a NUMBER", yytext); }
\)(\;)? { if (!COMMENT) printf("\n\t"); ECHO; printf("\n"); }
\( ECHO;
= { if (!COMMENT) printf("\n\t%s is an ASSIGNMENT OPERATOR", yytext); }
\<=|\>=|\<|==|\> { if (!COMMENT) printf("\n\t%s is a RELATIONAL OPERATOR", yytext); }
%%

int main(int argc, char **argv) { if (argc > 1) {
FILE *file;
file = fopen(argv[1], "r"); if (!file) {
printf("could not open %s \n", argv[1]); exit(0);
}
yyin = file;
}
yylex(); printf("\n\n"); return 0;
}
int yywrap() { return 0;
}

```

## OUTPUT

![377374996-ccfee339-5608-4a1c-9728-f35454dc432a](https://github.com/user-attachments/assets/8fb11c55-b7c8-40f1-b9c5-9ee52fd3efcb)


## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
