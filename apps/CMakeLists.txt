project(MinervaApps)

include_directories(
  ${MinervaLib_SOURCE_DIR}
)

set(app_list "")

file(GLOB_RECURSE app_file_list "*.cpp")
foreach(app_src ${app_file_list})
  get_filename_component(app_name ${app_src} NAME_WE)
  add_executable(${app_name} ${app_src})
  target_link_libraries(${app_name} minerva)
  if (CUDA_FOUND)
    CUDA_ADD_CUBLAS_TO_TARGET(${app_name})
  endif (CUDA_FOUND)
  list(APPEND app_list ${app_name})
endforeach()

message(STATUS "Apps: ${app_list}")
