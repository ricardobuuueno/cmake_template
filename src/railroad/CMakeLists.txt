include(GenerateExportHeader)

add_library(railroad building.cpp
                     carriage.cpp 
                     depot.cpp
                     line.cpp
                     locomotive.cpp 
                     section.cpp
                     station.cpp
                     system.cpp 
                     terminal.cpp
                     track.cpp 
                     train.cpp)

add_library(cmake_template::railroad ALIAS railroad)

target_link_libraries(railroad PRIVATE cmake_template_options cmake_template_warnings)

target_include_directories(railroad ${WARNING_GUARD} PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
                                                            $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}/include>)

target_compile_features(railroad PUBLIC cxx_std_23)

set_target_properties(
  railroad
  PROPERTIES VERSION ${PROJECT_VERSION}
             CXX_VISIBILITY_PRESET hidden
             VISIBILITY_INLINES_HIDDEN YES)

generate_export_header(railroad EXPORT_FILE_NAME ${PROJECT_BINARY_DIR}/include/railroad/train.hpp)

if(NOT BUILD_SHARED_LIBS)
  target_compile_definitions(railroad PUBLIC SAMPLE_LIBRARY_STATIC_DEFINE)
endif()
