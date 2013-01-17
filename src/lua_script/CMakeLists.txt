file(GLOB sources
	"*.c"
	"*.h")

include_directories(${LUA_INCLUDE_DIR})

add_library(lua_script ${sources})

target_link_libraries(lua_script ${LUA_LIBRARIES})
