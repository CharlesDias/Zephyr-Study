# Copyright (c) 2021 Nordic Semiconductor ASA
# SPDX-License-Identifier: Apache-2.0
#
# This CMake file is picked by the Zephyr build system because it is defined
# as the module CMake entry point (see zephyr/module.yml).

# This is necessary for Sonarlint tools
# If enabled, generates a compile_commands.json file containing the exact compiler calls for all 
# translation units of the project in machine-readable form.
# Note: This option currently does not work well in combination with the UNITY_BUILD target 
# property or the CMAKE_UNITY_BUILD variable.
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

zephyr_include_directories(include)

add_subdirectory(drivers)
add_subdirectory(lib)
