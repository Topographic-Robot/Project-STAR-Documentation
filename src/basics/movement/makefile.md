# Movement Makefile

This Makefile is used to build and upload firmware for the MSP432P401R microcontroller. Below is an explanation of each part, including every flag and its purpose.

## Variables

```makefile
SIMPLELINK_MSP432P4_SDK := $(SIMPLELINK_MSP432P4_SDK)
```

- **SIMPLELINK_MSP432P4_SDK**: Path to the SimpleLink MSP432P4 SDK. It allows the inclusion of SDK source files and headers, which are necessary for using the libraries and functions provided by TI for the MSP432P401R microcontroller.

### Toolchain

```makefile
CC  = arm-none-eabi-gcc # compiler
AS  = arm-none-eabi-gcc # assembler
LNK = arm-none-eabi-gcc # linker

OBJCOPY = arm-none-eabi-objcopy # copy and translate object files into machine-readable opcodes
```

- **CC**: The C compiler. `arm-none-eabi-gcc` is a cross-compiler for ARM Cortex microcontrollers. We use this to compile C source code into object files for embedded systems.
- **AS**: The assembler, also using `arm-none-eabi-gcc` for consistency, to convert assembly language source code into object files.
- **LNK**: The linker, which combines object files into a single executable. This is crucial for creating a final firmware image.
- **OBJCOPY**: A utility to copy and translate object files into different formats, such as converting ELF (Executable and Linkable Format) to binary. This is used for creating the final binary file that will be uploaded to the microcontroller.

### Project Information

```makefile
NAME        = topographic-robot
SRC_DIR     = src
LIB_DIR     = ../../lib
LNK_DIR     = ../../lnk
BUILD_DIR   = build
DEBUG_DIR   = $(BUILD_DIR)/debug
RELEASE_DIR = $(BUILD_DIR)/release
```

- **NAME**: The name of the project, which will be used for naming the final output files.
- **SRC_DIR**: Directory containing source files. This keeps the source code organized.
- **LIB_DIR**: Directory containing library files. This allows for modular development by reusing libraries.
- **LNK_DIR**: Directory containing linker scripts. Linker scripts are used to control the memory layout of the output file.
- **BUILD_DIR**: Directory for build output. This keeps the build artifacts separate from the source code.
- **DEBUG_DIR**: Directory for debug build output. This helps in organizing the output files for different build configurations.
- **RELEASE_DIR**: Directory for release build output. This helps in organizing the output files for different build configurations.

### Debugging and Simulation Tools

```makefile
OPENOCD     = openocd # open on-chip debugger (debugging)
OPENOCD_DIR = /usr/share/openocd/scripts/board
OPENOCD_CFG = "$(OPENOCD_DIR)/ti_msp432_launchpad.cfg"
QEMU        = qemu-system-arm
```

- **OPENOCD**: Open On-Chip Debugger used for programming and debugging embedded targets. It communicates with the microcontroller and allows us to flash firmware and perform debugging.
- **OPENOCD_DIR**: Directory containing OpenOCD scripts, which are necessary for specifying the target board and its configuration.
- **OPENOCD_CFG**: Configuration file for OpenOCD to specify the target board (MSP432 Launchpad in this case).
- **QEMU**: QEMU emulator for simulating ARM systems. This is used for running the firmware in a simulated environment, which is useful for testing without needing the actual hardware.

### GDB Configuration

```makefile
ifeq (, $(shell which arm-none-eabi-gdb))
  GDB = gdb-multiarch
else
  GDB = arm-none-eabi-gdb
endif
```

- **GDB**: GNU Debugger for ARM, used for debugging applications. If `arm-none-eabi-gdb` is not found, it falls back to `gdb-multiarch`. This ensures that we have a debugger available regardless of the specific toolchain installation.

## Compiler and Linker Flags

### Common Flags

```makefile
CFLAGS_COMMON = -I"$(SIMPLELINK_MSP432P4_SDK)/source" \
                -I"$(SIMPLELINK_MSP432P4_SDK)/source/third_party/CMSIS/Include" \
                -D__MSP432P401R__ \
                -DDeviceFamily_MSP432P401x \
                -mcpu=cortex-m4 \
                -mthumb \
                -mfloat-abi=hard \
                -mfpu=fpv4-sp-d16
```

