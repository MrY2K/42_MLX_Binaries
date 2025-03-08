# 42_MLX_Binaries
For Mac And Linux

# Dependencies for linux:
**Make sure you install glfw package for your linux desto**

## For Debian based Distros:
```bash
sudo apt-get update
sudo apt-get install libglfw3-dev
```

## For Fedora and RHEL based Distros:
```bash
sudo dnf install glfw glfw-devel
```

## For Arch based Distros:
```bash
sudo pacman -Syu
sudo pacman -S glfw
```

# Example of dynamic Makefile if your using both systems:
```Makefile
BUILD_DIR    = ./build
NAME		 = t
CFLAGS       = # -Wall -Wexta -Werror -Ofast -DDEBUG=1 

MLX_Version  = Old
UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Darwin)
	MLX_FLAGS = -LMLX/build -lmlx42 -lglfw3 -IMLX/include -framework Cocoa -framework OpenGL -framework IOKit
	CC        = clang
	os_msg = "$(GREEN)OS DETECTED Mac!$(RESET)"

else ifeq ($(UNAME_S),Linux)
	MLX_FLAGS = -LMLX_Linux/build/ -lmlx42 -lglfw -lGL -lm -ldl -lpthread -lX11 -I MLX_Linux/include
	CC		  = gcc
	os_msg = "$(GREEN)OS DETECTED Linux!$(RESET)"
endif


all: os_msg $(BUILD_DIR) $(NAME)

os_msg:
	@echo $(os_msg)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(NAME):
	echo "$(GREEN)MADE program $(RESET)"
	$(CC) $(CFLAGS) main.c -o $(NAME) $(MLX_FLAGS)

clean:
	rm -rf $(BUILD_DIR)

fclean: clean
	rm -rf $(NAME)

re: fclean all

GREEN = \033[0;32m
RED = \033[0;31m
RESET = \033[0m
```