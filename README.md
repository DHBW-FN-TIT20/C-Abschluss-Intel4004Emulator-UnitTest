# UnitTests for C-Abschluss-Intel4004Emulator
Version 1.1.1

## Folder structure
Folder | Usage
------ | -----
[4001-ROM](4001-ROM) | source files for Intel4001 ROM module
[4002-RAM](4002-RAM) | source files for Intel4002 RAM module
[4004](4004) | source files for Intel4004 module
[docs](docs) | documentaion on Intel400x
[inc](inc) | source files for Intel400x
[src](src) | contains [unittest.cpp](src/unittest.cpp)

> Note: The 400x files are only for test and error indication purposes and are property of group [Felder, Herkommer, Schuler, Silberzahn](https://github.com/DHBW-FN-TIT20/C-Abschluss-Intel4004Emulator)

## How to use
* Copy the file [unittest.cpp](src/unittest.cpp) from the [src](src) folder to your project
* Copy the file [BinaryFile.bin](inc/BinaryFile.bin) and [IntelHexFile.hex](inc/IntelHexFile.hex) from the [inc](inc) folder to your project
* Replace the following include paths with your corresponding paths *(Make sure to use \\ for windows and / for unix!)*
```C++
#if defined(WIN32) || defined(_WIN32) || defined(__WIN32__) || defined(__NT__)
    #include "..\inc\catch.hpp"
    #include "..\4004\4004.h"
#elif __unix__
    #include "../inc/catch.hpp"
    #include "../4004/4004.h"
#endif
```
* Replace the following define paths with your corresponding paths *(Make sure to use \\\\ for windows and / for unix!)*
```C++
#if defined(WIN32) || defined(_WIN32) || defined(__WIN32__) || defined(__NT__)
    #define INTEL_HEX_FILE_PATH "..\\inc\\IntelHexFile.hex"
    #define BINARY_FILE_PATH "..\\inc\\BinaryFile.bin"
#elif __unix__
    #define INTEL_HEX_FILE_PATH "../inc/IntelHexFile.hex"
    #define BINARY_FILE_PATH "../inc/BinaryFile.bin"
#endif
```
* Compile unittest.cpp according to the [Compile](#Compile) section
* Run the compiled file, for help, take a look at the [How to Run](#How-to-Run) section
* For help during execution, take a look at the [Bug Fixing](#Bug-Fixing) section
> Note: Due to the fact that I made some changes to the given sample solutions, some of the unit tests for Intel4001 and Intel4004Stack might fail. In that case you have to decide wheter you want to stick to the sample solution or make changes according to the unit tests.

## Compile
### Windows:
```powershell
g++ unittest.cpp ..\4001-ROM\4001.cpp ..\4002-RAM\4002.cpp ..\4004\4004.cpp ..\4004\4004_stack.cpp ..\inc\intelhex.c -o unittest.exe
```

### Linux:
```bash
g++ unittest.cpp ../4001-ROM/4001.cpp ../4002-RAM/4002.cpp ../4004/4004.cpp ../4004/4004_stack.cpp ../inc/intelhex.c -o unittest.out
```

> Note: Your relative paths to the needed c/cpp files might be different if you are not using this project's structure or file naming

## How to Run
### Windows:
* `unittest.exe <test name>`

### Linux:
* `./unittest.out <test name>`
> Note: With \<test name\> you can specify the TestCase that should be executed i.e.: `UnitTest_Intel4004_Mnemonics` or `UnitTest_4001`

### Commandline Options:
Option | Effect
------ | ------
-h, -? | display usage information
-s | include successful tests in output
-x \<no. failures\> | abort after x failures
-d \<yes\|no\> | show test durations
-c \<section name\> | specify section to run

> Note: The section names correspond with the Mnemonic names and follow the order of [4004Data.pdf](docs/4004Data.pdf). i.e.: `NOP`, `JCN`, `FIM`, ...

## Bug Fixing
* If the unit test stops execution printing only `Filters:` there was an error!
    * Make sure to differentiate when deleting variables that where created with the `new` statement
        - [ ] Objects / everyting except arrays: `delete <var>`
        - [ ] Arrays: `delete[] <var>`
    * Check whether you are writing to memory you do not own (i.e. if your array is too small)

## ToDo
* Reset in 4002 -> data ram bank 0 selection

## Authors
* Henry Schuler / [github](https://github.com/schuler-henry) / [E-Mail](mailto:schuler.henry-it20@it.dhbw-ravensburg.de?subject=[GitHub]%20C%20Intel4004%20Emulator%20UnitTest)

## [License](LICENSE.md)

MIT License

Copyright (c) 2021 Henry Schuler

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