- **CFLAGS_COMMON**: Common compiler flags for both debug and release builds.
  - `-I"$(SIMPLELINK_MSP432P4_SDK)/source"`: Adds the SDK source directory to the compiler's include path, allowing the compiler to find header files.
  - `-I"$(SIMPLELINK_MSP432P4_SDK)/source/third_party/CMSIS/Include"`: Adds the CMSIS include directory to the compiler's include path. CMSIS (Cortex Microcontroller Software Interface Standard) provides a standardized interface to the processor and peripherals.
  - `-D__MSP432P401R__`: Defines a preprocessor macro for the MSP432P401R device, enabling device-specific code.
  - `-DDeviceFamily_MSP432P401x`: Defines a preprocessor macro for the MSP432P401x device family, enabling family-specific code.
  - `-mcpu=cortex-m4`: Specifies the target CPU architecture as Cortex-M4, optimizing the code for this specific processor.
  - `-mthumb`: Generates code for the Thumb instruction set, which is a compact, efficient instruction set for ARM processors.
  - `-mfloat-abi=hard`: Uses hardware floating-point instructions, which are faster than software emulation.
  - `-mfpu=fpv4-sp-d16`: Specifies the floating-point unit as single-precision, with 16 registers, enhancing floating-point operations' performance.

### Debug Flags

```makefile
CFLAGS_DEBUG = -g -O0 -DDEBUG $(CFLAGS_COMMON)
ASFLAGS_DEBUG = $(CFLAGS_COMMON)
```

- **CFLAGS_DEBUG**: Compiler flags for debug builds.
  - `-g`: Generates debug information, which is essential for source-level debugging.
  - `-O0`: Disables optimizations to make debugging easier and more predictable, as optimized code can be difficult to debug.
  - `-DDEBUG`: Defines a preprocessor macro for debugging, enabling debug-specific code.
- **ASFLAGS_DEBUG**: Assembler flags for debug builds, same as the common flags to ensure consistency.

### Release Flags

```makefile
CFLAGS_RELEASE = -s -O3 -DNDEBUG $(CFLAGS_COMMON)
ASFLAGS_RELEASE = $(CFLAGS_COMMON)
```

- **CFLAGS_RELEASE**: Compiler flags for release builds.
  - `-s`: Strips symbols from the output, reducing the final binary size.
  - `-O3`: Optimizes for speed, generating the fastest possible code.
  - `-DNDEBUG`: Defines a preprocessor macro to disable debugging code, ensuring that no debug-related code is included in the release build.
- **ASFLAGS_RELEASE**: Assembler flags for release builds, same as the common flags to ensure consistency.

### Linker Flags

```makefile
LFLAGS = -T "$(LNK_DIR)/msp432p401r.lds" --specs=nosys.specs \
         -L"$(SIMPLELINK_MSP432P4_SDK)/source" \
         -l:ti/devices/msp432p4xx/driverlib/gcc/msp432p4xx_driverlib.a \
         -static \
         -Wl,--gc-sections \
         -lgcc \
         -lc \
         -lm \
         -lnosys \
         --specs=nano.specs \
         -mcpu=cortex-m4 \
         -mthumb \
         -mfloat-abi=hard \
         -mfpu=fpv4-sp-d16
```

- **LFLAGS**: Linker flags.
  - `-T "$(LNK_DIR)/msp432p401r.lds"`: Specifies the linker script, which defines the memory layout of the output file.
  - `--specs=nosys.specs`: Links with a minimal C library suitable for embedded systems.
  - `-L"$(SIMPLELINK_MSP432P4_SDK)/source"`: Adds the SDK source directory to the linker search path.
  - `-l:ti/devices/msp432p4xx/driverlib/gcc/msp432p4xx_driverlib.a`: Links with the MSP432 driver library, providing peripheral driver support.
  - `-static`: Produces a statically linked executable, which includes all necessary libraries, making the executable self-contained.
  - `-Wl,--gc-sections`: Removes unused sections, reducing the final binary size.
  - `-lgcc`: Links with the GCC runtime library, providing necessary runtime support.
  - `-lc`: Links with the standard C library.
  - `-lm`: Links with the math library.
  - `-lnosys`: Links with the minimal system library, suitable for bare-metal applications.
  - `--specs=nano.specs`: Uses the newlib-nano C library, which is a smaller, more efficient version of the standard C library.
  -

 `-mcpu=cortex-m4`: Specifies the target CPU architecture.
  - `-mthumb`: Generates code for the Thumb instruction set.
  - `-mfloat-abi=hard`: Uses hardware floating-point instructions.
  - `-mfpu=fpv4-sp-d16`: Specifies the floating-point unit.

