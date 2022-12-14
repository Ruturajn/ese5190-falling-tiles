# cmake version
cmake_minimum_required(VERSION 3.13)

# include the sdk.cmake file
include(pico_sdk_import.cmake)

# give the project a name (anything you want)
project(vga-graphics-project)

# initialize the sdk
pico_sdk_init()

#######

# name anything you want
add_executable(graphics_test)

# must match with pio filename and executable name from above
pico_generate_pio_header(graphics_test ${CMAKE_CURRENT_LIST_DIR}/hsync.pio)
pico_generate_pio_header(graphics_test ${CMAKE_CURRENT_LIST_DIR}/vsync.pio)
pico_generate_pio_header(graphics_test ${CMAKE_CURRENT_LIST_DIR}/rgb.pio)

# must match with executable name and source file names
target_sources(graphics_test PRIVATE vga_graphics_demo.c vga_graphics.c)

# must match with executable name
target_link_libraries(graphics_test PRIVATE pico_stdlib hardware_pio hardware_dma hardware_adc hardware_irq)

# must match with executable name
pico_add_extra_outputs(graphics_test)
