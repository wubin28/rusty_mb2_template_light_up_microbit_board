# An embedded Rust project template for the micro:bit v2

## How to generate a new project

Install Rust:

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Install cargo-generate:

```
cargo install cargo-generate
```

If you see the error: "failed to run custom build command for openssl-sys v0.9.104" when installing cargo-generate on Ubuntu, please run the following commands to install openssl dev library:

```
sudo apt update
sudo apt install libssl-dev pkg-config
# verify the installation
pkg-config --modversion openssl
# should see something like 3.0.2
```

Then generate a new project:

```
cargo generate wubin28/rusty_mb2_template_light_up_microbit_board
```

## How to run the code

Before cross-compiling you have to download a pre-compiled version of the standard library (a reduced version of it, actually) for your target:

```
rustup target add thumbv7em-none-eabihf
cargo build
```

Install the embedded toolkit [probe-rs](https://probe.rs/):

```
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/probe-rs/probe-rs/releases/latest/download/probe-rs-tools-installer.sh | sh
```

### On Ubuntu and macOS:

```
cargo run
```

### On Windows 11:
```
cargo run --probe <VID:PID:SN>
```

## How to debug the code on Ubuntu

### On terminal 1:
```
cd {{project-name}}
cargo embed
```

### On terminal 2:
```
cd {{project-name}}
gdb-multiarch target/thumbv7em-none-eabihf/debug/{{project-name}}
(gdb) target remote :1337
(gdb) break main
(gdb) continue
(gdb) quit
```

## How to debug the code on macOS

### On terminal 1:
```
cd {{project-name}}
cargo embed
```

### On terminal 2:
```
cd {{project-name}}
arm-none-eabi-gdb target/thumbv7em-none-eabihf/debug/{{project-name}}
(gdb) target remote :1337
(gdb) break main
(gdb) continue
(gdb) quit
```

## How to debug the code on Windows 11

### On PowerShell 1:
```
cd {{project-name}}
cargo embed --probe <VID:PID:SN>
```

### On PowerShell 2:
```
cd {{project-name}}
arm-none-eabi-gdb target/thumbv7em-none-eabihf/debug/{{project-name}}
(gdb) target remote :1337
(gdb) break main
(gdb) continue
(gdb) quit
```
