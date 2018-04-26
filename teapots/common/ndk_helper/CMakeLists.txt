
# build native_app_glue as a static lib
include(AndroidNdkModules)
android_ndk_import_module_native_app_glue()

add_library(NdkHelper
  STATIC
    gestureDetector.cpp
    gl3stub.cpp
    GLContext.cpp
    interpolator.cpp
    JNIHelper.cpp
    perfMonitor.cpp
    sensorManager.cpp
    shader.cpp
    tapCamera.cpp
    vecmath.cpp
)

set_target_properties(NdkHelper
  PROPERTIES
    CXX_STANDARD 11
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
)
target_compile_options(NdkHelper
  PUBLIC
    -Wall -Werror -fno-exceptions -fno-rtti
)

target_include_directories(NdkHelper
  PUBLIC
    ${ANDROID_NDK}/sources/android/native_app_glue
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(NdkHelper
  PRIVATE
    native_app_glue
    GLESv2
    EGL
    log
    android
    atomic
)
