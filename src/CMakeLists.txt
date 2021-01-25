# Define a library for the FreeRTOS kernel.
add_library(
  FreeRTOS
  croutine.c
  event_groups.c
  list.c
  queue.c
  stream_buffer.c
  tasks.c
  timers.c)

# Include the kernel header files.
target_include_directories(FreeRTOS PUBLIC include)

# Create a library for each dynamic memory heap implementation.
add_library(FreeRTOS_heap_1 EXCLUDE_FROM_ALL portable/MemMang/heap_1.c)
add_library(FreeRTOS_heap_2 EXCLUDE_FROM_ALL portable/MemMang/heap_2.c)
add_library(FreeRTOS_heap_3 EXCLUDE_FROM_ALL portable/MemMang/heap_3.c)
add_library(FreeRTOS_heap_4 EXCLUDE_FROM_ALL portable/MemMang/heap_4.c)
add_library(FreeRTOS_heap_5 EXCLUDE_FROM_ALL portable/MemMang/heap_5.c)

# Link each heap library to the FreeRTOS kernel.
target_link_libraries(FreeRTOS_heap_1 PRIVATE FreeRTOS)
target_link_libraries(FreeRTOS_heap_2 PRIVATE FreeRTOS)
target_link_libraries(FreeRTOS_heap_3 PRIVATE FreeRTOS)
target_link_libraries(FreeRTOS_heap_4 PRIVATE FreeRTOS)
target_link_libraries(FreeRTOS_heap_5 PRIVATE FreeRTOS)

# Create a library for the mpu_wrappers.c source file.
add_library(FreeRTOS_mpu_wrappers EXCLUDE_FROM_ALL portable/Common/mpu_wrappers.c)

# Link the MPU specific library to the FreeRTOS kernel.
target_link_libraries(FreeRTOS_mpu_wrappers PRIVATE FreeRTOS)
