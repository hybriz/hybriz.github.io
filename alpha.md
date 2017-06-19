original in Portuguese:
https://blol.org/1396-arvorezinha-melhor-arquitectura-do-mundo-alpha
https://web.archive.org/web/20110812180220/https://blol.org/1396-arvorezinha-melhor-arquitectura-do-mundo-alpha

this is an internationalized version cause like idk apparently not everyone speaks portuguese for some reason

```
tru64> gcc arvore.S -o arvorezinha
tru64> ./arvorezinha
*
**
***
****
*****
tru64> cat arvore.S
.data
LF:             .ascii          "\n\0"
GAY:            .ascii          "*"
 
.text
        .align  4
        .set    noreorder
        .arch   ev4
        .globl  main
        .ent    main
 
main:
        ldgp    $gp,0($27)			# load that global pointer
        stq     $26,0($sp)			# initialize? the stack pointer (just in case right)
 
        lda $10,5				# RFC_MAX for main loop
        lda $9,0				# counter for loop1
 
loop1:
        cmpeq $9,$10,$7				# if $9 equals $10, branch to end
        bne $7,final
 
        lda $11,0				# counter for loop2
 
loop2:
        cmple $11,$9,$7				# if $11 less or equal to $9, star it!
        bne $7,estrela
 
        lda $16,LF				# new line pl0x
        jsr $26,printf
        ldgp $gp,0($26)
 
        lda $9,1($9)				# a gay way to increment
        br loop1
 
estrela:
        lda     $16,GAY				# print the little star...
        jsr     $26,printf			# one always needs to reset $gp
        ldgp    $gp,0($26)			# after using a function
 
        addq $11,1,$11				# another gay way to increment :p
        br loop2
 
final:
        mov     $31,$0				# return = 0
        ldq     $26,0($sp)			# cleanup stack, though we didn't use it but oh well..
        ret     $31,($26),1			# returnarrrrrrrrr
        .end    main
 
tru64>
```
