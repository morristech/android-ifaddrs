cmake_minimum_required (VERSION 2.8.11)
project (ifaddrs)
add_library (ifaddrs ifaddrs.c)
file(GLOB HEADERS *.h)
install(TARGETS ifaddrs DESTINATION lib/})

install(FILES ${HEADERS} DESTINATION include/)
