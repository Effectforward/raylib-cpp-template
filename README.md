# Raylib C++ Template

A cross-platform C++ template using CMake and raylib. Configured for Windows, Linux, and macOS.

## Features

- Cross-platform build system using CMake
- raylib automatically downloaded and built via FetchContent
- Code formatting with clang-format
- Pre-configured VSCode environment
- C++17 standard

## Prerequisites

Install CMake (3.28+), Git, and platform-specific build tools:

### Ubuntu / Debian
```bash
sudo apt install cmake git build-essential libx11-dev libxrandr-dev libxinerama-dev libxi-dev libxext-dev libxcursor-dev mesa-common-dev
```

### Fedora / RHEL / CentOS
```bash
sudo dnf install cmake git gcc-c++ libX11-devel libXrandr-devel libXinerama-devel libXi-devel libXext-devel libXcursor-devel mesa-libGL-devel
```

### Arch / Manjaro
```bash
sudo pacman -S cmake git base-devel libx11 libxrandr libxinerama libxi libxext libxcursor mesa
```

### openSUSE
```bash
sudo zypper install cmake git gcc-c++ libX11-devel libXrandr-devel libXinerama-devel libXi-devel libXext-devel libXcursor-devel Mesa-devel
```

### Alpine
```bash
apk add cmake git musl-dev gcc g++ libx11-dev libxrandr-dev libxinerama-dev libxi-dev libxext-dev libxcursor-dev mesa-dev
```

### macOS
```bash
brew install cmake git
```

### Windows
1. Download CMake: https://cmake.org/download/
- During installation, check "Add CMake to system PATH"
2. Download Git: https://git-scm.com/download/win
3. Download Visual Studio Build Tools: https://visualstudio.microsoft.com/visual-cpp-build-tools/
- During installation, select "Desktop development with C++"

## Building

```bash
git clone https://github.com/Effectforward/raylib-cpp-template.git
cd raylib-cpp-template
cmake -B build
cmake --build build
```

First build takes longer as raylib is downloaded and compiled. Subsequent builds are faster. 
Time depends on internet connection and system performance.

On successful build, a window opens displaying a green circle in the center. The circle responds 
to keyboard input (WASD or arrow keys to move, ESC to close).

## Running

```bash
./build/bin/game              # Linux/macOS
./build/bin/game.exe          # Windows
```

## Development

### Adding Source Files

Edit `CMakeLists.txt` and add new files to the executable:

```cmake
add_executable(game 
    src/main.cpp
    src/new_file.cpp
)
```

Rebuild: `cmake --build build`

### Code Style

Code formatting is configured with clang-format:
- Indentation: tabs (displayed as 4 spaces)
- Line length: 100 characters
- Brace style: K&R

Apply formatting: `clang-format -i src/filename.cpp`

VSCode auto-formats on save.

### IDE

You are more than welcome to use any editor or IDE. This project includes VSCode configuration for convenience (clangd IntelliSense, cmake syntax highlighting). Extensions install automatically on first launch if using VSCode.

## Project Structure

```
.
├── CMakeLists.txt           # Build configuration
├── .clang-format            # Code formatting rules
├── .gitignore               # Git ignore patterns
├── README.md                # Setup guide
├── .vscode/                 # VSCode configuration
├── src/
│   └── main.cpp             # Main source file
└── include/
    └── game.h               # Header file
```
