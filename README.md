# Assembler
ORG 2500h
LHLD 2504h
XCHG
LHLD 2500h

;pos/neg numbers
mvi A,1b
STA 24FEh; sign of number N1
mvi A,0b
STA 24FFh; numbers have same sign?


;enter numbers
LXI HL,84h
  ;test N1
  lda 24FEh
  
  JNZ neg_n1
  JZ pos_n1
    neg_n1:
    mvi C,1b
    mov A,H
    xra A
    mov H,A
    mov A,L
    xra A
    inr A
    mov L,A
    mvi A,0b
    STA 24FEh
    
    pos_n1:
    
LXI DE,202h
  ;test N2
  lda 24FFh
     JZ different
     JNZ same_sign
     same_sign:
     mov A,C
     JZ pos_n2
     JNZ neg_n2
     different:
     mov A,C
     xra A
     JZ pos_n2
     JNZ neg_n2

     neg_n2:
     mov A,D
     xra A
     mov D,A
     mov A,E
     xra A
     inr A
     mov E,A
     mvi A,1b
     STA 24FFh
     pos_n2:
     mvi A,1b
     STA 24FFh
     
CALL 2560h
ORG 2560h
MVI a,43h


  
HLT

;MVI A,10000000b
;MVI C,0b
;Add C
