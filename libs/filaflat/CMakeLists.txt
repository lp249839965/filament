cmake_minimum_required(VERSION 3.1)
project(filaflat)

set(TARGET         filaflat)
set(PUBLIC_HDR_DIR include)

# ==================================================================================================
# Sources and headers
# ==================================================================================================
file(GLOB_RECURSE HDRS include/filaflat/*.h)

set(SRCS
        src/ChunkContainer.cpp
        src/ChunkInterfaceBlock.cpp
        src/TextDictionaryReader.cpp
        src/SpirvDictionaryReader.cpp
        src/MaterialChunk.cpp
        src/ShaderBuilder.cpp
        src/MaterialParser.cpp
        src/Unflattener.cpp)

# ==================================================================================================
# Include and target definitions
# ==================================================================================================
include_directories(${PUBLIC_HDR_DIR})

add_library(${TARGET} ${HDRS} ${SRCS})
target_include_directories(${TARGET} PUBLIC ${PUBLIC_HDR_DIR})

target_link_libraries(${TARGET} filabridge utils)

# ==================================================================================================
# Compiler flags
# ==================================================================================================
target_compile_options(${TARGET} PRIVATE
        -fvisibility=hidden
        $<$<PLATFORM_ID:Linux>:-fPIC>
)

# ==================================================================================================
# Installation
# ==================================================================================================
install(DIRECTORY ${PUBLIC_HDR_DIR}/filaflat DESTINATION include)
install(TARGETS ${TARGET} ARCHIVE DESTINATION lib/${DIST_DIR})