## Source Files and Objects

```makefile
C_SOURCES           = $(wildcard $(SRC_DIR)/*.c) $(wildcard $(LIB_DIR)/*.c)
ASM_SOURCES         = $(wildcard $(SRC_DIR)/*.s)
C_OBJECTS_DEBUG     = $(patsubst $(SRC_DIR)/%.c,$(DEBUG_DIR)/%.o,$(wildcard $(SRC_DIR)/*.c)) \
                      $(patsubst $(LIB_DIR)/%.c,$(DEBUG_DIR)/%.o,$(wildcard $(LIB_DIR)/*.c))
C_OBJECTS_RELEASE   = $(patsubst $(SRC_DIR)/%.c,$(RELEASE_DIR)/%.o,$(wildcard $(SRC_DIR)/*.c)) \
                      $(patsubst $(LIB_DIR)/%.c,$(RELEASE_DIR)/%.o,$(wildcard $(LIB_DIR)/*.c))
ASM_OBJECTS_DEBUG   = $(patsubst $(SRC_DIR)/%.s,$(DEBUG_DIR)/%.o,$(wildcard $(SRC_DIR)/*.s))
ASM_OBJECTS_RELEASE = $(patsubst $(SRC_DIR)/%.s,$(RELEASE_DIR)/%.o,$(wildcard $(SRC_DIR)/*.s))
OBJECTS_DEBUG       = $(C_OBJECTS_DEBUG) $(ASM_OBJECTS_DEBUG)
OBJECTS_RELEASE     = $(C_OBJECTS_RELEASE) $(ASM_OBJECTS_RELEASE)
```

- **C_SOURCES**: C source files in `src` and `lib` directories.
- **ASM_SOURCES**: Assembly source files in `src` directory.
- **C_OBJECTS_DEBUG**: Debug build object files from C sources, using pattern substitution to map source files to object files.
- **C_OBJECTS_RELEASE**: Release build object files from C sources, using pattern substitution to map source files to object files.
- **ASM_OBJECTS_DEBUG**: Debug build object files from assembly sources, using pattern substitution to map source files to object files.
- **ASM_OBJECTS_RELEASE**: Release build object files from assembly sources, using pattern substitution to map source files to object files.
- **OBJECTS_DEBUG**: All debug build object files, both C and assembly.
- **OBJECTS_RELEASE**: All release build object files, both C and assembly.

## Build Targets

### All

```makefile
all: release
```

- **all**: Default target that builds the release version.

### Debug and Release

```makefile
debug: CFLAGS = $(CFLAGS_DEBUG)
debug: $(DEBUG_DIR)/$(NAME).elf

release: CFLAGS = $(CFLAGS_RELEASE)
release: $(RELEASE_DIR)/$(NAME).elf
```

- **debug**: Builds the project with debug flags.
- **release**: Builds the project with release flags.

### Linking

```makefile
$(DEBUG_DIR)/$(NAME).elf: $(OBJECTS_DEBUG)
    @mkdir -p $(DEBUG_DIR)
    @echo "Linking $@"
    $(LNK) $(OBJECTS_DEBUG) $(LFLAGS) -o $@

$(RELEASE_DIR)/$(NAME).elf: $(OBJECTS_RELEASE)
    @mkdir -p $(RELEASE_DIR)
    @echo "Linking $@"
    $(LNK) $(OBJECTS_RELEASE) $(LFLAGS) -o $@
```

