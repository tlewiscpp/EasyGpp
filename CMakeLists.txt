#CMakeLists.txt -> EasyGpp

cmake_minimum_required (VERSION 3.1) 
project(EasyGpp CXX)

set(CMAKE_BUILD_TYPE Release)
set(SOURCE_BASE ${CMAKE_CURRENT_SOURCE_DIR})
set(CMAKE_CXX_STANDARD 14)

if (CMAKE_SYSTEM_PROCESSOR MATCHES "(x86)|(X86)|(amd64)|(AMD64)")
    set (X86 TRUE)
else()
    set (X86 FALSE)
endif()

if (CYGWIN OR WIN32 OR (NOT X86))
    set(GCC_ADDITIONAL_COMPILE_FLAGS "")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GCC_ADDITIONAL_COMPILE_FLAGS}")
else()
    set(GCC_ADDITIONAL_COMPILE_FLAGS "-fsanitize=undefined -frecord-gcc-switches")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GCC_ADDITIONAL_COMPILE_FLAGS}")
endif()

include_directories("${SOURCE_BASE}/include")

set (EASYGPP_SOURCES "${SOURCE_BASE}/src/easygpp.cpp"
                     "${SOURCE_BASE}/src/configurationfilereader.cpp"
                     "${SOURCE_BASE}/src/easygppstrings.cpp")

add_executable(easyg++ ${EASYGPP_SOURCES})
target_link_libraries(easyg++ tjlutils pthread)
