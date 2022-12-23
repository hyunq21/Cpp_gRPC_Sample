file(GLOB ProtoFiles CONFIGURE_DEPENDS "*.proto")

file(MAKE_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/.src)
set(PROTO_SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/.src")

foreach(file ${ProtoFiles})
    execute_process(
        COMMAND ${Protobuf_PROTOC_EXECUTABLE} -I=${CMAKE_CURRENT_SOURCE_DIR} --grpc_out=${PROTO_SRC_DIR} --plugin=protoc-gen-grpc=${gRPC_TOOL_DIR}/grpc_cpp_plugin.exe ${file} 
        COMMAND ${Protobuf_PROTOC_EXECUTABLE} -I=${CMAKE_CURRENT_SOURCE_DIR} --cpp_out=${PROTO_SRC_DIR} ${file} 
    )
endforeach()

file(GLOB Proto_Gen_SRC CONFIGURE_DEPENDS ".src/*.h" ".src/*.cpp" ".src/*.cc")

add_library(genprotobuf ${Proto_Gen_SRC})
target_include_directories(genprotobuf PUBLIC ${PROTO_SRC_DIR})
target_link_libraries(genprotobuf 
PRIVATE 
    gRPC::gpr 
    gRPC::grpc 
    gRPC::grpc++ 
    gRPC::grpc++_reflection
    #protobuf::libprotoc 
    protobuf::libprotobuf 
    #protobuf::libprotobuf-lite 
)

foreach(file ${ProtoFiles})
    add_custom_command(
        TARGET genprotobuf 
        PRE_BUILD       
        COMMAND ${Protobuf_PROTOC_EXECUTABLE} -I=${CMAKE_CURRENT_SOURCE_DIR} --grpc_out=${PROTO_SRC_DIR} --plugin=protoc-gen-grpc=${gRPC_TOOL_DIR}/grpc_cpp_plugin.exe ${file}
        COMMAND ${Protobuf_PROTOC_EXECUTABLE} -I=${CMAKE_CURRENT_SOURCE_DIR} --cpp_out=${PROTO_SRC_DIR} ${file}
    ) 
endforeach()