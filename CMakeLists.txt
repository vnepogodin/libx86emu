cmake_minimum_required(VERSION 3.6)

project(x86emu
        VERSION 3.5
        LANGUAGES C)

include(GNUInstallDirs)

set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -flto")

if(CMAKE_C_COMPILER_ID STREQUAL "GNU")
   set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -fwhole-program -fuse-linker-plugin")
endif()

###
### x86emu library
###

set(LIB_SOURCES
    api.c
    decode.c
    mem.c
    ops2.c
    ops.c
    prim_ops.c
)

include_directories(${CMAKE_CURRENT_PROJECT_DIR}/include)

add_library(x86emu STATIC ${LIB_SOURCES})
add_library(x86emu::x86emu ALIAS x86emu)

install(TARGETS x86emu
  LIBRARY DESTINATION lib
)
