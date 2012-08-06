project(fuse-google-drive)

cmake_minimum_required(VERSION 2.8)

find_package(PkgConfig REQUIRED)

pkg_check_modules(FUSE REQUIRED fuse)
pkg_check_modules(CURL REQUIRED libcurl)
pkg_check_modules(JSON REQUIRED json)
pkg_check_modules(XML REQUIRED libxml-2.0)

add_definitions("-D_FILE_OFFSET_BITS=64")

include_directories(${FUSE_INCLUDE_DIRS} ${CURL_INCLUDE_DIRS} ${JSON_INCLUDE_DIRS} ${XML_INCLUDE_DIRS})

add_executable(fuse-google-drive
 gd_fuse_operations.c
 gd_interface.c
 gd_cache.c
 stack.c
 functional_stack.c
 str.c
 curl_interface.c
)

target_link_libraries(fuse-google-drive ${FUSE_LIBRARIES} ${CURL_LIBRARIES} ${JSON_LIBRARIES} ${XML_LIBRARIES})

install(TARGETS fuse-google-drive DESTINATION bin)
