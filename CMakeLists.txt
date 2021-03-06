cmake_minimum_required(VERSION 3.8)
project(ss)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_CXX_FLAGS -Wall)
set(CMAKE_BUILD_TYPE Debug CACHE STRING "set build type to debug")
#set(CMAKE_BUILD_TYPE Release CACHE STRING "set build type to Release")

if (NOT (${CMAKE_BUILD_TYPE} MATCHES "Debug"))
    set(CMAKE_CXX_FLAGS -O3)
endif ()

file(GLOB SRCS "*.h" "*.cpp" "*.qrc")

find_package(PkgConfig REQUIRED)
find_package(Qt5 REQUIRED Core Gui Widgets Network DBus)
pkg_check_modules(QtShadowsocks REQUIRED QtShadowsocks)
pkg_check_modules(Botan REQUIRED botan-1.10)
pkg_check_modules(DtkBase REQUIRED dtkbase)
pkg_check_modules(DtkWidget REQUIRED dtkwidget)
pkg_check_modules(DFrameworkDBus REQUIRED dframeworkdbus)
add_executable(ss ${SRCS})
target_include_directories(ss PUBLIC
        ${QtShadowsocks_INCLUDE_DIRS}
        ${Botan_INCLUDE_DIRS}
        ${DtkBase_INCLUDE_DIRS}
        ${DtkWidget_INCLUDE_DIRS}
        ${DFrameworkDBus_INCLUDE_DIRS}
        )
target_link_libraries(ss
        ${QtShadowsocks_LIBRARIES}
        ${Botan_LIBRARIES}
        ${DtkBase_LIBRARIES}
        ${DtkWidget_LIBRARIES}
        ${DFrameworkDBus_LIBRARIES}
        )
qt5_use_modules(${PROJECT_NAME} Core Gui Widgets Network DBus)