- **$(DEBUG_DIR)/$(NAME).elf**: Links all debug build object files into an ELF file. 
  - The `@mkdir -p $(DEBUG_DIR)` command ensures the debug build directory exists.
  - `$(LNK) $(OBJECTS_DEBUG) $(LFLAGS) -o $@` invokes the linker with the debug object files and linker flags to produce the ELF file.
- **$(RELEASE_DIR)/$(NAME).elf**: Links all release build object files into an ELF file. 
  - The `@mkdir -p $(RELEASE_DIR)` command ensures the release build directory exists.
  - `$(LNK) $(OBJECTS_RELEASE) $(LFLAGS) -o $@` invokes the linker with the release object files and linker flags to produce the ELF file.

### Compiling and Assembling

```makefile
$(DEBUG_DIR)/%.o: $(SRC_DIR)/%.c
    @mkdir -p $(DEBUG_DIR)
    @echo "Compiling $<"
    $(CC) $(CFLAGS_COMMON) -c $< -o $@

$(DEBUG_DIR)/%.o: $(SRC_DIR)/%.s
    @mkdir -p $(DEBUG_DIR)
    @echo "Assembling $<"
    $(AS) $(ASFLAGS_DEBUG) -c $< -o $@

$(DEBUG_DIR)/%.o: $(LIB_DIR)/%.c
    @mkdir -p $(DEBUG_DIR)
    @echo "Compiling $<"
    $(CC) $(CFLAGS_COMMON) -c $< -o $@

$(RELEASE_DIR)/%.o: $(SRC_DIR)/%.c
    @mkdir -p $(RELEASE_DIR)
    @echo "Compiling $<"
    $(CC) $(CFLAGS_COMMON) -c $< -o $@

$(RELEASE_DIR)/%.o: $(SRC_DIR)/%.s
    @mkdir -p $(RELEASE_DIR)
    @echo "Assembling $<"
    $(AS) $(ASFLAGS_RELEASE) -c $< -o $@

$(RELEASE_DIR)/%.o: $(LIB_DIR)/%.c
    @mkdir -p $(RELEASE_DIR)
    @echo "Compiling $<"
    $(CC) $(CFLAGS_COMMON) -c $< -o $@
```

- **$(DEBUG_DIR)/%.o: $(SRC_DIR)/%.c**: Compiles C source files in the `src` directory for the debug build.
  - `@mkdir -p $(DEBUG_DIR)` ensures the debug build directory exists.
  - `@echo "Compiling $<"` prints a message indicating the file being compiled.
  - `$(CC) $(CFLAGS_COMMON) -c $< -o $@` compiles the C source file with common compiler flags.
- **$(DEBUG_DIR)/%.o: $(SRC_DIR)/%.s**: Assembles assembly source files in the `src` directory for the debug build.
  - `@mkdir -p $(DEBUG_DIR)` ensures the debug build directory exists.
  - `@echo "Assembling $<"` prints a message indicating the file being assembled.
  - `$(AS) $(ASFLAGS_DEBUG) -c $< -o $@` assembles the assembly source file with debug assembler flags.
- **$(DEBUG_DIR)/%.o: $(LIB_DIR)/%.c**: Compiles C source files in the `lib` directory for the debug build.
  - `@mkdir -p $(DEBUG_DIR)` ensures the debug build directory exists.
  - `@echo "Compiling $<"` prints a message indicating the file being compiled.
  - `$(CC) $(CFLAGS_COMMON) -c $< -o $@` compiles the C source file with common compiler flags.
- **$(RELEASE_DIR)/%.o: $(SRC_DIR)/%.c**: Compiles C source files in the `src` directory for the release build.
  - `@mkdir -p $(RELEASE_DIR)` ensures the release build directory exists.
  - `@echo "Compiling $<"` prints a message indicating the file being compiled.
  - `$(CC) $(CFLAGS_COMMON) -c $< -o $@` compiles the C source file with common compiler flags.
