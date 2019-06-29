project(rdp)
cmake_minimum_required(VERSION 3.13)

include(FindPkgConfig)
pkg_search_module(RDP REQUIRED rdp)
pkg_search_module(SERIAL_DATAGRAM REQUIRED serial_datagram)
pkg_search_module(CRC32 REQUIRED crc32)

add_executable(rdpos_terminal rdpos_terminal.c)

target_include_directories(rdpos_terminal PUBLIC .)
target_link_libraries(rdpos_terminal rt pthread)

target_include_directories(rdpos_terminal SYSTEM PUBLIC ${CRC32_INCLUDE_DIRS} ${RDP_INCLUDE_DIRS} ${SERIAL_DATAGRAM_INCLUDE_DIRS})
target_link_directories(rdpos_terminal PUBLIC ${CRC32_LIBRARY_DIRS} ${RDP_LIBRARY_DIRS} ${SERIAL_DATAGRAM_LIBRARY_DIRS})
target_link_libraries(rdpos_terminal  ${RDP_LIBRARIES} ${SERIAL_DATAGRAM_LIBRARIES} ${CRC32_LIBRARIES})

install(TARGETS rdpos_terminal RUNTIME DESTINATION bin)
