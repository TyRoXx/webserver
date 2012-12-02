cmake_minimum_required(VERSION 2.8)

project(webserver)

if(MSVC)
	set(WEBSERVER_WITH_VLD false CACHE BOOL "Visual Leak Detector, finds memory leaks with Visual C++ (vld.codeplex.com)")
	add_definitions("/wd4996") #'Funktion': wurde als veraltet deklariert
	add_definitions("/we4013") #behandelt Warnung "'..' undefined; assuming extern returning int" als Fehler
	add_definitions("/WX")
endif(MSVC)

if(CMAKE_COMPILER_IS_GNUCXX)
	set(flags "-g -Wall -Wconversion -Wextra -ansi")
	set(flags "${flags} -Wno-unused-parameter")
	set(flags "${flags} -Wno-missing-field-initializers")
	#set(flags "${flags} -pedantic")
	set(CMAKE_C_FLAGS ${flags})
endif()

if("${CMAKE_C_COMPILER_ID}" STREQUAL "Clang")
	message("Using Clang")
	set(flags "-g -Wall -Wconversion -Wextra")
	set(flags "${flags} -Wno-unused-parameter")
	set(flags "${flags} -Wno-missing-field-initializers")
	set(flags "${flags} -pedantic")
	set(CMAKE_C_FLAGS ${flags})
endif()

find_package(Lua51)
if(NOT LUA51_FOUND)
	message(FATAL_ERROR "Lua 5.1 required")
endif()

include_directories(.)

add_subdirectory(common)
add_subdirectory(http)
add_subdirectory(sub_directory)
add_subdirectory(file_system)
add_subdirectory(lua_script)
add_subdirectory(test)
add_subdirectory(webserver)
add_subdirectory(empty_plugin)
