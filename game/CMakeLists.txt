#
# Executable variables
#
file(GLOB_RECURSE GAME_SRCS
    ${CMAKE_CURRENT_LIST_DIR}/*.c
    ${CMAKE_CURRENT_LIST_DIR}/*.h
)

#
# Executable definition
#
add_library(QuakeGame SHARED ${GAME_SRCS})

set_target_properties(QuakeGame PROPERTIES OUTPUT_NAME "${QUAKE_GAME_NAME}")