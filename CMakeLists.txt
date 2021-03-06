cmake_minimum_required (VERSION 2.6)
PROJECT(Tiered-Storage)

SET (CMAKE_CXX_COMPILER /usr/bin/clang++)

SET(CMAKE_CXX_FLAGS_COMMON
    "-std=c++11 \
    -stdlib=libc++")
SET(CMAKE_CXX_FLAGS_DEBUG
    "${CMAKE_CXX_FLAGS_DEBUG} \
    ${CMAKE_CXX_FLAGS_COMMON}")
SET(CMAKE_CXX_FLAGS_RELEASE
    "${CMAKE_CXX_FLAGS_RELEASE} \
    ${CMAKE_CXX_FLAGS_COMMON} \
    -O3")

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake/modules/)

ADD_SUBDIRECTORY(vendor/tbb)
ADD_SUBDIRECTORY(vendor/boost)
ADD_SUBDIRECTORY(vendor/googlebenchmark)
ADD_SUBDIRECTORY(vendor/googletest)
ADD_SUBDIRECTORY(vendor/zeromq)
ADD_SUBDIRECTORY(vendor/zeromqcpp)

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})
INCLUDE_DIRECTORIES(.)
INCLUDE_DIRECTORIES(include)
INCLUDE_DIRECTORIES(${BOOST_INCLUDE_DIRS})
INCLUDE_DIRECTORIES(${GBENCH_INCLUDE_DIRS})
INCLUDE_DIRECTORIES(${GTEST_INCLUDE_DIRS})
INCLUDE_DIRECTORIES(${ZEROMQCPP_INCLUDE_DIRS})
INCLUDE_DIRECTORIES(${ZEROMQ_INCLUDE_DIRS})
INCLUDE_DIRECTORIES(${TBB_INCLUDE_DIRS})

LINK_DIRECTORIES(${BOOST_LINK_DIRS})
LINK_DIRECTORIES(${ZEROMQ_LINK_DIRS})
LINK_DIRECTORIES(${TBB_LINK_DIRS})

ADD_SUBDIRECTORY(kvs)