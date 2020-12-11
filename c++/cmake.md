---
description: Various CMake spells.
---

# CMake

### Copy folders to output directory

```text
add_custom_command(
        TARGET your_target PRE_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/dir_to_copy
        $<TARGET_FILE_DIR:your_target>)

```



