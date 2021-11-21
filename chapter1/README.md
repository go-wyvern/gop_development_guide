# 词法分析

我们知道编译首先需要构建抽象语法树，如何构建抽象语法树？这里就是聊到词法分析，所谓的词法分析就是将源代码分解为一个个词素（token）的过程。

## token

token 也就是词素，他可以分为特殊类型的Token、基本类型文字的Token、运算符Token和关键字。每个token都有3个重要的属性：首先是token所在的位置，其次是token的类型，最后是token在代码中的文本形式。具体语法定义如下：

```golang
// token
pos token.Pos   // token position
tok token.Token // one token look-ahead
lit string      // token literal
```

特殊类型的Token有错误、文件结束和注释

```golang
// Special tokens
ILLEGAL Token = iota
EOF
COMMENT
```

基本类型面值的Token

```golang
literal_beg
IDENT  // main
INT    // 12345
FLOAT  // 123.45
IMAG   // 123.45i
CHAR   // 'a'
STRING // "abc"
literal_end
```

运算符Token

```golang
operator_beg
// Operators and delimiters
ADD // +
SUB // -
MUL // *
QUO // /
REM // %

AND     // &
OR      // |
XOR     // ^
SHL     // <<
SHR     // >>
AND_NOT // &^

ADD_ASSIGN // +=
SUB_ASSIGN // -=
MUL_ASSIGN // *=
QUO_ASSIGN // /=
REM_ASSIGN // %=

AND_ASSIGN     // &=
OR_ASSIGN      // |=
XOR_ASSIGN     // ^=
SHL_ASSIGN     // <<=
SHR_ASSIGN     // >>=
AND_NOT_ASSIGN // &^=

LAND  // &&
LOR   // ||
ARROW // <-
INC   // ++
DEC   // --

EQL    // ==
LSS    // <
GTR    // >
ASSIGN // =
NOT    // !

NEQ      // !=
LEQ      // <=
GEQ      // >=
DEFINE   // :=
ELLIPSIS // ...

LPAREN // (
LBRACK // [
LBRACE // {
COMMA  // ,
PERIOD // .

RPAREN    // )
RBRACK    // ]
RBRACE    // }
SEMICOLON // ;
COLON     // :
operator_end
```

关键字token

```golang
keyword_beg
// Keywords
BREAK
CASE
CHAN
CONST
CONTINUE

DEFAULT
DEFER
ELSE
FALLTHROUGH
FOR

FUNC
GO
GOTO
IF
IMPORT

INTERFACE
MAP
PACKAGE
RANGE
RETURN

SELECT
STRUCT
SWITCH
TYPE
VAR
keyword_end
```

go+ 还自已定义了几个token

```
RAT      = literal_end  // 123.5r
RARROW   = operator_beg // =>
QUESTION = operator_end // ?
```

## scanner

有了token 的定义，如何将代码解析为表达式，这里就需要扫描器（scanner），扫描源代码文本，scanner会从左到右扫描文本，把文本拆成一些单词。然后，这些单词传入分词器，经过一系列的识别器，确定这些单词的词性，这一过程的产物是token序列。我们举一个例子：

```
3 + (12 - 8)
```

3 也是其中的一个单词, 它实际上是一个常量。分词和所使用的语言种类密切相关，分解后的token序列为 ['3', '+', '(', '12', '-', '8', ')']。在 Go+ 中最终会被解析如下：

```
INT: 5
ADD: +
LPAREN: (
INT: 12
SUB: -
INT: 8
RPAREN: )
```

scanner和分词器所做的工作，构成了编译器的词法分析阶段。具体 scanner 的实现的源码分析会在后面的章节讲解。