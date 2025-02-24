add_executable(shinkansen main.cpp)

target_link_libraries(
  shinkansen
  PRIVATE cmake_template::cmake_template_options
          cmake_template::cmake_template_warnings)

target_link_system_libraries(
  shinkansen
  PRIVATE
          CLI11::CLI11
          fmt::fmt
          spdlog::spdlog
          lefticus::tools
          ftxui::screen
          ftxui::dom
          ftxui::component)

target_include_directories(intro PRIVATE "${CMAKE_BINARY_DIR}/include/railroad")
