cmake_minimum_required(VERSION 3.1)

project(Qt-Service LANGUAGES CXX)
include(CMake/ProjectOut.cmake)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt5 COMPONENTS Core Network REQUIRED)


if (WIN32)
    file(GLOB SOURCE_CPP
        "src/qtservice.cpp"
        "src/qtunixserversocket.cpp"
        "src/qtunixsocket.cpp"
        "src/qtservice_win.cpp"
    )
else(WIN32)
    file(GLOB SOURCE_CPP
        "src/qtservice.cpp"
        "src/qtunixserversocket.cpp"
        "src/qtunixsocket.cpp"
        "src/qtservice_unix.cpp"
    )
endif(WIN32)

add_library(${PROJECT_NAME} SHARED ${SOURCE_CPP})
target_link_libraries(${PROJECT_NAME} PUBLIC Qt5::Core Qt5::Network)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)


