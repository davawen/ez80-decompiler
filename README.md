# ez80 Decompiler

This is a quickly made (and pretty blursed) ez80 assembly decompiler.  
It takes in hexadecimal ascii coded bincode (whitespace authorized), and it spits out the corresponding assembly.  
It assumes adl mode is on, which means it only handles 8 bit and  24 bit wide constants.

One of its quirks is that it puts the suffix before the instruction. 
For example: `push.s hl` becomes `52 e5` to which the decompiler gives `.s push hl`.

## Build instructions

There are dependencies beyond a C compiler:
```
$ gcc main.c -o ez80dump
```

## Usage

Feed it bincode through stdin.

```
$ cat file | ./ez80dump
```

Content of `file`: 
```
e1 d1 c1
c5 d5 e5
21 00 00 00
19 09
c9
```

Output:
```
pop  hl
pop  de
pop  bc
push bc
push de
push hl
ld hl, 0x000000
add hl, de
add hl, bc
ret
```

## Sources:

[https://mdfs.net/Docs/Comp/eZ80/OpList](https://mdfs.net/Docs/Comp/eZ80/OpList)
[http://www.zilog.com/docs/um0077.pdf](http://www.zilog.com/docs/um0077.pdf)
