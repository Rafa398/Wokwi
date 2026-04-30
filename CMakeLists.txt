cmake_minimum_required(VERSION 3.13)
project(pico_w_keypad_led_controller C CXX)

# Documentation-oriented scaffold:
# The current firmware source (src/main.cpp) is Arduino-style and depends on <Keypad.h>.
# Build/run it with the Arduino core for RP2040 (or Wokwi Arduino project mode).
# This CMakeLists.txt is included to provide a clean C/C++ repository layout.

add_custom_target(info ALL
  COMMAND ${CMAKE_COMMAND} -E echo "Use Arduino IDE or Wokwi Arduino mode to build src/main.cpp"
)
