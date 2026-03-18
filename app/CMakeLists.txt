zephyr_include_directories(include)

zephyr_library_named(zmk)

zephyr_linker_sources(SECTIONS include/linker/zmk-behaviors.ld)
zephyr_linker_sources(RODATA include/linker/zmk-events.ld)

if(CONFIG_ZMK_BEHAVIOR_LOCAL_IDS)
  zephyr_linker_sources(DATA_SECTIONS
                        include/linker/zmk-behavior-local-id-map.ld)
endif()

zephyr_syscall_header(${CMAKE_CURRENT_LIST_DIR}/include/drivers/behavior.h)
zephyr_syscall_header(
  ${CMAKE_CURRENT_LIST_DIR}/include/drivers/input_processor.h)
zephyr_syscall_header(${CMAKE_CURRENT_LIST_DIR}/include/drivers/ext_power.h)

zephyr_library_sources(src/stdlib.c)
zephyr_library_sources(src/activity.c)
zephyr_library_sources(src/behavior.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_KSCAN_SIDEBAND_BEHAVIORS
                             src/kscan_sideband_behaviors.c)
zephyr_library_sources(src/matrix_transform.c)
zephyr_library_sources(src/physical_layouts.c)
zephyr_library_sources(src/sensors.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_WPM src/wpm.c)
zephyr_library_sources(src/event_manager.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_PM src/pm.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_EXT_POWER src/ext_power_generic.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_GPIO_KEY_WAKEUP_TRIGGER
                             src/gpio_key_wakeup_trigger.c)
zephyr_library_sources(src/events/activity_state_changed.c)
zephyr_library_sources(src/events/position_state_changed.c)
zephyr_library_sources(src/events/sensor_event.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_WPM src/events/wpm_state_changed.c)
zephyr_library_sources_ifdef(CONFIG_USB_DEVICE_STACK
                             src/events/usb_conn_state_changed.c)
zephyr_library_sources(src/behaviors/behavior_reset.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_EXT_POWER
                             src/behaviors/behavior_ext_power.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_SOFT_OFF
                             src/behaviors/behavior_soft_off.c)
add_subdirectory_ifdef(CONFIG_ZMK_POINTING src/pointing/)
if((NOT CONFIG_ZMK_SPLIT) OR CONFIG_ZMK_SPLIT_ROLE_CENTRAL)
  zephyr_library_sources(src/hid.c)
  zephyr_library_sources(src/behaviors/behavior_key_press.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_KEY_TOGGLE
                               src/behaviors/behavior_key_toggle.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_HOLD_TAP
                               src/behaviors/behavior_hold_tap.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_STICKY_KEY
                               src/behaviors/behavior_sticky_key.c)
  zephyr_library_sources(src/behaviors/behavior_caps_word.c)
  zephyr_library_sources(src/behaviors/behavior_key_repeat.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_MACRO
                               src/behaviors/behavior_macro.c)
  zephyr_library_sources(src/behaviors/behavior_momentary_layer.c)
  zephyr_library_sources(src/behaviors/behavior_mod_morph.c)
  zephyr_library_sources(src/behaviors/behavior_outputs.c)
  zephyr_library_sources(src/behaviors/behavior_toggle_layer.c)
  zephyr_library_sources(src/behaviors/behavior_to_layer.c)
  zephyr_library_sources(src/behaviors/behavior_transparent.c)
  zephyr_library_sources(src/behaviors/behavior_none.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_SENSOR_ROTATE
                               src/behaviors/behavior_sensor_rotate.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_SENSOR_ROTATE_VAR
                               src/behaviors/behavior_sensor_rotate_var.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_SENSOR_ROTATE_COMMON
                               src/behaviors/behavior_sensor_rotate_common.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_MOUSE_KEY_PRESS
                               src/behaviors/behavior_mouse_key_press.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_STUDIO_UNLOCK
                               src/behaviors/behavior_studio_unlock.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_INPUT_TWO_AXIS
                               src/behaviors/behavior_input_two_axis.c)
  zephyr_library_sources(src/combo.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_TAP_DANCE
                               src/behaviors/behavior_tap_dance.c)
  zephyr_library_sources(src/behavior_queue.c)
  zephyr_library_sources(src/conditional_layer.c)
  zephyr_library_sources(src/endpoints.c)
  zephyr_library_sources(src/events/endpoint_changed.c)
  zephyr_library_sources(src/hid_listener.c)
  zephyr_library_sources(src/keymap.c)
  zephyr_library_sources(src/events/layer_state_changed.c)
  zephyr_library_sources(src/events/modifiers_state_changed.c)
  zephyr_library_sources(src/events/keycode_state_changed.c)
  zephyr_library_sources_ifdef(CONFIG_ZMK_HID_INDICATORS src/hid_indicators.c)

  if(CONFIG_ZMK_BLE)
    zephyr_library_sources(src/events/ble_active_profile_changed.c)
    zephyr_library_sources(src/behaviors/behavior_bt.c)
    zephyr_library_sources(src/ble.c)
    zephyr_library_sources(src/hog.c)
  endif()
