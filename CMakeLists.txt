cmake_minimum_required(VERSION 3.20)
project(zmk-workspace LANGUAGES C CXX)

# This CMakeLists.txt is for CLion IDE support only.
# The actual build is done via West/Zephyr build system using:
#   just build <target>
#
# To get full IDE support in CLion:
# 1. Build a target first: just build crosses
# 2. In CLion: Settings -> Build -> CMake -> Add
# 3. Set "Build directory" to one of the build dirs (e.g., .build/crosses_left-nice_nano)
# 4. CLion will use the compile_commands.json from that directory

# Set paths for IDE indexing
set(ZEPHYR_BASE "${CMAKE_CURRENT_SOURCE_DIR}/zephyr" CACHE PATH "Zephyr base")
set(ZMK_APP "${CMAKE_CURRENT_SOURCE_DIR}/zmk/app" CACHE PATH "ZMK app")
set(ZMK_CONFIG "${CMAKE_CURRENT_SOURCE_DIR}/config" CACHE PATH "ZMK config")

# Include directories for IDE code completion
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/config
    ${CMAKE_CURRENT_SOURCE_DIR}/zmk/app/include
    ${CMAKE_CURRENT_SOURCE_DIR}/zephyr/include
    ${CMAKE_CURRENT_SOURCE_DIR}/zephyr/soc/common/include
    ${CMAKE_CURRENT_SOURCE_DIR}/modules/hal/nordic/nrfx
    ${CMAKE_CURRENT_SOURCE_DIR}/modules/hal/nordic/nrfx/mdk
    ${CMAKE_CURRENT_SOURCE_DIR}/modules/hal/nordic/nrfx/drivers/include
    ${CMAKE_CURRENT_SOURCE_DIR}/modules/lib/zcbor/include
    ${CMAKE_CURRENT_SOURCE_DIR}/modules/crypto/tinycrypt/lib/include
    ${CMAKE_CURRENT_SOURCE_DIR}/modules/zmk/helpers/include
)

# Collect source files for IDE indexing (not for actual compilation)
file(GLOB_RECURSE CONFIG_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/config/*.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/config/*.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/config/*.dtsi"
    "${CMAKE_CURRENT_SOURCE_DIR}/config/*.keymap"
    "${CMAKE_CURRENT_SOURCE_DIR}/config/*.conf"
)

file(GLOB_RECURSE ZMK_APP_SOURCES
    "${ZMK_APP}/src/*.c"
    "${ZMK_APP}/include/*.h"
)

# Add sources to a custom target for IDE visibility
add_custom_target(zmk-ide-index SOURCES
    ${CONFIG_SOURCES}
    ${ZMK_APP_SOURCES}
)

# Compiler definitions for IDE parsing
add_compile_definitions(
    __ZEPHYR__=1
    CONFIG_ARM=1
    CONFIG_SOC_SERIES_NRF52X=1
    CONFIG_BT=1
    CONFIG_ZMK_BLE=1
)
