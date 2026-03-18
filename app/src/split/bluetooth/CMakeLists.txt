# Copyright (c) 2022 The ZMK Contributors
# SPDX-License-Identifier: MIT

if (NOT CONFIG_ZMK_SPLIT_ROLE_CENTRAL)
  zephyr_library_sources(service.c)
  zephyr_library_sources(peripheral.c)
endif()
if (CONFIG_ZMK_SPLIT_ROLE_CENTRAL)
  zephyr_library_sources(central.c)
endif()

if (CONFIG_ZMK_SPLIT_BLE_CENTRAL_BATTERY_LEVEL_PROXY)
  zephyr_library_sources(central_bas_proxy.c)
endif()
