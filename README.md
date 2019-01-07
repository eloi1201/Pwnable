# Pwnable

* GCC command - Compiles binary via vulnerable configuration
```
gcc -z execstack -no-pie -w -o stack0 stack0.c: 
```

* PEDA installation
```
git clone https://github.com/longld/peda.git ~/peda
echo "source ~/peda/peda.py" >> ~/.gdbinit
echo "DONE! debug your program with gdb and enjoy"
```
