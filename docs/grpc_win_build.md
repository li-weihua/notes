#  windows grpc build

## install grpc on Windows
The main reference website is: https://github.com/grpc/grpc/blob/master/test/distrib/cpp/run_distrib_test_cmake.bat

**NOTE：Do not follow  https://github.com/grpc/grpc/blob/master/BUILDING.md ！**

grpc depends openssl, zlib, protobuf, cares.

### Install Steps
1. Download openssl from website：https://storage.googleapis.com/grpc-testing.appspot.com/OpenSSL-Win64-1_1_0g.zip  and extract the .zip file. Then set the following varibles in cmd or powershell, for example on my machine
```bat
set OPENSSL_DIR=D:\ProgramFiles\OpenSSL-Win64
set SRC=D:\github\grpc-v1.21.0
set INSTALL_DIR=D:\ProgramFiles\grpc
```
2. zlib
cmake generate options for reference:
  - “Visual Studio 14 2015”
 - “Visual Studio 14 2015 ARM”
  - “Visual Studio 14 2015 Win64”
  - “Visual Studio 15 2017”
  - “Visual Studio 15 2017 ARM”
  - “Visual Studio 15 2017 Win64”

```bat
cd %SRC%
cd third_party/zlib
mkdir build
cd build

cmake .. -G "Visual Studio 14 2015 Win64" -DCMAKE_INSTALL_PREFIX=%INSTALL_DIR% -DZLIB_ROOT=%INSTALL_DIR% -Dprotobuf_MSVC_STATIC_RUNTIME=OFF -Dprotobuf_BUILD_TESTS=OFF

cmake --build . --config Release --target install
```

3. protobuf
```bat
cd third_party/protobuf/cmake
mkdir build
cd build

cmake .. -G "Visual Studio 14 2015 Win64" -DCMAKE_INSTALL_PREFIX=%INSTALL_DIR% -DZLIB_ROOT=%INSTALL_DIR% -Dprotobuf_MSVC_STATIC_RUNTIME=OFF -Dprotobuf_BUILD_TESTS=OFF

cmake --build . --config Release --target install
```

4. cares
```bat
cd %SRC%
cd third_party/cares/cares
mkdir cmake
cd cmake

cmake .. -G "Visual Studio 14 2015 Win64" -DCMAKE_INSTALL_PREFIX=%INSTALL_DIR%

cmake --build . --config Release --target install
```
5. grpc
```bat
cd %SRC%
mkdir .build
cd .build

cmake .. -G "Visual Studio 14 2015 Win64" -DCMAKE_INSTALL_PREFIX=%INSTALL_DIR% -DOPENSSL_ROOT_DIR=%OPENSSL_DIR% -DZLIB_ROOT=%INSTALL_DIR% -DgRPC_INSTALL=ON -DgRPC_BUILD_TESTS=OFF -DgRPC_PROTOBUF_PROVIDER=package -DgRPC_ZLIB_PROVIDER=package -DgRPC_CARES_PROVIDER=package -DgRPC_SSL_PROVIDER=package -DCMAKE_BUILD_TYPE=Release

cmake --build . --config Release --target install
```

## compiling example with grpc
```bat
cd %SRC%
cd examples/cpp/helloworld
mkdir build
cd build

cmake .. -G "Visual Studio 14 2015 Win64" -DOPENSSL_ROOT_DIR=%OPENSSL_DIR% -DCMAKE_PREFIX_PATH=%INSTALL_DIR%

cmake --build . --config Release
```
