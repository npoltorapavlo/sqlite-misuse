cmake_minimum_required(VERSION 3.14)

project(l1test)

set(CMAKE_CXX_STANDARD 11)

include(FetchContent)
FetchContent_Declare(
        googletest
        URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)
FetchContent_MakeAvailable(googletest)

add_executable(${PROJECT_NAME}
        OpenDbTest.cpp
        OpenDbWithEmptyJournalTest.cpp
        OpenExistingDbTest.cpp
        DbInRuntimeTest.cpp
)

target_link_libraries(${PROJECT_NAME} PRIVATE
        gmock_main
)

find_package(PkgConfig REQUIRED)
pkg_search_module(SQLITE REQUIRED sqlite3)
target_link_libraries(${PROJECT_NAME} PRIVATE ${SQLITE_LIBRARIES})

install(TARGETS ${PROJECT_NAME} DESTINATION bin)