- **$(RELEASE_DIR)/%.o: $(SRC_DIR)/%.s**: Assembles assembly source files in the `src` directory for the release build.
  - `@mkdir -p $(RELEASE_DIR)` ensures the release build directory exists.
  - `@echo "Assembling $<"` prints a message indicating the file being assembled.
  - `$(AS) $(ASFLAGS_RELEASE) -c $< -o $@` assembles the assembly source file with release assembler flags.
- **$(RELEASE_DIR)/%.o: $(LIB_DIR)/%.c**: Compiles C source files in the `lib` directory for the release build.
  - `@mkdir -p $(RELEASE_DIR)` ensures the release build directory exists.
  - `@echo "Compiling $<"` prints a message indicating the file being compiled.
  - `$(CC) $(CFLAGS_COMMON) -c $< -o $@` compiles the C source file with common compiler flags.

### Clean

```makefile
clean:
    @echo "Cleaning..."
    rm -rf $(BUILD_DIR)
```

- **clean**: Removes the build directory and its contents.
  - `@echo "Cleaning..."` prints a message indicating the cleaning process.
  - `rm -rf $(BUILD_DIR)` recursively deletes the build directory, removing all build artifacts to ensure a clean slate for the next build.

### Upload

```makefile
upload: release
    @echo "Uploading..."
    $(OPENOCD) -f $(OPENOCD_CFG) -c "program $(RELEASE_DIR)/$(NAME).elf verify reset; shutdown"
```

- **upload**: Builds the release version and uploads the firmware to the target device using OpenOCD.
  - `@echo "Uploading..."` prints a message indicating the upload process.
  - `$(OPENOCD) -f $(OPENOCD_CFG) -c

 "program $(RELEASE_DIR)/$(NAME).elf verify reset; shutdown"` uses OpenOCD to program the ELF file to the microcontroller, verify the programming, reset the microcontroller, and shut down OpenOCD. This ensures that the firmware is correctly uploaded and the microcontroller is ready to run the new firmware.

### Debug Run

```makefile
debug-run: debug
    @echo "Starting debugger..."
    @$(OPENOCD) -f $(OPENOCD_CFG) & \
    $(GDB) $(DEBUG_DIR)/$(NAME).elf \
    -ex "target remote localhost:3333" \
    -ex "monitor reset halt"
```

- **debug-run**: Builds the debug version and starts the debugger using OpenOCD and GDB.
  - `@echo "Starting debugger..."` prints a message indicating the start of the debugger.
  - `@$(OPENOCD) -f $(OPENOCD_CFG) &` starts OpenOCD in the background to connect to the microcontroller.
  - `$(GDB) $(DEBUG_DIR)/$(NAME).elf -ex "target remote localhost:3333" -ex "monitor reset halt"` starts GDB, connects to the OpenOCD server, and resets and halts the microcontroller. This setup allows interactive debugging of the firmware.

### Simulate

```makefile
simulate: debug
    @echo "Simulating..."
    pkill qemu-system-arm || true
    @$(QEMU) -machine mps2-an385 -cpu cortex-m3 -kernel $(DEBUG_DIR)/$(NAME).elf -nographic -s -S &
    @$(GDB) $(DEBUG_DIR)/$(NAME).elf -ex "target remote localhost:1234"
    @pkill qemu-system-arm || true
```

- **simulate**: Builds the debug version and starts the QEMU emulator for simulation.
  - `@echo "Simulating..."` prints a message indicating the start of the simulation.
  - `pkill qemu-system-arm || true` kills any running QEMU instances to avoid conflicts.
  - `@$(QEMU) -machine mps2-an385 -cpu cortex-m3 -kernel $(DEBUG_DIR)/$(NAME).elf -nographic -s -S &` starts QEMU in the background, simulating the ARM Cortex-M3 environment with the debug ELF file.
  - `@$(GDB) $(DEBUG_DIR)/$(NAME).elf -ex "target remote localhost:1234"` starts GDB and connects to the QEMU server for debugging.
  - `@pkill qemu-system-arm || true` stops the QEMU simulation after debugging.

### Phony Targets

```makefile
.PHONY: all debug release clean upload debug-run simulate
```

- **.PHONY**: Declares phony targets that do not represent actual files, ensuring make will always execute the commands associated with these targets. This is useful to avoid conflicts with files that might have the same name as the targets.
