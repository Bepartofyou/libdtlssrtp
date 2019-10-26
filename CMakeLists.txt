cmake_minimum_required(VERSION 2.8)
project(srtp C)

add_definitions(
    -g
    -O0
    -std=gnu11 
)

set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS} -fPIC)

include_directories(
    /usr/local/opt/openssl/include
)

link_directories(
    /usr/local/opt/openssl/lib
)

set(SOURCES_LIST
    data_sink.h
    dsink_udp.c
    dsink_udp.h
    dtls_srtp.c
    dtls_srtp.h
    example.c
)

add_executable(${PROJECT_NAME} ${SOURCES_LIST})

if(APPLE)
    target_link_libraries(${PROJECT_NAME}
        crypto
        ssl
        z
    )
else(APPLE)
    target_link_libraries(${PROJECT_NAME}
        crypto
        ssl
        dl
        m
        z
        c
    )
endif(APPLE)