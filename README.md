# Makefiles

## Makefile for C projects

### C/Makefile

This Makefile allows you to: 
* create your project; 
* automatically compile no matter how many .c and .h files you have; 
* create .c and .h files; 
* add libraries; 
* add functions;
Suggestion: all includes should be made in the file "headers/headers.h" and all .c files should only include this file.

### Usage
#### Start your project
```shell
make start
```
This command will generate four directories (src, obj, bin, headers) with two files: src/main.c and headers/headers.h:
* src
  * main.c
* headers
  * headers.h
    * only <stdio.h> is added by deafult
* bin
* obj

#### Compile your project
```shell
make compile
```
This command will compile all your .c and .h files into .o objects inside obj directory and a bin/exec file for your main function at src/main.c

#### Run your project
```shell
make run
```
This command will compile, if necessary, your files and run /bin/exec

#### Add a library to your project
```shell
make add_library
```
This command will ask you for a lib name, *i.e. <math.h>* and will add it to header/headers.h file:
```c
#include <math.h>
```

#### Create a new module
```shell
make new_module
```
This command will ask you a name for your module, after that he will create two files:
* src/your_module.c
  * "headers.h" already included
* headers/your_module.h
  * "headers.h" already included
  * "your_module.h" is included in "headers.h"
  
#### Add a new method
```shell
make add_method
```
This command will ask you for a method call, *i.e. int square(int a)* and a existing module. After that it will add the lines:
```c
int square(int a);
```
at headers/your_module.h and
```c
int square(int a){

}
```
at src/your_module.c. **Notice that no return is added in non-void functions, that is up to you.**

#### Clean
```shell
make clean
```
This command will remove all .o files in obj directory and the file bin/exec and all \*~ files for emacs users.


### I hope you all find this useful, any problems contact me 😊

