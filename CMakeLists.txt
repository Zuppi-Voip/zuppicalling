name: Build MicroSIP Executable

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: windows-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Set Up CMake
      uses: lukka/get-cmake@v3

    - name: Install Dependencies
      run: |
        choco install -y visualstudio2022buildtools
        choco install -y visualstudio2022-workload-vctools
        choco install -y git cmake ninja

    - name: Install PJSIP
      run: |
        git clone https://github.com/pjsip/pjproject.git
        cd pjproject
        ./configure --enable-shared
        cmake . -B build
        cmake --build build --config Release
        cmake --install build --prefix /pjsip/install

    - name: Build Project
      run: |
        mkdir build
        cd build
        cmake -A x64 -DPJSIP_INCLUDE_DIR=/pjsip/install/include -DPJSIP_LIBRARY=/pjsip/install/lib .. 
        cmake --build . --config Release

    - name: Upload Executable
      uses: actions/upload-artifact@v3
      with:
        name: ZuppiCalling-Executable
        path: build/Release/ZuppiCalling.exe
