cmake_minimum_required(VERSION 3.9)

add_library(librtlsdr SHARED IMPORTED GLOBAL)

set(LIB_SUBDIR "win_x64")
if(CMAKE_SIZEOF_VOID_P EQUAL 4)
    set(LIB_SUBDIR "win_x86")
endif()

set_target_properties(librtlsdr PROPERTIES INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include)
set_target_properties(librtlsdr PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/dll/${LIB_SUBDIR}/rtlsdr.dll)
set_target_properties(librtlsdr PROPERTIES IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/lib/${LIB_SUBDIR}/rtlsdr.lib)

if(NOT TARGET libusb)
    add_library(libusb SHARED IMPORTED GLOBAL)
    set_target_properties(libusb PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/dll/${LIB_SUBDIR}/libusb-1.0.dll)
endif()

if(NOT TARGET pthreads)
    add_library(pthreads SHARED IMPORTED GLOBAL)
    set_target_properties(pthreads PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/dll/${LIB_SUBDIR}/pthreadVC2.dll)
endif()