cmake_minimum_required (VERSION 3.18)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# need download vcpkg first 
set(CMAKE_TOOLCHAIN_FILE "~/vcpkg/scripts/buildsystems/vcpkg.cmake" CACHE STRING "Vcpkg toolchain file")

set(flatbuffers_TOOL_DIR "~/vcpkg/installed/arm64-osx/tools/flatbuffers")
set(protobuf_TOOL_DIR "~/vcpkg/installed/arm64-osx/tools/protobuf") #Protobuf_PROTOC_EXECUTABLE
set(gRPC_TOOL_DIR "~/vcpkg/installed/arm64-osx/tools/grpc") #x64-windows

# download pkgs
# [CMD] ./vcpkg install grpc:x64-windows
# [CMD] ./vcpkg install protobuf protobuf:x64-windows
# [CMD] ./vcpkg install protobuf[zlib] protobuf[zlib]:x64-windows
# [CMD] ./vcpkg install flatbuffers

# [CMD] ./vcpkg integrate install

# ref doc. https://sanoj.in/2020/05/07/working-with-grpc-in-windows.html

project ("Grpc_FlatBuffers_Sample")
project ("Grpc_ProtocolBuffers_Sample" LANGUAGES CXX)


# Include sub-projects.
add_subdirectory ("Grpc_FlatBuffers_Sample")
add_subdirectory ("Grpc_ProtocolBuffers_Sample")