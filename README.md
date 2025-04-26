.data
arr:    .word 5, 4, 3, 2, 1

.text
.globl main

main:
    la $a0, arr
    li $t0, 0
    li $t1, 4
    li $s0, 0

outer_loop:
    bge $t0, $t1, end

    li $t2, 0
    la $a1, arr

inner_loop:
    sub $t3, $t1, $t0
    bgt $t2, $t3, next_pass

    lw $t4, 0($a1)
    lw $t5, 4($a1)

    bge $t4, $t5, skip

    sw $t5, 0($a1)
    sw $t4, 4($a1)
    addi $s0, $s0, 1

skip:
    addi $a1, $a1, 4
    addi $t2, $t2, 1
    j inner_loop

next_pass:
    addi $t0, $t0, 1
    j outer_loop

end:
    j end
