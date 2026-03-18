# Copyright (c) 2020 The ZMK Contributors
# SPDX-License-Identifier: MIT

zephyr_library_sources_ifdef(CONFIG_ZMK_DISPLAY main.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_DISPLAY_STATUS_SCREEN_BUILT_IN status_screen.c)

add_subdirectory_ifdef(CONFIG_ZMK_DISPLAY widgets/)
