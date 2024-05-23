# Environment Setup

The first thing we need to do is setup your environemnt.

1. Clone the [SIMPLELINK-MSP432-SDK Repo](https://github.com/Topographic-Robot/SIMPLELINK-MSP432-SDK)
2. Install the correct instance for your OS
3. Link the install path of the files to your system.
	1. In your `~/.bashrc` add the following:

```sh
export MSP432_HEADERS=/path/to/headers/
# for example
export MSP432_HEADERS=/home/brighton/Documents/SDK/ti/msp432/simplelink_msp432p4_sdk_3_40_01_02/
```

4. Source: `source ~/.bashrc`
5. Install more packages with sudo

```sh
apt-get install build-essential gcc make gcc-arm-none-eabi openocd gconf2 bear screen
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
export PATH=$PATH:$HOME/go/bin

# source
source ~/.bashrc
```
