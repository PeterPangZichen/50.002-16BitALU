# 50.002-16BitALU

## Input and Ouput Terminal
#### INPUT: 
SWITCH[2] ALUFN[6] INPUT[16]
#### OUTPUT: 
OUTPUT[16] → LED[16]

## Functions
#### Add16
-	ADD: out = a + b
-	SUB: out = a + b^16x{0}
-	MUL: out = a * b. 
Note that MUL will produce a number up to 32 bits. Use out[16] will only take the lowest 16 bits

#### Bool16
-	AND: out = a & b
-	OR: out = a | b
-	XOR: out = a ^ b
-	“A”: out = a

#### Comp16
-	CMPEQ: out = z
-	CMPLT: out = n^v
-	CMPLE: out = z|n^v

#### Shift16:
-	SHL: ..
-	SHR: ..
-	SAR: ..


## Manual Test: 

### Manual Test FSM:
#### State 1:
	SWITCH[1:0] = 00. Put binary number A in INPUT[16]. The value of A will be stored in a DFF.
#### State 2: INPUTB 10
	SWITCH[1:0] = 10. Put binary number B in INPUT[16]. The value of B will be stored in a DFF.
#### State 3: OUTPUT 11
	SWITCH[1:0] = 11. The value of A and B will be calculated by ALU due to different ALUFN, then the output will be reflected in io_led[1:0].

## Auto Test: 
ADD, SUB, MUL, AND, OR, XOR, LDR, CMPEQ, CMPLT, CMPLE, SHL, SHR, SRA, ADDERROR, BOOLERROR, COMPERROR, SHIFTERROR, PASS

### Auto Test FSM:
#### States: 
In each state, values of A and B will be automatically selected and the output will be reflected on io_led[2][7:3]. It has 5 final states.
#### Final State 1: PASS
	OUTPUT = 10000
#### Final State 2: ADDERROR
	OUTPUT = 01000
#### Final State 3: BOOLERROR
	OUTPUT = 00100
#### Final State 4: COMPERROR
	OUTPUT = 00010
#### Final State 5: SHIFTERROR
	OUTPUT = 00001
