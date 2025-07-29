# Count_MHM
# 2025/03/03
# 2025/03/22
# 2025/07/29
add_library(imgui STATIC)

file(WRITE user_config.h "#pragma once\n")

option(IMGUI_ENABLE_CPP_STDLIB_ADDON "Enable wrappers for STL" ON)
option(IMGUI_ENABLE_FREETYPE "Allow ImGui to use FreeType" OFF)
option(IMGUI_ENABLE_FREETYPE_PLUTOSVG "Allow ImGui to use FreeType" OFF)

set(IMGUI_SOURCES
	"imconfig.h"
	"imgui_demo.cpp"
	"imgui_draw.cpp"
	"imgui_internal.h"
	"imgui_tables.cpp"
	"imgui_widgets.cpp"
	"imgui.cpp"
	"imgui.h"
	"imstb_rectpack.h"
	"imstb_textedit.h"
	"imstb_truetype.h"
)
set(IMGUI_INCLUDES
	"."
)

if (IMGUI_ENABLE_CPP_STDLIB_ADDON)
	list(APPEND IMGUI_SOURCES
		"misc/cpp/imgui_stdlib.h"
		"misc/cpp/imgui_stdlib.cpp"
	)
	list(APPEND IMGUI_INCLUDES
		"misc/cpp"
	)
endif()

if (IMGUI_ENABLE_FREETYPE)
	list(APPEND IMGUI_SOURCES
		"misc/freetype/imgui_freetype.h"
		"misc/freetype/imgui_freetype.cpp"
	)
	set(APPEND IMGUI_INCLUDES
		"misc/freetype"
	)
	if (TARGET freetype)
		target_link_libraries(imgui PRIVATE freetype)
	else()
		message(FATAL_ERROR "Cannot find freetype")
	endif()
	file(APPEND user_config.h "#define IMGUI_ENABLE_FREETYPE\n")

	if(IMGUI_ENABLE_FREETYPE_PLUTOSVG)
		if (TARGET plutosvg::plutosvg)
			target_link_libraries(imgui PRIVATE plutosvg::plutosvg)
		else()
			message(FATAL_ERROR "Cannot find plutosvg")
		endif()
		file(APPEND user_config.h "#define IMGUI_ENABLE_FREETYPE_PLUTOSVG\n")
	endif()
endif()

target_include_directories(imgui PUBLIC 
	${IMGUI_INCLUDES}
)
target_sources(imgui PRIVATE
	${IMGUI_SOURCES}
)

target_compile_definitions(imgui PUBLIC IMGUI_USER_CONFIG="user_config.h")
