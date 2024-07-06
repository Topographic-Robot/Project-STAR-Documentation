# Environment Setup

## Linux Environment (tested on debian-12.6.0)

## MacOS Environment (tested on MacBook Air M1 2020 with Sonoma v14.5)

1. Install esp-idf, follow and run: [esp-idf MacOS setup](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html)
   1. `brew install cmake ninja dfu-util`
   2. `git clone --recursive https://github.com/espressif/esp-idf.git`
   3. `cd esp-idf`
   4. `./install.sh esp32`
   5. `echo "alias get_idf=\". $(pwd)/export.sh\"" >> ~/.zshrc`
   6. `source ~/.zshrc`
   7. Run this every time in a project to get `idf.py`: `get_idf`
2. Install more packages
   1. `brew install gcc make pkg-config arm-none-eabi-gcc openocd bear screen qemu`
      - NOTE: `gdb` cant be installed so `lldb` must be used instead

Keep in mind

> GNU "make" has been installed as "gmake".
> If you need to use it as "make", you can add a "gnubin" directory
> to your PATH from your zshrc like:
>
> `export PATH="/opt/homebrew/opt/make/libexec/gnubin:$PATH"`

3. Install clang-format v17+
   1. `brew update`
   2. `brew install llvm`

> If you need to have llvm first in your PATH, run:
> `export PATH="/opt/homebrew/opt/llvm/bin:$PATH"`
>
> For compilers to find llvm you may need to set:
> `export LDFLAGS="-L/opt/homebrew/opt/llvm/lib"` > `export CPPFLAGS="-I/opt/homebrew/opt/llvm/include"`
>
> To avoid clobbering:
> `export LDFLAGS="$LDFLAGS -L/opt/homebrew/opt/llvm/lib"` > `export CPPFLAGS="$CPPFLAGS -I/opt/homebrew/opt/llvm/include"`

When I did this, I got

```sh
source ~/.zshrc
clang-format --version

Homebrew clang-format version 18.1.8
```

4. Install asmfmt

   1. `brew update`
   2. `brew install go`
   3. `go install github.com/klauspost/asmfmt/cmd/asmfmt@latest`
   4. `echo 'export PATH="$PATH:$HOME/go/bin"' >> ~/.zshrc`
   5. `source ~/.zshrc`

5. (Optional) Install VS Code Plugin
   1. [VS Code Plugin](https://github.com/espressif/vscode-esp-idf-extension/blob/master/docs/tutorial/install.md)
   2. ![vscode-esp-idf-extension](vscode-esp-idf-extension-macos.png)

## Windows Environment (tested on Windows 11 23H2)

The first thing we need to do is setup your environment.

1. Install esp-idf
   1. Follow and run: [esp-idf Windows setup](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html)
2. (Optional) Install VS Code Plugin
   1. [VS Code Plugin](https://github.com/espressif/vscode-esp-idf-extension/blob/master/docs/tutorial/install.md)
3. Install clang-format
   1. Download, Run, and Install [LLVM](https://github.com/llvm/llvm-project/releases/download/llvmorg-18.1.8/LLVM-18.1.8-win64.exe)
   2. Verify download worked

```sh
clang-format --version

clang-format version 18.1.8
```

4. Install asmfmt
   1. Install golang
      1. Download, Run, and Install [GO](https://go.dev/dl/go1.22.5.windows-amd64.msi)
   2. `go install github.com/klauspost/asmfmt/cmd/asmfmt@latest`
