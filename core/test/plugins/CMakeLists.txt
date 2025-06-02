# Plugins based on the blocklib generator
gr_add_block_plugin(
  GoodBase
  SOURCES
  good_base_plugin.cpp
  HEADERS
  good_base_plugin.hpp)

if(WIN32)
  target_compile_definitions(GoodBase PRIVATE BUILDING_MYPLUGIN)
endif()

# Ordinary plugins
function(add_non_blocklib_plugin PLUGIN_NAME)
  add_library(${PLUGIN_NAME} MODULE ${PLUGIN_NAME}.cpp)

  if(WIN32)
    target_compile_definitions(${PLUGIN_NAME} PRIVATE BUILDING_MYPLUGIN)
  endif()
  # target_compile_options(${PLUGIN_NAME} PRIVATE -fsanitize=address -Wall)
  target_compile_options(${PLUGIN_NAME} PRIVATE -Wall)

  target_include_directories(${PLUGIN_NAME} PUBLIC ${CMAKE_BINARY_DIR}/include)
  target_link_libraries(${PLUGIN_NAME} PUBLIC gnuradio-options gnuradio-core gnuradio-plugin)
endfunction()

add_non_blocklib_plugin(good_math_plugin)
add_non_blocklib_plugin(good_conversion_plugin)
add_non_blocklib_plugin(bad_plugin)
