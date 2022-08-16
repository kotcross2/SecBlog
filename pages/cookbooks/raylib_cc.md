
Some notes on crosscompiling raylib for windows, i did it on debian but it should work with some tweaks on other *nix that have a mingw toolchain too.   
   
## installing the tools

Install the libraries:
```
sudo apt-get install mingw-w64 mingw-w64-common mingw-w64-tools gdb-mingw-w64
```
   
## building raylib for win 

- make a copy of raylib into another folder, for example `winraylib`

- after proceeding, go to `winraylib/src` and `make clean`
```
make clean 
x86_64-w64-mingw32-windres raylib.rc -o raylib.rc.data
make OS=Windows_NT CC=x86_64-w64-mingw32-gcc AR=x86_64-w64-mingw32-ar
```
to generate a `libraylib.a` for windows 64 bit
   
## making a project that cross compiles 

I'm using the 4coder Makefile, into your project Makefile you should add the next section at line 184 to override some parameters when crosscompiling:
```
ifeq ($(CROSS),WINDOWS)
	PROJECT_NAME = your_game_name_win
	RAYLIB_PATH = /path/to/your/winraylib
	RAYLIB_RELEASE_PATH = $(RAYLIB_PATH)/src
	EXAMPLE_RUNTIME_PATH = $(RAYLIB_RELEASE_PATH)
	CC=x86_64-w64-mingw32-gcc
	AR=x86_64-w64-mingw32-ar
	MAKE = make
	PLATFORM_OS=WINDOWS
endif
```
fill the field with the path to your winraylib and a slightly different name for the output binary (otherwise it won't compile it if there is already an up to day compiled executable in the folder).

After that, when you use `make` it will spit out a binary for your system, if you use `make CROSS=WINDOWS` it will output a win64 binary instead. You can use `wine game.exe` for testing it.

## additional notes 

Sometimes small software written in c and compiled with minGW is [viewed by Windows as a virus](https://security.stackexchange.com/questions/229576/program-compiled-with-mingw32-is-reported-as-infected). For now i tested that using `-O3` instead of `-O1` as optimization flag fixes this, but surely more investigation has to be done.
 