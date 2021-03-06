---
title: Assembly Statement
parent: Statements.md
---

## Syntax

```
asm_stmt ::= 'asm'(string+                                                    ')' ';'
           | 'asm'(string+ ':' ('string',)*'                                  ')' ';'
           | 'asm'(string+ ':' ('string',)*' :' ('string',)*'                 ')' ';'
           | 'asm'(string+ ':' ('string',)*' :' ('string',)* ':' ('string',)* ')' ';'
```

## Typing

## Semantics

## Examples

``` rust
extern "C" {
    fn println(&[u8]) -> ();
}

fn main() -> int {
    let mut dst = "Don't overwrite me";
    let src = "Come on, copy me!\n";
    strcpy(&mut dst, src, 19u32);

    println(dst);
    0
}

fn strcpy(mut dst: &[u8], mut src: &[u8], mut count: u32) -> () {
    asm("cld\n\t"
        "rep movsb"
        : "={si}"(src), "={di}"(dst), "={cx}"(count)
        : "0"(src), "1"(dst), "2"(count)
        : "memory"
    );
}
```