endif()

zephyr_library_sources_ifdef(CONFIG_ZMK_RGB_UNDERGLOW
                             src/behaviors/behavior_rgb_underglow.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_BACKLIGHT
                             src/behaviors/behavior_backlight.c)

zephyr_library_sources_ifdef(CONFIG_ZMK_BATTERY_REPORTING
                             src/events/battery_state_changed.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_BATTERY_REPORTING src/battery.c)

zephyr_library_sources_ifdef(CONFIG_ZMK_HID_INDICATORS
                             src/events/hid_indicators_changed.c)

zephyr_library_sources_ifdef(CONFIG_ZMK_SPLIT
                             src/events/split_peripheral_status_changed.c)
add_subdirectory_ifdef(CONFIG_ZMK_SPLIT src/split)

zephyr_library_sources_ifdef(CONFIG_USB_DEVICE_STACK src/usb.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_USB src/usb_hid.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_RGB_UNDERGLOW src/rgb_underglow.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_BACKLIGHT src/backlight.c)
zephyr_library_sources_ifdef(CONFIG_ZMK_LOW_PRIORITY_WORK_QUEUE src/workqueue.c)
add_subdirectory(src/display/)
add_subdirectory_ifdef(CONFIG_SETTINGS src/settings/)

if(CONFIG_ZMK_STUDIO_RPC)
  # For some reason this is failing if run from a different sub-file.
  list(APPEND CMAKE_MODULE_PATH ${ZEPHYR_BASE}/modules/nanopb)

  include(nanopb)

  # Turn off the default nanopb behavior
  set(NANOPB_GENERATE_CPP_STANDALONE OFF)

  nanopb_generate_cpp(
    proto_srcs
    proto_hdrs
    RELPATH
    ${ZEPHYR_ZMK_STUDIO_MESSAGES_MODULE_DIR}
    ${ZEPHYR_ZMK_STUDIO_MESSAGES_MODULE_DIR}/proto/zmk/studio.proto
    ${ZEPHYR_ZMK_STUDIO_MESSAGES_MODULE_DIR}/proto/zmk/meta.proto
    ${ZEPHYR_ZMK_STUDIO_MESSAGES_MODULE_DIR}/proto/zmk/core.proto
    ${ZEPHYR_ZMK_STUDIO_MESSAGES_MODULE_DIR}/proto/zmk/behaviors.proto
    ${ZEPHYR_ZMK_STUDIO_MESSAGES_MODULE_DIR}/proto/zmk/keymap.proto)

  zephyr_library_include_directories(${CMAKE_CURRENT_BINARY_DIR})
  zephyr_library_sources(${proto_srcs} ${proto_hdrs})

  add_subdirectory(src/studio)
endif()
zephyr_cc_option(-Wfatal-errors)
