cmake_minimum_required(VERSION 3.1)
set(PROJECT_NAME "train-hog")

project(${PROJECT_NAME} C CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 11)
set(Boost_USE_STATIC_LIBS ON)

find_package(Threads REQUIRED)
find_package(OpenCV REQUIRED)
find_package(Boost 1.60.0 REQUIRED COMPONENTS
    thread system date_time chrono regex filesystem atomic program_options)

include_directories(svmlight)
include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(${Boost_INCLUDE_DIRS})

add_definitions(-D_WIN32_WINNT=_WIN32_WINNT_WS08)

set(HDR_FILES svmlight/svm_learn.h svmlight/svm_common.h svmlight/svmlight.h)
set(SRC_FILES main.cpp svmlight/svm_learn.c svmlight/svm_hideo.c svmlight/svm_common.c)

add_executable(${PROJECT_NAME} ${SRC_FILES} ${HDR_FILES})

target_link_libraries(${PROJECT_NAME}
    ${OpenCV_LIBS}
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT})
