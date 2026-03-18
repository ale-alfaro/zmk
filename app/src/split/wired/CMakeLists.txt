# Copyright (c) 2025 The ZMK Contributors
# SPDX-License-Identifier: MIT

zephyr_library_sources(wired.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_SPLIT_ROLE_CENTRAL central.c)
if (NOT CONFIG_ZMK_SPLIT_ROLE_CENTRAL)
  zephyr_library_sources(peripheral.c)
endif()
