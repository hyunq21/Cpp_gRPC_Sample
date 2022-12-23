find_package(gRPC CONFIG REQUIRED)
find_package(Protobuf REQUIRED)

add_subdirectory (schema)

add_executable(gRPC_ProtoBuffers_server "src/server.cc" )
target_link_libraries(gRPC_ProtoBuffers_server 
PUBLIC
    genprotobuf 
PRIVATE 
    gRPC::gpr 
    gRPC::grpc 
    gRPC::grpc++ 
    gRPC::grpc++_reflection
    #protobuf::libprotoc 
    protobuf::libprotobuf 
    #protobuf::libprotobuf-lite 
)


add_executable(gRPC_ProtoBuffers_client "src/client.cc" )
target_link_libraries(gRPC_ProtoBuffers_client 
PUBLIC
    genprotobuf
PRIVATE 
    gRPC::gpr
    gRPC::grpc 
    gRPC::grpc++ 
    gRPC::grpc++_reflection 
    #protobuf::libprotoc 
    protobuf::libprotobuf 
    #protobuf::libprotobuf-lite 
)