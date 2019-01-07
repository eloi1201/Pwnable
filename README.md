# Pwnable

* GCC command

  * gcc -z execstack -no-pie -w -o stack0 stack0.c: Compiles binary via vulnerable configuration

* PEDA installation
  * https://github.com/longld/peda
  ```
  git clone https://github.com/longld/peda.git ~/peda
  echo "source ~/peda/peda.py" >> ~/.gdbinit
  echo "DONE! debug your program with gdb and enjoy"
  ```
