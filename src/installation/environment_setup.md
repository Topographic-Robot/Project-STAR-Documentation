# Environment Setup

## Linux Environment (tested on debian-12.6.0)

The first thing we need to do is setup your environemnt.

1. Clone the [SIMPLELINK-SDK Repo](https://github.com/Topographic-Robot/SIMPLELINK-SDK)
2. Install the correct instance for your OS (`.run`)
3. Link the install path of the files to your system.
   1. In your `~/.bashrc` add the following:

```sh
export SIMPLELINK_MSP432P4_SDK="/path/to/headers/"
# for example
export SIMPLELINK_MSP432P4_SDK="/home/brighton/Documents/SDK/ti/msp432/simplelink_msp432p4_sdk_3_40_01_02/"
```

4. Source: `source ~/.bashrc`
5. Install more packages with sudo

```sh
apt-get install build-essential gcc make gcc-arm-none-eabi openocd gconf2 bear screen qemu-system-arm gdb-multiarch
```

6. Install clang-format

```sh
sudo apt-get install wget lsb-release software-properties-common
wget https://apt.llvm.org/llvm.sh
chmod +x llvm.sh
sudo bash ./llvm.sh 17
sudo apt-get update
sudo apt-get install clang-format-17
```

7. Install asmfmt

```sh
sudo apt update
sudo apt install golang
go install github.com/klauspost/asmfmt/cmd/asmfmt@latest

# in ~/.bashrc add:
export PATH="$PATH:$HOME/go/bin"

# source
source ~/.bashrc
```

## MacOS Environment (tested on MacBook Air M1 2020 with Sonoma v14.5)

The first thing we need to do is setup your environemnt.

1. Clone the [SIMPLELINK-SDK Repo](https://github.com/Topographic-Robot/SIMPLELINK-SDK)
2. Install the correct instance for your OS (`.zip`)
    1. You will need to extract the .zip, do this in finder or the terminal with `unzip`
    2. You will then see a `.app`, run these 2 files.
    3. Check below for common issues if they occur
3. Link the install path of the files to your system.
   1. In your `~/.zshrc` add the following:

```sh
export SIMPLELINK_MSP432P4_SDK="/path/to/headers/"
# for example
export SIMPLELINK_MSP432P4_SDK="/Applications/ti/simplelink_msp432p4_sdk_3_40_01_02"
```

4. Source: `source ~/.zshrc`
5. Install more packages
    - NOTE: `gdb` cant be installed so `lldb` must be used instead
```sh
brew install gcc make pkg-config arm-none-eabi-gcc openocd bear screen qemu
```

Keep in mind
> GNU "make" has been installed as "gmake".
> If you need to use it as "make", you can add a "gnubin" directory
> to your PATH from your bashrc like:
> 
>     ``PATH="/opt/homebrew/opt/make/libexec/gnubin:$PATH"``

6. Install clang-format

## Common Issues
1. MacOS: "“simplelink_sdk_wifi_plugin_4_20_00_10” can’t be opened because Apple cannot check it for malicious software."
    1. Open System Settings
    2. Go to Privacy & Security
    3. Allow the App
        1. In the "Security & Privacy" window
        2. You should see a message near the bottom saying that the app was blocked because it is not from an identified developer
        3. Click the "Open Anyway" button next to this message
        4. Open the App
        5. A new dialog box will appear asking if you are sure you want to open the app. Confirm by clicking "Open"
