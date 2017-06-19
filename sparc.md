https://blol.org/1402-arvorezinha-sparc

btw, this arch is somewhat inedible

```
solaris$ cat arvore.S
.section  ".rodata1"
.align    4
.L0:
        .ascii           "*\0"
.L1:
        .ascii          "\n\0"
 
.L2:
        .ascii          "bla\n\0"
 
        .section        ".text"
        .global         main
main:
        save            %sp,-96,%sp
        mov 0,%g2
 
arewedoneyet:
        cmp %g2,5       ! compare with RFC_MAX of course, no registers needed for this
        be weredonefaggot
 
        mov 0,%g3       ! initialize counter1
 
estrelitas:
        cmp %g3,%g2     ! ah e tal, compara-me a pissa, less or equal?
        ble estrela
 
        set .L1,%o0     ! meter LF no output register, e mandar printar
        call printf
 
        inc %g2         ! increasar o counter2
        ba arewedoneyet
 
estrela:
        set     .L0,%o0 ! printar estrelinha
        call    printf
 
        inc %g3
        ba estrelitas
 
weredonefaggot:
        nop
        restore
 
solaris$ gcc arvore.S -o arvorezinha
solaris$ ./arvorezinha
*
**
***
****
*****
solaris$
```
