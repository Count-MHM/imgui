# Count_MHM
# 2025/03/03
add_library(imgui STATIC)

target_include_directories(imgui PUBLIC .)

target_sources(imgui PRIVATE
		"imconfig.h"
		"imgui.h"
		"imgui.cpp"
		"imgui_draw.cpp"
		"imgui_internal.h"
		"imgui_tables.cpp"
		"imgui_widgets.cpp"
		"imstb_rectpack.h"
		"imstb_textedit.h"
		"imstb_truetype.h"
		"imgui_demo.cpp"
)
