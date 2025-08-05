# Use a define passed from platformio.ini to determine the environment
if(DEFINED TIDBYT_ENV_NAME)
    set(ENV_NAME ${TIDBYT_ENV_NAME})
else()
    set(ENV_NAME "tidbyt-gen2-legacy")  # fallback default
endif()

# Set the library path based on the environment
set(TIDBYT_LIB_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../../.pio/libdeps/${ENV_NAME}/ESP32 HUB75 LED MATRIX PANEL DMA Display")

idf_component_register(
    SRCS 
        "${TIDBYT_LIB_PATH}/esp32_i2s_parallel_dma.c"
        "${TIDBYT_LIB_PATH}/ESP32-HUB75-MatrixPanel-I2S-DMA.cpp"
        "${TIDBYT_LIB_PATH}/ESP32-HUB75-MatrixPanel-leddrivers.cpp"
    INCLUDE_DIRS 
        "${TIDBYT_LIB_PATH}"
    REQUIRES driver esp_common
    PRIV_REQUIRES esp_lcd
)

target_compile_options(${COMPONENT_LIB} PUBLIC -DNO_GFX -DNO_FAST_FUNCTIONS)