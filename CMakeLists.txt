cmake_minimum_required(VERSION 3.3)
project(kore)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/includes)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(CC gcc)
set(PREFIX /usr/local)
set(KORE kore)
set(INSTALL_DIR $(PREFIX)/bin)
set(INCLUDE_DIR $(PREFIX)/include/kore)


set(SOURCE_FILES src/kore.c src/accesslog.c src/auth.c src/buf.c src/cli.c src/config.c src/connection.c src/domain.c src/http.c src/mem.c src/msg.c src/module.c src/net.c src/pool.c src/spdy.c src/timer.c src/validator.c src/utils.c src/websocket.c src/worker.c src/zlib_dict.c)

#add_custom_target(clean COMMAND "find . -type f -name \*.o -exec rm {} \ && rm -f $(KORE)")

add_executable(kore ${SOURCE_FILES})