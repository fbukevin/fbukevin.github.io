title: ~計組~  MIPS 組語寫平方程式
date: 2011-04-26 01:20:00
tags: [MIPS]
---

因為最近在考試，就只有先PO上完成的程式碼當參考~  

<pre style="background: #FFE7CD; color: black;">#squre(x)  
.text  
.globl main      
main:  
square:  
        la $t0,<span style="color: #7f0055; font-weight: bold;">word</span>  

        la $a0,msg <span style="color: #3f7f59;">#print message for calling for type in</span>  
        li $v0,4  
        syscall  

        li $v0,5 <span style="color: #3f7f59;">#Read_int</span>  
        syscall  
        sw  $v0,0($t0)  

        lw $t2,0($t0)          

<span style="color: #3f7f59;">#不需要用 "li $t1,0" 或 "la $t1,word" 來 initialize $t1</span>  
<span style="color: #3f7f59;">#如果用 "la $t3,word",則運算元內容將會變成 address 而不是 value</span>  

Loop:  
        beq $t1,$t2,<span style="color: #7f0055; font-weight: bold;">EXIT</span> <span style="color: #3f7f59;">#$t1 is count, $t3 is sum, if i==x, than branch to EXIT</span>  
        <span style="color: #7f0055; font-weight: bold;">add</span> $t3,$t3,$t2 <span style="color: #3f7f59;">#j=j+x</span>  
        addi $t1,$t1,1 <span style="color: #3f7f59;">#increment i</span>  
        sw $t3,4($t0)  

        j Loop          
<span style="color: #7f0055; font-weight: bold;">EXIT</span>:  

        la $a0,ans <span style="color: #3f7f59;">#print message of result prompt</span>  
        li $v0,4  
        syscall  

        lw $t4,4($t0) <span style="color: #3f7f59;">#print the answer</span>   
        li $v0,1  
        <span style="color: #7f0055; font-weight: bold;">move</span> $a0,$t4  
        syscall  

.<span style="color: #7f0055; font-weight: bold;">data</span>  
    msg:    .asciiz <span style="color: #2a00ff;">"請輸入一個數字："</span>  
    <span style="color: #7f0055; font-weight: bold;">word</span>: .<span style="color: #7f0055; font-weight: bold;">word</span> 0,0  
    ans: .asciiz <span style="color: #2a00ff;">"平方的結果是："</span>  

#Finished by Veck Hsiao  
</pre>

[閱讀更多 »](http://veckcode.blogspot.com/2011/04/asm-mips.html#more)