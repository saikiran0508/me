=OFFSET(
    B3, 
    0, 
    MAX(0, MATCH(TRUE, INDEX(B3:XFD3="",0),0)-13), 
    1, 
    MIN(12, MATCH(TRUE, INDEX(B3:XFD3="",0),0)-1)
)
