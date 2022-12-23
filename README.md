## [CPP/cmake] gRPC sample
gRPC + Protocol Buffer sample & gRPC + FlatBuffers sample


### How to Use

1. need download vcpkg first 

2. open Cpp_gRPC_Sample/CMakeLists.txt and set CMAKE_TOOLCHAIN_FILE, flatbuffers_TOOL_DIR, gRPC_TOOL_DIR 

3. download pkgs
```Shell
./vcpkg install grpc:x64-windows
./vcpkg install protobuf protobuf:x64-windows
./vcpkg install protobuf[zlib] protobuf[zlib]:x64-windows
./vcpkg install flatbuffers

./vcpkg integrate install
```








ref doc. https://sanoj.in/2020/05/07/working-with-grpc-in-windows.html

