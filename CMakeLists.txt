cmake_minimum_required(VERSION 3.1)
project(SDL_FontCache VERSION 0.10.0 LANGUAGES C)

find_path(sdl2_INCLUDE_DIR SDL.h)
find_library(sdl2_LIBRARY SDL2)
find_path(sdl2_ttf_INCLUDE_DIR SDL_ttf.h)
find_library(sdl2_ttf_LIBRARY SDL2_ttf)
find_path(sdl2_gpu_INCLUDE_DIR SDL_gpu.h)
find_library(sdl2_gpu_LIBRARY SDL2_gpu)

if (NOT sdl2_INCLUDE_DIR)
    message(FATAL_ERROR "SDL2 include dir not found")
endif()
if (NOT sdl2_LIBRARY)
    message(FATAL_ERROR "SDL2 library dir not found")
endif()
if (NOT sdl2_ttf_INCLUDE_DIR)
    message(FATAL_ERROR "SDL2_TTF include dir not found")
endif()
if (NOT sdl2_ttf_LIBRARY)
    message(FATAL_ERROR "SDL2_TTF library dir not found")
endif()
if (NOT sdl2_gpu_INCLUDE_DIR)
    message(FATAL_ERROR "SDL_gpu include dir not found")
endif()
if (NOT sdl2_gpu_LIBRARY)
    message(FATAL_ERROR "SDL_gpu library dir not found")
endif()

add_definitions(-DFC_USE_SDL_GPU)

add_library(SDL_FontCache
    SDL_FontCache.h
    SDL_FontCache.c
)

target_include_directories(SDL_FontCache PUBLIC ${sdl2_INCLUDE_DIR})
target_include_directories(SDL_FontCache PUBLIC .)
target_link_libraries(SDL_FontCache ${sdl2_LIBRARY})
target_include_directories(SDL_FontCache PUBLIC ${sdl2_ttf_INCLUDE_DIR})
target_link_libraries(SDL_FontCache ${sdl2_ttf_LIBRARY})
target_include_directories(SDL_FontCache PUBLIC ${sdl2_gpu_INCLUDE_DIR})
target_link_libraries(SDL_FontCache ${sdl2_gpu_LIBRARY})

install(TARGETS SDL_FontCache DESTINATION lib)
install(FILES SDL_FontCache.h DESTINATION include/SDL2)
