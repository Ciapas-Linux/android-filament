
cmake_minimum_required(VERSION 3.10.2)

project("irrlicht")

add_library(app-glue
            STATIC
            ${ANDROID_NDK}/sources/android/native_app_glue/android_native_app_glue.c )

add_library(lirrlicht STATIC IMPORTED)
set_target_properties(lirrlicht PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libIrrlicht.a)

add_library(native-lib SHARED   main.cpp )

include_directories(${CMAKE_CURRENT_SOURCE_DIR}
        ${ANDROID_NDK}/sources/android/native_app_glue/
        ${CMAKE_SOURCE_DIR}/include/ )

message("cmake working directory: " ${CMAKE_SOURCE_DIR})


find_library(log-lib log)

target_link_libraries(native-lib
        app-glue
        android
        EGL
        log
        GLESv1_CM
        GLESv2
        z
        m
        ${log-lib}
        )







