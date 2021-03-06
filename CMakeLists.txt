file(GLOB SRCS
	ThirdParty/imgui/*.cpp
	ThirdParty/ImGuizmo/*.cpp
	Src/*.cpp
)

# test cpp files should be automatically gathered by the unittest library
list(FILTER SRCS EXCLUDE REGEX ".*test.cpp")

add_library(bsfImgui SHARED ${SRCS})

add_common_flags(bsfImgui)

# include the thirdparty submodules
target_include_directories(bsfImgui PUBLIC
	ThirdParty/imgui
	ThirdParty/ImGuizmo
)

# disable default osx/win32 functions (we use bsf inputs only)
target_compile_definitions(bsfImgui PUBLIC -DIMGUI_DISABLE_OSX_FUNCTIONS -DIMGUI_DISABLE_WIN32_FUNCTIONS)
# until more standard way for plugins to register their assets
target_compile_definitions(bsfImgui PUBLIC -DCURRENT_SOURCE_DIR="${CMAKE_CURRENT_SOURCE_DIR}")

target_link_libraries(bsfImgui bsf)
