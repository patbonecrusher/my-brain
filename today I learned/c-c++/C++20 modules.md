---
creation date: 2024-05-27 22:22
modification date: Monday, 27th May 2024, 22:22:55
tags: today_i_leaned
---
## Cause

Thanks for the comments - the errors above are an indication of a Clang version that was built without module support. This is what Xcode comes with, i.e. by running `xcode-select --install` in a terminal.

## Solution

As suggested the solution has been to install Clang thru HomeBrew which is done as follows (tested on macOS Monterey):

```cpp
brew install llvm
```

Clang gets installed to `/opt/homebrew/opt/llvm/bin/clang++`. Confirm the running version as shown below:

```cpp
% /opt/homebrew/opt/llvm/bin/clang++ --version
Homebrew clang version 13.0.0
Target: arm64-apple-darwin21.1.0
Thread model: posix
InstalledDir: /opt/homebrew/opt/llvm/bin
```

Which is a different build from the Xcode system-wide default version:

```cpp
% clang++ --version
Apple clang version 13.0.0 (clang-1300.0.29.3)
Target: arm64-apple-darwin21.1.0
Thread model: posix
InstalledDir: /Library/Developer/CommandLineTools/usr/bin
```

## Working Example

Steps to see working example loosely based on [repo](https://github.com/alexpanter/modules_testing) posted by @alexpanter:

**main.cpp**

```cpp
import <iostream>;
import mathlib;

using namespace std;

int main() {
    cout << "Modules, baby!" << endl;
    cout << "2 plus 3 makes " << add(2, 3) << " says module 'mathlib'" << endl;
}
```

**mathlib.cpp**

```cpp
export module mathlib;

export int add(int a, int b)
{
    return a + b;
}
```

Build by runnning in a terminal in same directory as files above:

```cpp
/opt/homebrew/opt/llvm/bin/clang++ -std=c++20 -c -Xclang -emit-module-interface mathlib.cpp -o mathlib.pcm
/opt/homebrew/opt/llvm/bin/clang++ -std=c++20 -fmodules -c -fprebuilt-module-path=. main.cpp -o main.o
/opt/homebrew/opt/llvm/bin/clang++ -std=c++2a -fmodules -o main main.o *.pcm
```

Test module-based executable:

```cpp
./main
```

Expected output:

```cpp
Modules, baby!
2 plus 3 makes 5 says module 'mathlib'
```
