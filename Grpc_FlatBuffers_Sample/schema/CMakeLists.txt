file(GLOB FlatbufFiles CONFIGURE_DEPENDS "*.fbs")


message(${flatbuffers_TOOL_DIR}/flatc.exec --cpp --grpc -o ${CMAKE_CURRENT_SOURCE_DIR}/.src ${FlatbufFiles})


execute_process(
    COMMAND ${flatbuffers_TOOL_DIR}/flatc.exec --cpp --grpc -o ${CMAKE_CURRENT_SOURCE_DIR}/.src ${FlatbufFiles}
) # window -> .exe mac none

file(GLOB Flat_Gen_SRC CONFIGURE_DEPENDS ".src/*.h" ".src/*.cpp" ".src/*.cc")

add_library(genflatbuf ${Flat_Gen_SRC})
target_include_directories(genflatbuf PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/.src)
target_link_libraries(genflatbuf 
PRIVATE 
    gRPC::gpr 
    gRPC::grpc 
    gRPC::grpc++ 
    gRPC::grpc++_reflection
    flatbuffers::flatbuffers
)

add_custom_command(
    TARGET genflatbuf 
    PRE_BUILD 
    COMMAND ${flatbuffers_TOOL_DIR}/flatc.exe --cpp --grpc -o ${CMAKE_CURRENT_SOURCE_DIR}/.src ${FlatbufFiles}
) 