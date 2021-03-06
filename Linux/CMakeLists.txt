cmake_minimum_required(VERSION 3.3)

project(JSerial)

add_definitions(-DJSERIAL_LIB)

# You must replace this path according to your system. This is
# the default path for Ubuntu 16.04 64 bits.
include_directories("/usr/lib/jvm/java-1.8.0-openjdk-amd64/include")
include_directories("/usr/lib/jvm/java-1.8.0-openjdk-amd64/include/linux")

add_library(JSerial64 MODULE JSerial.c JSerial.h JNI.c)
add_library(JSerial32 MODULE JSerial.c JSerial.h JNI.c)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3 -std=gnu99")

# Configuration for 32-bits build. You need a multi-lib gcc for this to work.
# On Ubuntu 64, you must install the package libc6-dev-i386.
set_target_properties(JSerial32 PROPERTIES
    OUTPUT_NAME "JSerial"
    COMPILE_FLAGS "-m32"
    LINK_FLAGS "-m32"
    LIBRARY_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/../JSerial-Linux/resources/x86"
)

# Configuration for 64-bits. You need a multi-lib gcc for this to work.
set_target_properties(JSerial64 PROPERTIES
    OUTPUT_NAME "JSerial"
    COMPILE_FLAGS "-m64"
    LINK_FLAGS "-m64"
    LIBRARY_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/../JSerial-Linux/resources/amd64"
)
