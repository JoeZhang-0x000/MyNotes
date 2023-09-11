习题集[[Byrant, 2003 习题]]
## chapter 1
## chapter 2
### 2.1 Information Storage 
#### 2.1.3 Addressing and Byte Ordering
##### Big endian and Little endian
big endian machines store the most significant byte first, which is similar to human beings.
for example, `0x01234567`
![[Pasted image 20230625160031.png]]
Most Intel-compatible machines operate in **little-endian mode**, while most machines from IBM or Oracle operate in **big-endian mode**. Some recent microprocessor chips are **bi-endian**, means they can either be little-endian mode or big-endian mode.
#### 2.1.9 Shift Operations in C
For an operated $x$ having bit representation $[x_{w-1},x_{w-2},...,x_{0}]$, the C expression `x<<k` yields a value with bit representation $[[x_{w-k-1},x_{w-k-2},...,x_{0},0,...,0]]$. While the expression `x>>k` has two forms of behaviors:
	1. logical. $[0,...,0,x_{w-1},x_{w-2},...,x_{k}]$
	2. Arithmetic.$[x_{w-1},...,x_{w-1},x_{w-1},x_{w-2},...,x_{k}]$
 ![[Pasted image 20230625165207.png]]
 ### 2.2 Integer Representations
 #### 2.2.2 Unsigned Encodings
For vector $[x_{w-1},...,x_1,x_0]$:
$$
B2U_{w(x)}=\sum_{i=0}^{w-1}\limits x_{i}2^i
$$
Range:
The least value: $[0,..,0]$, $UMin_w=0$
The greatest value: $[1,...,1]$, $UMax_{w}=\sum_{i=0}^{w-1}\limits2^i=2^w-1$
 ![[Pasted image 20230626154259.png|200]]
 #### 2.2.3 Two's Complement Encodings
 This method is defined by interpreting **the most significant bit** of the word(called the *signed bit*) to have negative weight.
 For a vector $[x_{w-1},...x_1,x_0]$,
 $$
 B2T_w(x)=-x_{w-1}2^{w-1}+\sum_{i=0}^{w-2}\limits x_i2^i
$$
![[Pasted image 20230626155420.png|300]]
#### 2.2.6 Expanding the Bit Representation of a Number
To convert different integers of **different word size** while retaining the same numeric value.
For converting an unsigned number, we can use *zero extension*:
$u=[u_{w-1},u_{w-2},...,u_0]$,
$u^{`}=[0,..,0,u_{w-1},...,u_0]$,

For converting a tow'2 complement number to a larger data type, we can use *sign extension*:
$u=[u_{w-1},u_{w-2},...,u_0]$,
$u^{`}=[u_{w-1},..,u_{w-1},u_{w-1},...,u_0]$,
#### 2.2.7 Truncating Numbers
For truncating an unsigned number represented by $w$ bits vector $[x_{w-1},...x_0]$ to $k$ bits vector $[x_{k-1},...,x_0]$, then $B2U_{k}(x^{`})=B2U_{w}(x)\mod 2^k$.
![[Pasted image 20230626163343.png]]

For truncating a two's-complement number, then $B2T_{k}(x^{`)}=B2T_{k}(B2T_{w}(x) \mod 2^k)$.
![[Pasted image 20230626164309.png]]

