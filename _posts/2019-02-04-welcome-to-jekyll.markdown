---
layout: post
title:  "Weird Programming Languages That You May Have Not Heard"
categories: [ Jekyll ]
image: https://hashnode.imgix.net/res/hashnode/image/upload/v1557209053906/hbB7JDlHy.jpeg?w=1600&h=840&fit=crop&crop=entropy&auto=format,enhance&q=60
---

There are thousands of programming languages are invented and only about hundred of programming languages are commonly used to build software. Among this thousands of programming languages, there are some weird type of programming languages can be also found. These programming languages are seems to be called weird, since their programming syntax and the way it represent its code. In this blog we will look into some of these language syntax.

## Legit

![hello.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1556948608996/c7g-29oC3.png)

Have you ever wonder, when you come to a Github project that print hello world program, but you cannot see any codes or any content. Check this link [https://github.com/blinry/legit-hello](https://github.com/blinry/legit-hello) and you will see nothing in this repository. But trust me, there is hidden code in this project.

If you see the [commit](https://github.com/blinry/legit-hello/commits/master) section, you can reveal the magic. Yeah, you are right. Its storing hello world code in inside the git commit history. If you clone this project and run the following command, then you can see the hidden code in this project.

```
 git log --graph --oneline
```
Here are the supported instructions.

- "[<tag>]": jump to the specified Git tag. For example, [loop] will jump to the tag loop.
- "quit": stop the program.
- "get": read a char from standard input and place its ASCII value on the stack. On EOF, push a 0.
- "put:' pop top stack value and write it to standard output as a char. The value is always truncated to an unsigned byte.
- "<Number>": push the specified integer on the stack. For example, 42 will push the value 42.
- "<Letters>": unescape string, then push the individual ASCII characters on the stack. For example, "Hi\n" will push the numbers 72, 105, and 10.
- "dup": duplicate top stack value
- "pop": pop top stack value and discard it
- "add": pop two topmost stack values, add them, push result on the stack
- "sub": pop two topmost stack values, subtract top one from bottom one, push result on the stack
- "cmp": pop two topmost stack values, pushes 1 if bottommost one is larger, 0 otherwise
- "read": place value of current tape cell on the stack
- "write": pop top stack value and write it to the current tape cell
- "left": pop top stack value, move tape head left for that many places
- "right": pop top stack value, move tape head right for that many places

Legit programming language source code hosted in [Github](https://github.com/blinry/legit) and you can tryout yourself. Read out more about [Legit](https://morr.cc/legit/).

## Folder

![1548px-PureFolders_HelloWorld.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1556948661388/ZKbrI1C4H.png)

Here's another one, which does not maintain any code inside its repository. This language keep its code as folders. Instructions are read according to the oder of the folders. Inside these folder, there are three folders to represent Type, Command and Expression. Number of folders in inside these folders represent relevant mapping with type, command or expression. It can be represented as follows.

| Command | # of Folder | Details |
| --- | --- | --- |
| if | 0 folder | Second sub-folder holds expression, third holds list of commands |
| while | 1 folder | Second sub-folder holds expression, third holds list of commands |
| declare | 2 folders | Second sub-folder holds type, third holds var name (in number of folders) |
| let | 3 folders | Second holds var name (in number of folders), third holds expression |
| print | 4 folders | 	Second sub-folder holds expression |
| input | 5 folders | 	Second sub-folder holds var name |

Read full description of this language in [here](https://esolangs.org/wiki/Folders)

## Befunge

This is another interesting programming language which represent its code in two dimensional space. Take a look following code of infinite loop.
```
>v
^<
```
Did you get that? Execution start with first line ">" character. It mean to execute next instruction in right side. right side instruction is "v". This means to execute down instruction. This continues as an infinite loop. Here I added some of its instructions.

- "+" Addition: Pop two values a and b, then push the result of a+b
- "-"	Subtraction: Pop two values a and b, then push the result of b-a
- "**" Multiplication: Pop two values a and b, then push the result of a*b
- "/"	Integer division: Pop two values a and b, then push the result of b/a, rounded down. According to the specifications, if a is zero, ask the user what result they want.
- "%"	Modulo: Pop two values a and b, then push the remainder of the integer division of b/a.
- "!"	Logical NOT: Pop a value. If the value is zero, push 1; otherwise, push zero.
- "`"	Greater than: Pop two values a and b, then push 1 if b>a, otherwise zero.
- ">" PC direction right
- "<" PC direction left
- "^"	PC direction up
- "v"	PC direction down
- "?"	Random PC direction
- "_"	Horizontal IF: pop a value; set direction to right if value=0, set to left otherwise

Read complete language specifications [here](https://esolangs.org/wiki/Befunge). 3D represented languages also built called "Suzy" based on this language. Here below an example of finding factorial with Befunge language
```
&>:1-:v v *_$.@ 
 ^    _$>\:^
```
## Brainfuck

This language was invented in 1993, as an attempt to create the smallest possible compiler. This compiler allow eight commands to write program and operate based on memory cell which also known as tapes. Here is the list of command Brainfuck support.

- ">" Move the pointer to the right
- "<" Move the pointer to the left
- "+" Increment the memory cell under the pointer
- "-"	Decrement the memory cell under the pointer
- "."	Output the character signified by the cell at the pointer
- ","	Input a character and store it in the cell at the pointer
- "["	Jump past the matching ] if the cell under the pointer is 0
- "]"	Jump back to the matching [ if the cell under the pointer is nonzero

Here below how hello world application implemented in Brainfuck language.
```
 1 +++++ +++               Set Cell #0 to 8
 2 [
 3     >++++               Add 4 to Cell #1; this will always set Cell #1 to 4
 4     [                   as the cell will be cleared by the loop
 5         >++             Add 4*2 to Cell #2
 6         >+++            Add 4*3 to Cell #3
 7         >+++            Add 4*3 to Cell #4
 8         >+              Add 4 to Cell #5
 9         <<<<-           Decrement the loop counter in Cell #1
10     ]                   Loop till Cell #1 is zero
11     >+                  Add 1 to Cell #2
12     >+                  Add 1 to Cell #3
13     >-                  Subtract 1 from Cell #4
14     >>+                 Add 1 to Cell #6
15     [<]                 Move back to the first zero cell you find; this will
16                         be Cell #1 which was cleared by the previous loop
17     <-                  Decrement the loop Counter in Cell #0
18 ]                       Loop till Cell #0 is zero
19 
20 The result of this is:
21 Cell No :   0   1   2   3   4   5   6
22 Contents:   0   0  72 104  88  32   8
23 Pointer :   ^
24 
25 >>.                     Cell #2 has value 72 which is 'H'
26 >---.                   Subtract 3 from Cell #3 to get 101 which is 'e'
27 +++++ ++..+++.          Likewise for 'llo' from Cell #3
28 >>.                     Cell #5 is 32 for the space
29 <-.                     Subtract 1 from Cell #4 for 87 to give a 'W'
30 <.                      Cell #3 was set to 'o' from the end of 'Hello'
31 +++.----- -.----- ---.  Cell #3 for 'rl' and 'd'
32 >>+.                    Add 1 to Cell #5 gives us an exclamation point
33 >++.                    And finally a newline from Cell #6
```

This can be represented in one line as follows.
```
++++++++[>++++[>++>+++>+++>+<<<<-]>+>+>->>+[<]<-]>>.>---.+++++++..+++.>>.<-.<.+++.------.--------.>>+.>++.
```

## Piet


![piet.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1556963788616/t_X2tQcHq.jpeg)

As you see it, It is programming language, that programmer need to color a grid instead of coding words. Pointer used to move around the bitmap image and execute command relevant to each color code. There are twenty colors used to represent command and white color does not represent any operation. when the pointer tries to enter a black region, the rules of choosing the next block are changed instead. Here below the sample program to print "Piet".

![Piet_Program.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1556964190433/eneEasY2X.gif)

## Malbolge
One last programming language! This is known as "Programming from hell". The idea of this language is that programming should be hard. Therefore there is no point of discussing language syntax in this blog. Interesting fact of this language is that, even the inventor of this language was not even write a program by him self. However, Here an example program of hello world in Malbolge language.
```
 (=<`#9]~6ZY32Vx/4Rs+0No-&Jk)"Fh}|Bcy?`=*z]Kw%oG4UUS0/@-ejc(:'8dc
```

## Conclusion

I am not going to discuss all the programming languages here, since there are lot of it. I have list down below multiple programming languages that I have found for further reading. Interesting fact about most of these languages was these  are Turing complete. Which mean, you can implement any computer program that other programming languages can do. Even though these programming languages are seems useless, it open our mind to look things we seen to see differently.

Hope you enjoy reading this article. If you have any comment, [this](https://twitter.com/Dhanushkamadus2) is my tweet account. Follow me for more interesting stories. Feel free to comment down your thoughts. See you in another article. Cheers :)

- [Charcoal](https://github.com/somebody1234/Charcoal)
- [Chef](http://www.dangermouse.net/esoteric/chef.html)
- [Chicken](https://esolangs.org/wiki/Chicken)
- [Dots](https://github.com/josconno/dots)
- [Ook](http://www.dangermouse.net/esoteric/ook.html)
- [Suzy](https://github.com/gvx/suzy) 
