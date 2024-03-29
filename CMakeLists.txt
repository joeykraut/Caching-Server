cmake_minimum_required(VERSION 3.10)

project(Caching-Server C)

# Server executable
set(
        SERVER_SOURCES
        src/server/server.c
        src/server/server_utils.c
        src/kv_store/kv_store.c
        src/kv_store/lock_manager.c
        src/server/thread_pool.c
        hashmap/hashmap.c
        include/types.h
)

add_executable(server ${SERVER_SOURCES})
target_include_directories(
        server PRIVATE
        include
        hashmap
        src/kv_store
)

# Client executable
set(
        CLIENT_SOURCES
        src/client/client.c
        include/types.h
)

add_executable(client ${CLIENT_SOURCES})
target_include_directories(client PRIVATE include)

# Testing executable
set(
        TEST_SOURCES
        src/test/test_all.c
        src/test/helpers.c
        src/test/kv_store/test_kv_store.c

        hashmap/hashmap.c
        src/kv_store/kv_store.c
        src/kv_store/lock_manager.c
)

add_executable(test ${TEST_SOURCES})
target_include_directories(
        test PRIVATE
        include
        hashmap
        src/test
        src/kv_store
)

