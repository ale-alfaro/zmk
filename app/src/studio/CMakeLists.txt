# Copyright (c) 2024 The ZMK Contributors
# SPDX-License-Identifier: MIT

zephyr_linker_sources(DATA_SECTIONS ../../include/linker/zmk-rpc-subsystems.ld)
zephyr_linker_sources(SECTIONS ../../include/linker/zmk-rpc-subsystem-handlers.ld)
zephyr_linker_sources(SECTIONS ../../include/linker/zmk-rpc-subsystem-settings-reset.ld)
zephyr_linker_sources(SECTIONS ../../include/linker/zmk-rpc-event-mappers.ld)
zephyr_linker_sources(SECTIONS ../../include/linker/zmk-rpc-transport.ld)

zephyr_library_sources(msg_framing.c)
zephyr_library_sources(rpc.c)
zephyr_library_sources(core.c)
zephyr_library_sources(behavior_subsystem.c)
zephyr_library_sources(core_subsystem.c)
zephyr_library_sources(keymap_subsystem.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_STUDIO_TRANSPORT_UART uart_rpc_transport.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_STUDIO_TRANSPORT_BLE gatt_rpc_transport.c)
