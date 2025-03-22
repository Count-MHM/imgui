# Count_MHM
# 2025/03/03
# 2025/03/22
add_library(imgui STATIC)

target_include_directories(imgui PUBLIC .)
target_include_directories(imgui PUBLIC misc/cpp)

target_sources(imgui PRIVATE
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
		"misc/cpp/imgui_stdlib.h"
		"misc/cpp/imgui_stdlib.cpp"
)
