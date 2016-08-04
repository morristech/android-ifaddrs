cmake_minimum_required(VERSION 3.0.0)

set(CMAKE_C_FLAGS "" CACHE STRING "Common C Flags")
set(CMAKE_C_FLAGS_DEBUG "-g -O0" CACHE STRING "Debug C Flags")
set(CMAKE_C_FLAGS_MINSIZEREL "-Os" CACHE STRING "Minimum-size Release C Flags")
set(CMAKE_C_FLAGS_RELEASE "-O2" CACHE STRING "Release C Flags")
set(CMAKE_C_FLAGS_RELWITHDEBINFO "-g -O2" CACHE STRING "Release with Debug Info C Flags")

set(CMAKE_C_COMPILER arm-linux-androideabi-gcc CACHE STRING "Compiler")

project(AndroidIfaddrs)

if(NOT TARGET ifaddrs)
	set(IFADDRS_LINKING_TYPE "STATIC" CACHE STRING "Set to SHARED to build dynamic library")
	set(IFADDRS_EXPORT_CONTROLS OFF CACHE STRING "Set to ON to build export controls")

	add_library(ifaddrs ${IFADDRS_LINKING_TYPE} ifaddrs.c)
	target_compile_definitions(ifaddrs PRIVATE _FORTIFY_SOURCE=2)
	target_compile_options(ifaddrs PRIVATE -pie -fstack-protector)
	install(TARGETS ifaddrs EXPORT ifaddrs DESTINATION lib)
	
	install(FILES ifaddrs.h DESTINATION include)
	
	if(IFADDRS_EXPORT_CONTROLS)
		install(EXPORT ifaddrs DESTINATION lib)
	endif()
endif()
