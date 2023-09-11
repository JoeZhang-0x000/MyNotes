# chapter 3
## 3.1
0x100
0x108
0x103
0xff
0xab
(0x100+0x003+0x009) = (0x10C), 0x11
260 = 0x104, %rcx = 0x1, %rdx = 0x3, M[0x104+0x1+0x3] = M[0x108] = 0x13
%rcx = 0x1, M[0xfc+0x1 * 4] = M[0xfc+0x4] = M[0x100] = 0xff

## 3.2

|source | destination | instruction|
|-|-|-|
|32b|memory|`movl %eax,(%rsp)`|
|memory|16b|`movw (%rax),%dx`|
|immediate|8b|`movb $0xff,%bl$`|
|memory|8b|`movb %(rsp,%rdx,4),%dl`|
|memory|64b|`movq %(rdx),%rax`|
|16b|memory|`movw %dx,(%rax)`|

## 3.3
1. ? | can not use %ebx as address register
2. -> movq
3. ? | can not have both source and destination be memory reference
4. -> movw | no register named %sl
5. can not move value from a register to immediate value
6. -> movw
7. -> movq

