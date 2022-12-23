find_package(gRPC CONFIG REQUIRED)
find_package(flatbuffers CONFIG REQUIRED)

add_subdirectory (schema)

add_executable(gRPC_flatbuffers_server 
    "src/server.cc" 
)
target_link_libraries(gRPC_flatbuffers_server 
PUBLIC
    genflatbuf
PRIVATE 
    gRPC::gpr 
    gRPC::grpc 
    gRPC::grpc++ 
    gRPC::grpc++_reflection
    flatbuffers::flatbuffers
)


add_executable(gRPC_flatbuffers_client 
    "src/client.cc" 
)
target_link_libraries(gRPC_flatbuffers_client 
PUBLIC
    genflatbuf
PRIVATE 
    gRPC::gpr 
    gRPC::grpc 
    gRPC::grpc++ 
    gRPC::grpc++_reflection
    flatbuffers::flatbuffers
)