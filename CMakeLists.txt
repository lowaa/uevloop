cmake_minimum_required(VERSION 3.13)

project(uevloop)

add_library(libuevloop)

target_include_directories(libuevloop
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/include
        )

target_sources(libuevloop
        PUBLIC
        src/system/containers/application.c
        src/system/containers/system-pools.c
        src/system/containers/system-queues.c
        src/system/event.c
        src/system/event-loop.c
        src/system/scheduler.c
        src/system/signal.c
        src/utils/automatic-pool.c
        src/utils/circular-queue.c
        src/utils/closure.c
        src/utils/conditional.c
        src/utils/functional.c
        src/utils/iterator.c
        src/utils/linked-list.c
        src/utils/module.c
        src/utils/object-pool.c
        src/utils/pipeline.c
        src/utils/promise.c
        )

add_executable(test_libuevloop
        test/test.c
        test/system/containers/application.c
        test/system/containers/system-queues.c
        test/system/containers/system-pools.c
        test/system/event.c
        test/system/event-loop.c
        test/system/scheduler.c
        test/system/signal.c
        test/utils/automatic-pool.c
        test/utils/circular-queue.c
        test/utils/closure.c
        test/utils/conditional.c
        test/utils/functional.c
        test/utils/iterator.c
        test/utils/linked-list.c
        test/utils/module.c
        test/utils/object-pool.c
        test/utils/pipeline.c
        test/utils/promise.c
        )

target_include_directories(test_libuevloop
        PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        )

target_link_libraries(test_libuevloop libuevloop)