![[Pasted image 20230626164427.png]]
### 2.3 Integer Arithmetic
#### 2.3.1 Unsigned Addition
Unsigned addition can be represented as follow:
$$
x+_w^uy=
\left \{
	\begin{array}{**lr**}
	 x + y, & x + y< 2^w \\
	 x + y - 2^{w}, & x + y \ge 2^w
	\end{array}
\right .
$$
![[Pasted image 20230630095401.png|300]]

**Detecting** overflow of unsigned addition:
For x and y are unsigned integers in the range $0 \le x, y \le UMax_w$, let $s = x +^u_w$ overflows when $s < x$ or $s < y$.

#### 2.3.2 Two's Complement Addition
$$
x+^t_wy=
\left\{
	\begin{array}{*l*}
	 x+y-2^{w},&2^{w-1}\leq x+y & postive overflow \\
	 x+y,&-2^{w-1}\leq x+y <2^{w-1} & Normal \\
	 x+y+2^{w}, & x+y<-2^{w-1} & Negative overflow
	\end{array}
\right.
$$
![[Pasted image 20230630100626.png|300]]

Detecting overflow in two's complement addition:
$TMin_{w}\leq x,y\leq TMax_w$, let $s=x+^t_wy$, then $s$ has
	1. positive overflow, when $x>0,y>0$ but $s\le0$ 
	2. negative overflow, when $x<0,y<0$ but $s\ge0$
#### 2.3.3 Two's Complement  Negation
$$
-^t_{w}=
\left\{
	 \begin{array}{l}
	  TMin_{w},&x=TMin_{w}\\
	  -x,&x>TMin_w
	 \end{array}
\right.
$$
#### 2.3.4 Unsigned Multiplication
$$
x *^u_{w} y=(x\cdot y)\%2^w
$$
#### 2.3.5 Two's complement Multiplication
$$
x *^{u}_{w} y= U2T_{w}((x*y)\%2^{w})
$$
#### 2.3.6 Multiplying by Constants
Historically, many machine perform integer multiplication and division very slowly, usually requiring 10 or more than clock cycles, whereas other operations such as addition, subtraction, bit-level operations, and shifting requires only **1** clock cycle. As a consequence, on important optimization used by complier is to attempt to replace multiplication and division with combinations of shift and addition operations.

$$
x<<k =>x*^{u}_{w}2^{k}
$$
#### 2.3.7 Dividing by power of 2
$$
x>>k=>\lfloor x/2^{k} \rfloor
$$
$$
(x+(1<<k)-1)>>k=>\lceil x/2^{k} \rceil
$$
The C expression:
```c
(x<0 ? x+(1<<k)-1 : x) >> K
```
will compute the value of $x/2^k$.

### 2.4 Floating Point
#### 2.4.1 Fractional Binary Numbers
$$
b = \sum\limits_{i=-n}^{m}2^{i}\times b_{i}
$$
![[Pasted image 20230703152316.png#C|Fractional binary representation.]]
Fractional binary numbers can only represent numbers can be written $x \times 2^{y}$, other values can only be approximated.

#### 2.4.2 IEEE Floating-Point Representation
The IEEE floating-point standard represents a number in a form $V=(-1)^{s} \times M \times 2^E$.
![[Pasted image 20230703152826.png#C|standard floating-point numbers]]
The value encoded by a given bit representation can be divided into three cases:
![[Pasted image 20230703153242.png#C|Categories of single-precision floating-point values.]]
##### case 1: Normalized Values
$E = e - Bias$, where Bias is  as bias value equal to $2^{k-1}-1$(127 for single precision and 1023 for double).
The significand is defined to be $M=1+f$, which is called *implied leading 1 representation*.
As we can view M to be the number with binary representation $1 f_{n-1} f_{n-2} ....$, the leading bit is always equals to 1, so we can take this trick for getting an additional bit of precision for free.

##### case 2: Denormalized Values
When exponent field is **all zeros**, the represented number is in *denormalized form*.
This case serves for **two purposes**:
1. Providing a way to represent numeric value 0.
2. Providing a way to represent numbers that are close to 0.

##### case 3: Special Values
The exponent filed is **all ones**,
1. When the fraction filed is **all zeros**, the resulting values represent **infinity**.
2. When the fraction field is **nonzero**, the resulting value is called a *NaN*, short for 'not a number'.

#### 2.4.3 Example Numbers
![[Pasted image 20230703155059.png#C|Represntable values for 6 bit floating-point format]]

#### 2.4.4 Rounding
##### rounding-to-even(rounding-to-nearest)
Rounding towards even numbers avoids statistical bias in most of real-life situations.
##### rounding-towards-zero
##### rounding-up
##### rounding-down

![[Pasted image 20230704134800.png#C|Illustraion of rounding modes for dollar rounding]]

## chapter 3
### Accessing Information
![[Pasted image 20230707163707.png#C|Integer registers]]
**Summarized** by GPT-3.5:
以下是x86-64架构中常用的寄存器及其大小：

- 通用寄存器（General-purpose Registers）：
    - 64位寄存器：`%rax`、`%rbx`、`%rcx`、`%rdx`、`%rsi`、`%rdi`、`%rbp`、`%rsp`
    - 32位寄存器：`%eax`、`%ebx`、`%ecx`、`%edx`、`%esi`、`%edi`、`%ebp`、`%esp`
    - 16位寄存器：`%ax`、`%bx`、`%cx`、`%dx`、`%si`、`%di`、`%bp`、`%sp`
    - 8位寄存器：`%al`、`%bl`、`%cl`、`%dl`、`%sil`、`%dil`、`%bpl`、`%spl`
- 其他寄存器：
    - 64位指令指针寄存器：`%rip`
    - 64位标志寄存器：`%rflags`
    - 浮点寄存器：`%xmm0` - `%xmm15`、`%xmm16` - `%xmm31`
    - 向量寄存器：`%ymm0` - `%ymm15`、`%ymm16` - `%ymm31`
    - 控制寄存器：`%cr0` - `%cr8`
    - 调试寄存器：`%dr0` - `%dr7`

注意到，通用寄存器中的64位寄存器（如`%rax`、`%rbx`）是8字节（64位），32位寄存器（如`%eax`、`%ebx`）是4字节（32位），16位寄存器（如`%ax`、`%bx`）是2字节（16位），8位寄存器（如`%al`、`%bl`）是1字节（8位）。

所以，不是所有的寄存器都是4字节，寄存器的大小根据其具体的设计和用途而有所不同。

#### 3.4.1 Operand Specifiers
![[Pasted image 20230707152947.png#C|Oprand forms]]
#### 3.4.2 Data Movement Instructions
MOV class:
	![[Pasted image 20230707155104.png#C|Simple data movement instructions]]
Examples:
```x86asm
`movl $0x4050,%eax` (Immediate--Register, 4 bytes)
`movw %bp,%sp` (Register--Register, 2 bytes)
`movb (%rdi,%rcx),%al` (Memory--Register, 1 byte)
`movb $-17,(%esp)` (Immediate--Memory, 1 byte)
`movq %rax,-12(%rbp)` (Register--Memory, 8 bytes)
```

MOVZ class:
	fill out the remaining bytes of the destination with zeros.
	![[Pasted image 20230707161216.png#C|Zero-extending data movement instructions]]
MOVS class:
	fill out the most significant bit of the source operand(the sign).
	![[Pasted image 20230707161244.png#C|Sign-extending data movement instructions.]]
