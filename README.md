# Pwnable

* GCC command - Compiles binary via vulnerable configuration
```
gcc -z execstack -no-pie -w -o stack0 stack0.c
```

* PEDA installation
```
git clone https://github.com/longld/peda.git ~/peda
echo "source ~/peda/peda.py" >> ~/.gdbinit
echo "DONE! debug your program with gdb and enjoy"
```

* Pwntool document
```
http://docs.pwntools.com/en/stable/intro.html
```

* Turns off ASLR in Kali
```
echo 0 | sudo tee /proc/sys/kernel/randomize_va_space
```
