cmake_minimum_required(VERSION 3.12)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project(vspcplay)

add_subdirectory("third_party/sdl2" EXCLUDE_FROM_ALL)

add_executable(vspcplay
	"apu.cpp"
	"apu.h"
	"apumem.h"
	"font.c"
	"font.h"
	"getopt.h"
	"globals.cpp"
	"id666.c"
	"id666.h"
	"libspc.cpp"
	"libspc.h"
	"main.c"
	"memmap.h"
	"port.h"
	"report.h"
	"sdlfont.c"
	"sdlfont.h"
	"snes9x.h"
	"soundux.cpp"
	"spc_structs.h"
	"spc700.cpp"
	"spc700.h"
	"wavewriter.c"
	"wavewriter.h"  )

if(TARGET SDL2::SDL2main)
    target_link_libraries(vspcplay PRIVATE SDL2::SDL2main)
endif()

target_link_libraries(vspcplay PRIVATE SDL2::SDL2)

target_compile_definitions(vspcplay PRIVATE "VERSION_STR=\"1.5\"")