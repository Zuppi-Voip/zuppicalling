name: Build MicroSIP Executable

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Install Dependencies
      run: |
        sudo apt-get update
        sudo apt-get install -y build-essential cmake libssl-dev
        # Install PJSIP
        git clone https://github.com/pjsip/pjproject.git
        cd pjproject
        ./configure
        make
        sudo make install

    - name: Build Project
      run: |
        mkdir build
        cd build
        cmake ..
        cmake --build . --config Release

    - name: Upload Executable
      uses: actions/upload-artifact@v3
      with:
        name: ZuppiCalling-Executable
        path: build/Release/ZuppiCalling.exe
