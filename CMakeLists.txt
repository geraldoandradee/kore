cmake_minimum_required(VERSION 3.3)
project(kore)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/includes /usr/include/openssl)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c++11")

set(CC gcc)
set(PREFIX /usr/local)
set(KORE kore)
set(INSTALL_DIR $(PREFIX)/bin)
set(INCLUDE_DIR $(PREFIX)/include/kore)

IF(APPLE)
    set(CMAKE_C_FLAGS "-I/opt/local/include/ -I/usr/local/opt/openssl/include")
    find_library(openssl "-L/opt/local/lib -L/usr/local/opt/openssl/lib")
    set(SOURCE_FILES "src/bsd.c")
ELSEIF(UNIX)
    set(CMAKE_C_FLAGS "-D_GNU_SOURCE=1")
    find_library(openssl "/usr/lib64/openssl")
    set(SOURCE_FILES "src/linux.c")
#    INCLUDE_DIRECTORIES(/usr/include/openssl)
    set(OPENSSL_ROOT_DIR /usr/lib64/openssl)
#    set(OPENSSL_LIBRARIES /usr/lib64/openssl/engines)
#    set(CMAKE_EXE_LINKER_FLAGS "-L/usr/lib64 -L/usr/lib -L/usr/lib64/openssl")
    find_package(OpenSSL)
ELSE()
    set(SOURCE_FILES "src/bsd.c")
ENDIF()

set(SOURCE_FILES ${SOURCE_FILES} src/kore.c src/accesslog.c src/auth.c src/buf.c src/cli.c src/config.c src/connection.c src/domain.c src/http.c src/mem.c src/msg.c src/module.c src/net.c src/pool.c src/spdy.c src/timer.c src/validator.c src/utils.c src/websocket.c src/worker.c src/zlib_dict.c)

#add_custom_target(clean COMMAND "find . -type f -name \*.o -exec rm {} \ && rm -f $(KORE)")

add_executable(kore ${SOURCE_FILES})




