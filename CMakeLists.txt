cmake_minimum_required(VERSION 3.13)

project(uevloop)

set(TEST_NAME test_${PROJECT_NAME})


add_library(${PROJECT_NAME})

# Includes ---------------------------------------------------------------------
include(GNUInstallDirs)
include(CMakePackageConfigHelpers)


target_include_directories(${PROJECT_NAME}
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME}>
        )

target_sources(${PROJECT_NAME}
        PRIVATE
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

add_executable(${TEST_NAME}
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

target_include_directories(${TEST_NAME}
        PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        )

target_link_libraries(${TEST_NAME} ${PROJECT_NAME})

#set(${PROJECT_NAME}_PUBLIC_HEADERS include/uevloop/config.h)
#
#set_target_properties(${PROJECT_NAME}
#        PROPERTIES
#        C_STANDARD          11
#        C_STANDARD_REQUIRED ON
#        C_EXTENSIONS        OFF
#        #PUBLIC_HEADER       "${${PROJECT_NAME}_PUBLIC_HEADERS}"
#        EXPORT_NAME         framework
#        )


## Target installation
install(TARGETS   ${PROJECT_NAME}
        EXPORT        ${PROJECT_NAME}Targets
        ARCHIVE       DESTINATION ${CMAKE_INSTALL_LIBDIR}
        LIBRARY       DESTINATION ${CMAKE_INSTALL_LIBDIR}
        PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME}
        COMPONENT     library
        )

message("bbb" ${CMAKE_INSTALL_INCLUDEDIR})
message("ccc ${CMAKE_INSTALL_LIBDIR}")
get_property(out TARGET ${PROJECT_NAME} PROPERTY INTERFACE_INCLUDE_DIRECTORIES)
message("SOURCES OUT ${out}")
message("interface sources ${INTERFACE_SOURCES}")

## Target's cmake files: targets export
install(EXPORT  ${PROJECT_NAME}Targets
        NAMESPACE   ${PROJECT_NAME}::
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
        )

## Target's cmake files: config and version config for find_package()
install(FILES   ${PROJECT_NAME}Config.cmake
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
        )
