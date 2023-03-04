# Set minimum required version of CMake
cmake_minimum_required(VERSION 3.24)

# Include build functions from Pico SDK
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)

# Include pico-extras
include($ENV{PICO_EXTRAS_PATH}/external/pico_extras_import.cmake)

# Set name of project (as PROJECT_NAME) and C/C++ standards
project(blink C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Creates a pico-sdk subdirectory in our project for the libraries
pico_sdk_init()

# Tell CMake where to find the executable source file
add_executable(${PROJECT_NAME} main.c)

# Link to pico_stdlib (gpio, time, etc. functions)
target_link_libraries(${PROJECT_NAME} pico_stdlib pico_audio_i2s)

target_compile_definitions(
  ${PROJECT_NAME}
  PRIVATE # compile time configuration of I2S
          PICO_AUDIO_I2S_MONO_INPUT=1
          # define for our example code
          USE_AUDIO_I2S=1
        #   PICO_AUDIO_I2S_DATA_PIN=24
        #   PICO_AUDIO_I2S_CLOCK_PIN_BASE=25
        #   PICO_DEFAULT_UART=0
        #   PICO_DEFAULT_UART_TX_PIN=28
        #   PICO_DEFAULT_UART_RX_PIN=29
)
# create map/bin/hex file etc.
pico_add_extra_outputs(${PROJECT_NAME})

# Enable usb output, disable uart output
pico_enable_stdio_usb(${PROJECT_NAME} 0)
pico_enable_stdio_uart(${PROJECT_NAME} 1)
