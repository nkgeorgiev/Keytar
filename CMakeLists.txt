cmake_minimum_required(VERSION 3.2)

project(Keytar)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set (ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set (SRC_DIR ${ROOT_DIR}/src)
set (BUILD_DIR ${ROOT_DIR}/build/x64)

include_directories( ${ROOT_DIR}/lib/fftw3 )

set(CMAKE_CXX_STANDARD 11)
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")

link_directories(${ROOT_DIR}/lib/fftw3)

add_executable (keytar ${SRC_DIR}/main.cpp)

target_link_libraries(keytar libfftw3f-3 libfftw3-3 libfftw3l-3 )

set_target_properties(keytar PROPERTIES
                      RUNTIME_OUTPUT_DIRECTORY ${BUILD_DIR})
					  
#add_custom_command(TARGET keytar POST_BUILD ${CMAKE_COMMAND} -E copy ${ROOT_DIR}/lib/fftw3/libfftw3l-3.dll ${BUILD_DIR}/libfftw3l-3.ddl)
add_custom_command(TARGET keytar POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy ${ROOT_DIR}/lib/fftw3/libfftw3-3.dll ${BUILD_DIR}/$<CONFIGURATION>/libfftw3-3.dll)
add_custom_command(TARGET keytar POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy ${ROOT_DIR}/lib/fftw3/libfftw3f-3.dll ${BUILD_DIR}/$<CONFIGURATION>/libfftw3f-3.dll)
add_custom_command(TARGET keytar POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy ${ROOT_DIR}/lib/fftw3/libfftw3l-3.dll ${BUILD_DIR}/$<CONFIGURATION>/libfftw3l-3.dll)

#add_custom_command(TARGET keytar POST_BUILD COMMAND xcopy ${ROOT_DIR}/lib/fftw3/libfftw3-3.dll ${BUILD_DIR}/libfftw3-3.ddl)
#add_custom_command(TARGET keytar POST_BUILD COMMAND xcopy ${ROOT_DIR}/lib/fftw3/libfftw3f-3.dll ${BUILD_DIR}/libfftw3f-3.ddl)