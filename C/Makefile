 # # # # # # # # # # # # # # # # # # # # # # # #
 # This Makefile was made by Laura Viglioni    #
 # https://github.com/viglioni                 #
 # 2018                                        #
 # License: GNU GENERAL PUBLIC LICENSE v3      #
 # # # # # # # # # # # # # # # # # # # # # # # # 



CC=gcc

SRC_DIR := src
EXEC_DIR := bin
INC_DIR := headers
OBJ_DIR := obj

SRC_PATH := ./$(SRC_DIR)
EXEC_PATH := ./$(EXEC_DIR)
INC_PATH := ./$(INC_DIR)
OBJ_PATH := ./$(OBJ_DIR)

EXEC := $(EXEC_PATH)/exec

CFLAGS=-c  -pedantic -Wall -m64
INC_FLAGS := -I$(INC_PATH)
LDFLAGS:=

SOURCES= $(shell ( [ -d $(SRC_PATH) ] && find $(SRC_PATH) -name *.c))
OBJECTS= $(SOURCES:$(SRC_PATH)/%.c=$(OBJ_PATH)/%.o)

all: start welcome

welcome:
	@printf "\n\nWelcome!\nType \"make help\" for usage!\n\n"
compile: $(EXEC)

run: compile
	$(EXEC)

new_module:
	@read -p "Enter Module Name: " module; \
	touch $(INC_PATH)/$$module.h; \
	touch $(SRC_PATH)/$$module.c; \
	([ -s $(SRC_PATH)/$$module.c ] && echo "Module already exists!!") || \
	( \
	printf "#include \"headers.h\" \n" > $(SRC_PATH)/$$module.c ; \
	echo "#include \"$$module.h\"" >> $(INC_PATH)/headers.h ; \
	echo "Module $$module created with success!" ; \
	ls $(SRC_PATH) $(INC_PATH) \
	)

start:
	@echo "Building project"
	@mkdir -p $(SRC_DIR) $(EXEC_DIR) $(INC_DIR) $(OBJ_DIR)
	@touch $(SRC_PATH)/main.c
	@touch $(INC_PATH)/headers.h
	@[ -s $(SRC_PATH)/main.c ] || printf "#include \"headers.h\" \n\nint main(){\nputs(\"Your project is working!\");\nreturn 0;\n}\n" > $(SRC_PATH)/main.c
	@[ -s $(INC_PATH)/headers.h ] || printf "#include <stdio.h>\n" > $(INC_PATH)/headers.h
	@ls -R

add_method:
	@read -p "Enter method header (e.g. \"int sum(int a, int b)\" without quotes and ;): " method; \
	read -p "For which module?: " module; \
	( \
	([ -f $(SRC_PATH)/$$module.c ] && [ -f $(INC_PATH)/$$module.h ]) && \
	echo $$method ";" >> $(INC_PATH)/$$module.h ; \
	echo $$method "{" >> $(SRC_PATH)/$$module.c ; \
	echo "" >> $(SRC_PATH)/$$module.c ; \
	echo "}" >> $(SRC_PATH)/$$module.c ; \
	echo "Method added with success!" ; \
	cat $(SRC_PATH)/$$module.c  \
	) || \
	echo "Module does not exist! Create it with \"make new_module\""

$(OBJECTS): $(OBJ_PATH)/%.o : $(SRC_PATH)/%.c
	@$(CC) $(INC_FLAGS) $(CFLAGS) $< -o $@

$(EXEC): $(OBJECTS)
	@$(CC) $(LDFLAGS) $(OBJECTS) -o $@

clean:
	@rm -rf $(EXEC) $(OBJECTS) 
	@find . -iname *~ -exec rm -rf {} \;

help:
	@printf "\n\nHello!\n\
	Start your project with: make or make start\n\
	Compile with: make compile\n\
	Run with: make run\n\
	Create new file.c and file.h with: make new_module\n\
	\t- includes will be made automatically!\n\
	Clean *.o, *~ and exec files with: make clean\n\
	To add a method to a .c and .h file: make add_method\n\
	\t- the .c and .h files must exist! You may create them with \"make new_module\"\n\
	Good work!!!\n\n\n"