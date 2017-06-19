original in Portuguese: 
https://blol.org/1407-arvorezinha-hp-precision-architecture-aka-pa-risc-aka-demonio

this is an internationalized version cause like idk apparently not everyone speaks portuguese for some reason

```
hpux$ cat arvorezinha.S
	.LEVEL 1.1						; gay stuff for HPUX
	.SPACE $PRIVATE$					; HPPA has a thing called spaces, read the arch book
	.SUBSPA $DATA$,QUAD=1,ALIGN=8,ACCESS=31			; for further info on this or early schizophrenia
	.SUBSPA $BSS$,QUAD=1,ALIGN=8,ACCESS=31,ZERO,SORT=82
	.SPACE $TEXT$
	.SUBSPA $LIT$,QUAD=0,ALIGN=8,ACCESS=44
	.SUBSPA $CODE$,QUAD=0,ALIGN=8,ACCESS=44,CODE_ONLY
	.IMPORT $global$,DATA
	.IMPORT $$dyncall,MILLICODE
	.IMPORT write,CODE					; it is nice to do imports
	.IMPORT exit,CODE
	.IMPORT __main,CODE
	.SPACE $TEXT$
	.SUBSPA $LIT$
 
	.align 4
STAR
	.STRING "\x2a\x00"
LF
	.STRING "\x0a\x00"
	.SPACE $TEXT$
	.SUBSPA $CODE$
 
	.align 4
	.NSUBSPA $CODE$,QUAD=0,ALIGN=8,ACCESS=44,CODE_ONLY
	.EXPORT main,ENTRY,PRIV_LEV=3,RTNVAL=GR			; the privilege levels is funny
main
	.PROC
	.CALLINFO FRAME=64,CALLS,SAVE_RP,SAVE_SP,ENTRY_GR=3
	.ENTRY
	.CALL
	xor     %r4,%r4,%r4					; aka set %r4 to zero :)
 
arewedoneyet
	comib,=,n 5,%r4,kk10xbai				; if %r4 is 5, BAI NAO!
	nop
	xor     %r3,%r3,%r3					; initialize counter for 2nd loop
 
letsdothis
	comb,<=,n %r3,%r4,estrela				; if %r3 is less or equal to %r4
	xor %r1,%r1,%r26					; yes, this is a nop
 
	ldi 1,%r26						; choose the fd (1 is stdout)
	ldil LR'LF,%r19						; copy string in
	ldo RR'LF(%r19),%r25					; a sissy way
	ldi 1,%r24						; length of stringue
	.CALL ARGW0=GR,ARGW1=GR,ARGW2=GR
	bl write,%r2
	xor %r1,%r2,%r3						; yes, this is a nop
 
	addi    1,%r4,%r4					; increment %r4
	b       arewedoneyet
	shladd %r4,2,%r8,%r15					; yes, this is a nop
 
estrela
	ldi 1,%r26						; see the other write
	ldil LR'STAR,%r19					; same shit going on
	ldo RR'STAR(%r19),%r25
	ldi 1,%r24
	.CALL ARGW0=GR,ARGW1=GR,ARGW2=GR
	bl write,%r2
	add %r13,%r14,%r15					; yes, this is a nop
 
	addi    1,%r3,%r3
	b       letsdothis
	nop							; guess what...
 
kk10xbai
	ldi 0,%r26
	.CALL ARGW0=GR
	bl exit,%r2
	shrpw %r8,%r7,8,%r9					; nop nop nop
	subi,OD  42,%r3,%r12					; nop nop nop nopppppp! :D
	.EXIT
	.PROCEND
hpux$ gcc arvorezinha.S && ./a.out
*
**
***
****
*****
hpux$
```
