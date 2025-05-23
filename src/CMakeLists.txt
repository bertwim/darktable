add_subdirectory(external)

include(CheckCSourceCompiles)
include(CheckCXXSymbolExists)


#
# Add files for libdarktable
#
FILE(GLOB SOURCE_FILES
  "bauhaus/bauhaus.c"
  "common/act_on.c"
  "common/atomic.c"
  "common/bilateral.c"
  "common/bilateralcl.c"
  "common/box_filters.cc"
  "common/cache.c"
  "common/calculator.c"
  "common/collection.c"
  "common/color_harmony.c"
  "common/color_picker.c"
  "common/color_vocabulary.c"
  "common/colorlabels.c"
  "common/colorspaces.c"
  "common/curl_tools.c"
  "common/curve_tools.c"
  "common/custom_primaries.c"
  "common/darktable.c"
  "common/database.c"
  "common/datetime.c"
  "common/dbus.c"
  "common/distance_transform.c"
  "common/dlopencl.c"
  "common/dng_opcode.c"
  "common/dtpthread.c"
  "common/dwt.c"
  "common/dynload.c"
  "common/eaw.c"
  "common/exif.cc"
  "common/file_location.c"
  "common/film.c"
  "common/gaussian.c"
  "common/gimp.c"
  "common/gpx.c"
  "common/grouping.c"
  "common/guided_filter.c"
  "common/heal.c"
  "common/histogram.c"
  "common/history.c"
  "common/history_snapshot.c"
  "common/image.c"
  "common/image_cache.c"
  "common/imagebuf.c"
  "common/import_session.c"
  "common/interpolation.c"
  "common/iop_group.c"
  "common/iop_order.c"
  "common/iop_profile.c"
  "common/l10n.c"
  "common/locallaplacian.c"
  "common/locallaplaciancl.c"
  "common/map_locations.c"
  "common/matrices.c"
  "common/metadata.c"
  "common/metadata_export.c"
  "common/mipmap_cache.c"
  "common/module.c"
  "common/nlmeans_core.c"
  "common/noiseprofiles.c"
  "common/opencl.c"
  "common/overlay.c"
  "common/pdf.c"
  "common/presets.c"
  "common/pwstorage/backend_kwallet.c"
  "common/pwstorage/pwstorage.c"
  "common/ratings.c"
  "common/resource_limits.c"
  "common/selection.c"
  "common/splines.cpp"
  "common/styles.c"
  "common/system_signal_handling.c"
  "common/tags.c"
  "common/undo.c"
  "common/usermanual_url.c"
  "common/utility.c"
  "common/variables.c"
  "common/wb_presets.c"
  "control/conf.c"
  "control/control.c"
  "control/crawler.c"
  "control/jobs.c"
  "control/jobs/control_jobs.c"
  "control/jobs/develop_jobs.c"
  "control/jobs/film_jobs.c"
  "control/jobs/image_jobs.c"
  "control/jobs/sidecar_jobs.c"
  "control/progress.c"
  "control/signal.c"
  "develop/blend.c"
  "develop/blend_gui.c"
  "develop/blends/blendif_lab.c"
  "develop/blends/blendif_raw.c"
  "develop/blends/blendif_rgb_hsl.c"
  "develop/blends/blendif_rgb_jzczhz.c"
  "develop/borders_helper.c"
  "develop/develop.c"
  "develop/format.c"
  "develop/imageop.c"
  "develop/imageop_gui.c"
  "develop/imageop_math.c"
  "develop/lightroom.c"
  "develop/masks/brush.c"
  "develop/masks/circle.c"
  "develop/masks/ellipse.c"
  "develop/masks/gradient.c"
  "develop/masks/group.c"
  "develop/masks/masks.c"
  "develop/masks/path.c"
  "develop/pixelpipe.c"
  "develop/tiling.c"
  "dtgtk/button.c"
  "dtgtk/culling.c"
  "dtgtk/drawingarea.c"
  "dtgtk/expander.c"
  "dtgtk/gradientslider.c"
  "dtgtk/icon.c"
  "dtgtk/paint.c"
  "dtgtk/range.c"
  "dtgtk/resetlabel.c"
  "dtgtk/sidepanel.c"
  "dtgtk/stylemenu.c"
  "dtgtk/thumbnail.c"
  "dtgtk/thumbnail_btn.c"
  "dtgtk/thumbtable.c"
  "dtgtk/togglebutton.c"
  "gui/about.c"
  "gui/accelerators.c"
  "gui/color_picker_proxy.c"
  "gui/gtk.c"
  "gui/gtkentry.c"
  "gui/guides.c"
  "gui/hist_dialog.c"
  "gui/import_metadata.c"
  "gui/metadata_tags.c"
  "gui/preferences.c"
  "gui/presets.c"
  "gui/splash.c"
  "gui/styles_dialog.c"
  "imageio/imageio.c"
  "imageio/imageio_jpeg.c"
  "imageio/imageio_module.c"
  "imageio/imageio_pfm.c"
  "imageio/imageio_png.c"
  "imageio/imageio_pnm.c"
  "imageio/imageio_qoi.c"
  "imageio/imageio_rgbe.c"
  "imageio/imageio_tiff.c"
  "libs/lib.c"
  "views/view.c"
  )

FILE(GLOB HEADER_FILES "*.h" "common/*.h" "external/OpenCL/CL/*.h" "control/*.h" "iop/*.h" "libs/*.h" "views/*.h")

if(APPLE)
  list(APPEND SOURCE_FILES "osx/osx.mm")
  list(APPEND HEADER_FILES "osx/osx.h")
  list(APPEND SOURCE_FILES "common/pwstorage/backend_apple_keychain.c")
  list(APPEND HEADER_FILES "common/pwstorage/backend_apple_keychain.h")
  list(APPEND SOURCE_FILES "main.c")
  include(CheckLanguage)
  check_language(OBJCXX)
  if(CMAKE_OBJCXX_COMPILER)
    enable_language(OBJCXX)
  else()
    set_source_files_properties(osx/osx.mm PROPERTIES LANGUAGE CXX)
  endif()
endif(APPLE)

if(WIN32)
  list(APPEND SOURCE_FILES "win/strptime.c")
  list(APPEND HEADER_FILES "win/strptime.h")
  list(APPEND SOURCE_FILES "win/statvfs.c")
  list(APPEND HEADER_FILES "win/statvfs.h")

  list(APPEND SOURCE_FILES "win/getrusage.c")
  list(APPEND HEADER_FILES "win/getrusage.h")

  list(APPEND SOURCE_FILES "win/rlimit.c")
  list(APPEND HEADER_FILES "win/rlimit.h")

  list(APPEND SOURCE_FILES "win/getdelim.c")
  list(APPEND HEADER_FILES "win/getdelim.h")

  list(APPEND SOURCE_FILES "win/dtwin.c")
  list(APPEND HEADER_FILES "win/dtwin.h")

  list(APPEND SOURCE_FILES "win/filepath.c")
  list(APPEND HEADER_FILES "win/filepath.h")

  list(APPEND SOURCE_FILES "win/scandir.c")
  list(APPEND HEADER_FILES "win/scandir.h")

  list(APPEND SOURCE_FILES "common/pwstorage/backend_windows_credentials.c")
  list(APPEND HEADER_FILES "common/pwstorage/backend_windows_credentials.h")

  # Use mingw's sprintf instead of windows's
  ADD_DEFINITIONS( -D__USE_MINGW_ANSI_STDIO=1 )

  # add it to have proper time.h functions available
  ADD_DEFINITIONS(-D_POSIX_THREAD_SAFE_FUNCTIONS)

  # avoid calling legacy ANSI win api functions
  add_definitions("-DUNICODE -D_UNICODE")

  # add icon, version, ... resources for Windows executable
  configure_file("${CMAKE_SOURCE_DIR}/data/pixmaps/dt_logo_128x128.ico" "${CMAKE_BINARY_DIR}/data/pixmaps/dt_logo_128x128.ico" COPYONLY)
  SET(CMAKE_RC_COMPILE_OBJECT "<CMAKE_RC_COMPILER> -O coff <DEFINES> -i <SOURCE> -o <OBJECT>")
  set(RESOURCE_OBJECT "${CMAKE_CURRENT_BINARY_DIR}/win/darktable.rc")
  configure_file("${CMAKE_CURRENT_SOURCE_DIR}/win/darktable.rc.in" "${CMAKE_CURRENT_BINARY_DIR}/win/darktable.rc")
endif(WIN32)

set(SOURCES ${SOURCE_FILES} ${HEADER_FILES})

if(CMAKE_SYSTEM_PROCESSOR STREQUAL "ppc64le")
  include_directories(${CMAKE_CURRENT_SOURCE_DIR}/ppc64le)
endif()

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/external)
include_directories(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/external/OpenCL)

# initial compiler flags
add_definitions("-DHAVE_CONFIG_H")

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(APPLE AND (CMAKE_CXX_COMPILER_ID STREQUAL "AppleClang" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang"))
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
        list(REMOVE_ITEM CMAKE_CXX_IMPLICIT_LINK_LIBRARIES stdc++)
        list(APPEND CMAKE_CXX_IMPLICIT_LINK_LIBRARIES c++)
        list(REMOVE_DUPLICATES CMAKE_CXX_IMPLICIT_LINK_LIBRARIES)
        # Also remove incorrectly parsed -lto_library flag
        # It wasn't present with Xcode 7.2 and appeared before 8.3 release
        # cmake 3.7.2 doesn't understand this flag and thinks it's a library
        list(REMOVE_ITEM CMAKE_CXX_IMPLICIT_LINK_LIBRARIES to_library)
endif()

# Append thread flags/libraries to LIBS
list(APPEND LIBS "${CMAKE_THREAD_LIBS_INIT}")

# Need to explicitly link against math library.
list(APPEND LIBS "-lm")

if(USE_OPENMP)
  if(OpenMP_C_FLAGS)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
  endif()

  if(OpenMP_CXX_FLAGS)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
  endif()

  if(OpenMP_C_INCLUDE_DIRS)
    include_directories(${OpenMP_C_INCLUDE_DIRS})
  endif()

  if(OpenMP_CXX_INCLUDE_DIRS)
    include_directories(${OpenMP_CXX_INCLUDE_DIRS})
  endif()

  list(APPEND LIBS ${OpenMP_C_LIBRARIES} ${OpenMP_CXX_LIBRARIES})
endif(USE_OPENMP)

if(USE_DARKTABLE_PROFILING)
	add_definitions(-DUSE_DARKTABLE_PROFILING)
	set(SOURCES ${SOURCES} "common/profiling.c")
endif()

#
# Find all other required libraries for building
#
# GTK3 does pull glib, but this allows us to check for the version
find_package(Glib 2.56 REQUIRED)
add_definitions("-DGLIB_VERSION_MIN_REQUIRED=GLIB_VERSION_2_56")
add_definitions("-DGLIB_VERSION_MAX_ALLOWED=GLIB_VERSION_MIN_REQUIRED")
include_directories(SYSTEM ${Glib_INCLUDE_DIRS})
list(APPEND LIBS ${Glib_LIBRARIES})

# GTK3 pulls in ATK, GDK, GDK-PIXBUF, CAIRO, GLIB, PANGO
find_package(GTK3 3.24.15 REQUIRED)
add_definitions("-DGDK_VERSION_MIN_REQUIRED=GDK_VERSION_3_24")
#add_definitions("-DGDK_VERSION_MAX_ALLOWED=GDK_VERSION_MIN_REQUIRED")
include_directories(SYSTEM ${GTK3_INCLUDE_DIRS})
list(APPEND LIBS ${GTK3_LIBRARIES})

# Check for libxml2 / broken cmake module can't be included in the foreach() below
find_package(LibXml2 2.6 REQUIRED)
include_directories(SYSTEM ${LIBXML2_INCLUDE_DIR})
list(APPEND LIBS ${LIBXML2_LIBRARIES})
add_definitions(${LIBXML2_DEFINITIONS})

if(USE_CAMERA_SUPPORT)
  find_package(Gphoto2 2.5)
  if(Gphoto2_FOUND)
    include_directories(SYSTEM ${Gphoto2_INCLUDE_DIRS})
    list(APPEND LIBS ${Gphoto2_LIBRARIES})
    set(SOURCES ${SOURCES} "common/camera_control.c" "control/jobs/camera_jobs.c" )
    add_definitions("-DHAVE_GPHOTO2")
    # CPack ignores variables you define in your CMakeLists.txt file,
    # and only variables ${CPACK_*} are correctly used.
    # so this needs to be saved by adding another variable with a name beginning with CPACK
    set(CPACK_NSIS_GPHOTO2_VERSION ${Gphoto2_VERSION_STRING} CACHE STRING "Gphoto2 version string")
    set(CPACK_NSIS_GPHOTO2_PORT_VERSION ${Gphoto2_PORT_VERSION_STRING} CACHE STRING "Gphoto2 port version string")
  endif()
endif(USE_CAMERA_SUPPORT)

# Used for 16-bit (half) float TIFF export (and faster import)
# (IlmBase Half library in 2.5 and earlier and Imath 3.0 did not have C API)
find_package(Imath 3.1 CONFIG)
if(TARGET Imath::Imath)
  list(APPEND LIBS Imath::Imath)
  add_compile_definitions(HAVE_IMATH)
endif()

if(USE_OPENEXR)
  find_package(OpenEXR 3.0 CONFIG)
  if(TARGET OpenEXR::OpenEXR)
    set(OpenEXR_LIBRARIES OpenEXR::OpenEXR)
  else()
    find_package(OpenEXR)
  endif()
  if(OpenEXR_FOUND)
    include_directories(SYSTEM ${OpenEXR_INCLUDE_DIRS})
    list(APPEND LIBS ${OpenEXR_LIBRARIES})
    add_definitions("-DHAVE_OPENEXR")
    list(APPEND SOURCES "imageio/imageio_exr.cc")
    set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} exr CACHE INTERNAL "")
  endif(OpenEXR_FOUND)
endif(USE_OPENEXR)

if(USE_JXL)
  find_package(JXL 0.7.0)
  if(JXL_FOUND)
    include_directories(SYSTEM ${JXL_INCLUDE_DIRS})
    list(APPEND LIBS ${JXL_LIBRARIES})
    add_definitions("-DHAVE_LIBJXL")
    list(APPEND SOURCES "imageio/imageio_jpegxl.c")
    set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} jxl CACHE INTERNAL "")
  endif(JXL_FOUND)
endif(USE_JXL)

if(USE_WEBP)
  find_package(WebP 0.3.0)
  if(WebP_FOUND)
    include_directories(SYSTEM ${WebP_INCLUDE_DIRS})
    list(APPEND LIBS ${WebP_LIBRARIES})
    add_definitions("-DHAVE_WEBP")
    list(APPEND SOURCES "imageio/imageio_webp.c")
    set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} webp CACHE INTERNAL "")
  endif(WebP_FOUND)
endif(USE_WEBP)

if(USE_AVIF)
  # no version check in config mode because of major only match policy
  find_package(libavif CONFIG)
  if(TARGET avif)
    if(libavif_VERSION VERSION_GREATER_EQUAL 0.9.3)
      list(APPEND LIBS avif)
      add_definitions(-DHAVE_LIBAVIF=1)
      list(APPEND SOURCES "imageio/imageio_avif.c")
      set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} avif CACHE INTERNAL "")
    else()
      set(libavif_FOUND NOTFOUND PARENT_SCOPE)
    endif()
  endif()
endif()

if(USE_HEIF)
  # no version check in config mode because of exact match policy
  find_package(libheif CONFIG)
  if(NOT TARGET heif)
    find_package(libheif 1.13.0 MODULE)
  endif()
  if(TARGET heif)
    if(libheif_VERSION VERSION_GREATER_EQUAL 1.13)
      list(APPEND LIBS heif)
      add_definitions(-DHAVE_LIBHEIF=1)
      list(APPEND SOURCES "imageio/imageio_heif.c")
      set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} heif heic hif hej2 avci CACHE INTERNAL "")
      if(NOT libavif_FOUND)
        # libheif can handle avif, too
        set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} avif CACHE INTERNAL "")
      endif()
    else()
      set(libheif_FOUND NOTFOUND)
    endif()
  endif()
endif()

# For now we use the LibRaw submodule
if(USE_LIBRAW)
  if(DONT_USE_INTERNAL_LIBRAW)
    find_package(libraw 0.21.0)
    if(libraw_FOUND)
      message(STATUS "Using system LibRaw")
      list(APPEND LIBS ${libraw_LIBRARY})
      add_definitions(-DHAVE_LIBRAW=1)
      list(APPEND SOURCES "imageio/imageio_libraw.c")
    else()
      message(STATUS "System LibRaw not found or not suitable, building from intree copy")
    endif()
  else()
    message(STATUS "Building LibRaw from intree copy")
    add_definitions(-DHAVE_LIBRAW=1)
    list(APPEND SOURCES "imageio/imageio_libraw.c")
  endif()
endif()

find_package(LensFun REQUIRED)
include_directories(SYSTEM ${LensFun_INCLUDE_DIRS})
list(APPEND LIBS ${LensFun_LIBRARIES})

find_package(SQLite3 3.26 REQUIRED)
list(APPEND LIBS SQLite::SQLite3)

foreach(lib ${OUR_LIBS} GIO GThread GModule PangoCairo Rsvg2 PNG JPEG TIFF LCMS2 JsonGlib)
  find_package(${lib} REQUIRED)
  include_directories(SYSTEM ${${lib}_INCLUDE_DIRS})
  list(APPEND LIBS ${${lib}_LIBRARIES})
  add_definitions(${${lib}_DEFINITIONS})
endforeach(lib)

if(PNG_VERSION_STRING VERSION_LESS 1.5)
  message(FATAL_ERROR "libpng version 1.5 or newer is required")
endif()

# Use imported target for curl
find_package(CURL 7.56 REQUIRED)
list(APPEND LIBS CURL::libcurl)

# Require exiv2 >= 0.27.2 to make sure everything we need is available
find_package(Exiv2 0.27.2 REQUIRED)
include_directories(SYSTEM ${Exiv2_INCLUDE_DIRS})
list(APPEND LIBS ${Exiv2_LIBRARIES})
add_definitions(${Exiv2_DEFINITIONS})
if(CMAKE_CXX_COMPILER_ID MATCHES "Clang" AND Exiv2_VERSION VERSION_LESS "0.28.0")
  add_compile_definitions(_LIBCPP_ENABLE_CXX17_REMOVED_AUTO_PTR)
endif()

# Optionally enable ISOBMFF support in Exiv2
if (USE_ISOBMFF)
  if(Exiv2_VERSION VERSION_GREATER_EQUAL "0.27.4")
    # exiv2 >= 0.27.4 provides optional support for ISOBMFF files.
    # This must be manually enabled during exiv2 build and can be checked with
    # the EXV_ENABLE_BMFF symbol.
    check_symbol_exists(EXV_ENABLE_BMFF
      "${Exiv2_INCLUDE_DIRS}/exiv2/exv_conf.h"
      HAVE_EXV_ENABLE_BMFF)
    if(HAVE_EXV_ENABLE_BMFF)
      set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} cr3 CACHE INTERNAL "")
      message(STATUS "Exiv2 >= 0.27.4 found with ISOBMFF support (CR3, AVIF, HEIF)")
    else()
      message(STATUS "Exiv2 >= 0.27.4 found, but was not compiled with ISOBMFF support (CR3, AVIF, HEIF)")
    endif()
  else()
    message(STATUS "Exiv2 < 0.27.4 found, no support for ISOBMFF files (CR3, AVIF, HEIF)")
  endif()
endif()

# Optionally enable MIDI support
if(USE_PORTMIDI)
  find_package(PortMidi)
endif(USE_PORTMIDI)

if(USE_OPENJPEG)
  find_package(OpenJPEG CONFIG)
  if(OpenJPEG_FOUND)
    add_definitions("-DHAVE_OPENJPEG")
    list(APPEND SOURCES "imageio/imageio_j2k.c")
    include_directories(SYSTEM ${OPENJPEG_INCLUDE_DIRS})
    list(APPEND LIBS ${OPENJPEG_LIBRARIES})
    set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} j2c j2k jp2 jpc jpf jpx CACHE INTERNAL "")
  endif(OpenJPEG_FOUND)
endif(USE_OPENJPEG)

find_package(IsoCodes 3.66)
if(IsoCodes_FOUND)
  add_definitions("-DHAVE_ISO_CODES")
else(IsoCodes_FOUND)
  message(STATUS "no suitable iso-codes, there will be no language names in the preferences")
endif(IsoCodes_FOUND)

#
# Detect compile of optional pwstorage backends
#
if(USE_LIBSECRET AND JsonGlib_FOUND)
  find_package(Libsecret)
  if(Libsecret_FOUND)
    if(Libsecret_VERSION VERSION_LESS "0.16")
      message(STATUS "Found libsecret version ${Libsecret_VERSION}. You need at least libsecret 0.16 or newer.")
      set(Libsecret_FOUND FALSE)
    else()
      if(Libsecret_VERSION VERSION_LESS "0.18")
        message(STATUS "Found libsecret version ${Libsecret_VERSION}. Enable unstable API. Please upgrade to version 0.18 or newer.")
        add_definitions("-DSECRET_API_SUBJECT_TO_CHANGE")
      endif()
      set(SOURCES ${SOURCES} "common/pwstorage/backend_libsecret.c")
      include_directories(SYSTEM ${Libsecret_INCLUDE_DIRS})
      list(APPEND LIBS ${Libsecret_LIBRARIES})
      add_definitions("-DHAVE_LIBSECRET")
    endif()
  endif(Libsecret_FOUND)
endif(USE_LIBSECRET AND JsonGlib_FOUND)

if(USE_KWALLET)
  add_definitions("-DHAVE_KWALLET")
endif(USE_KWALLET)

if(APPLE)
  add_definitions("-DHAVE_APPLE_KEYCHAIN")
endif(APPLE)

if(WIN32)
  add_definitions("-DHAVE_WINDOWS_CREDENTIALS")
endif(WIN32)

if(USE_MAC_INTEGRATION)
  find_package(MacIntegration)
  if(MacIntegration_FOUND)
    include_directories(SYSTEM ${MacIntegration_INCLUDE_DIRS})
    list(APPEND LIBS ${MacIntegration_LIBRARIES})
    add_definitions("-DMAC_INTEGRATION")
    find_package(P11Kit)
    if(P11Kit_FOUND)
      include_directories(SYSTEM ${P11Kit_INCLUDE_DIRS})
      list(APPEND LIBS ${P11Kit_LINK_LIBRARIES})
      add_definitions("-DHAVE_P11KIT")
    endif()
  endif(MacIntegration_FOUND)
endif(USE_MAC_INTEGRATION)

if(USE_UNITY)
  find_package(Unity)
  if(Unity_FOUND)
    add_definitions(-DHAVE_UNITY)
    include_directories(SYSTEM ${Unity_INCLUDE_DIRS})
    list(APPEND LIBS ${Unity_LIBRARIES})
  endif(Unity_FOUND)
endif(USE_UNITY)

if(USE_GRAPHICSMAGICK)
  find_package(GraphicsMagick)
  if(GraphicsMagick_FOUND)
    add_definitions(-DHAVE_GRAPHICSMAGICK)
    set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} bmp cin dcm dpx fit fits fts gif jng jp2 jpc jpf jpx miff mng pam webp jxl CACHE INTERNAL "")
    include_directories(SYSTEM ${GraphicsMagick_INCLUDE_DIRS})
    list(APPEND LIBS ${GraphicsMagick_LIBRARIES})
    list(APPEND SOURCES "imageio/imageio_gm.c")
  endif(GraphicsMagick_FOUND)
endif(USE_GRAPHICSMAGICK)

if(USE_IMAGEMAGICK AND NOT GraphicsMagick_FOUND)
  # Do not use find_package(): module is not providing needed CFLAGS
  find_package(PkgConfig)
  pkg_check_modules(ImageMagick MagickWand)
  if(ImageMagick_FOUND)
    list(APPEND SOURCES "imageio/imageio_im.c")
    if(ImageMagick_VERSION VERSION_GREATER 7)
      add_definitions(-DHAVE_IMAGEMAGICK7)
      set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} qoi CACHE INTERNAL "")
    endif(ImageMagick_VERSION VERSION_GREATER 7)
    add_definitions(-DHAVE_IMAGEMAGICK ${ImageMagick_CFLAGS_OTHER})
    include_directories(SYSTEM ${ImageMagick_INCLUDE_DIRS})
    foreach(lib ${ImageMagick_LIBRARIES})
      find_library(ImageMagick_LIBRARY NAMES ${lib} HINTS ${ImageMagick_LIBRARY_DIRS})
      list(APPEND LIBS ${ImageMagick_LIBRARY})
      unset(ImageMagick_LIBRARY CACHE)
    endforeach(lib)
    set(DT_SUPPORTED_EXTENSIONS ${DT_SUPPORTED_EXTENSIONS} bmp cin dcm dpx fit fits fts gif jng jp2 jpc jpf jpx miff mng pam webp jxl CACHE INTERNAL "")
  endif(ImageMagick_FOUND)
endif(USE_IMAGEMAGICK AND NOT GraphicsMagick_FOUND)

if(USE_GMIC)
  find_package(GMIC)
  if(GMIC_FOUND)
    add_definitions(-DHAVE_GMIC)
    include_directories(SYSTEM ${GMIC_INCLUDE_DIRS})
    list(APPEND LIBS ${GMIC_LIBRARIES})
  endif(GMIC_FOUND)
endif(USE_GMIC)

if(USE_ICU)
  find_package(ICU COMPONENTS i18n data uc)
  if(ICU_FOUND)
    add_definitions(-DHAVE_ICU -DSQLITE_CORE -DSQLITE_ENABLE_ICU)
    list(APPEND LIBS ICU::i18n ICU::data ICU::uc)
    set(SOURCES ${SOURCES} "common/sqliteicu.c")
  endif(ICU_FOUND)
endif(USE_ICU)

if(USE_OPENCL)
  add_definitions("-DHAVE_OPENCL")
endif(USE_OPENCL)


# Check for __builtin_cpu_supports here due to a bug in clang/llvm. LLVM uses
# libgcc to provide the symbols, so if clang wasn't compiled with libgcc, the
# compiler will say it's available; however the linker cannot find the symbols.
# So do a quick test compile to see if it's actually available.
# See https://llvm.org/bugs/show_bug.cgi?id=25510
check_c_source_compiles("#include <stdio.h>
int main() {
  __builtin_cpu_init();
  printf(\"%d\", __builtin_cpu_supports(\"sse3\"));
}" HAVE_BUILTIN_CPU_SUPPORTS)
if(HAVE_BUILTIN_CPU_SUPPORTS)
  add_definitions("-DHAVE_BUILTIN_CPU_SUPPORTS")
endif(HAVE_BUILTIN_CPU_SUPPORTS)
MESSAGE(STATUS "Does the compiler support __builtin_cpu_supports(): ${HAVE_BUILTIN_CPU_SUPPORTS}")

check_c_source_compiles("
static __thread int tls;
int main(void)
{
  return 0;
}" HAVE_TLS)
if(NOT HAVE_TLS)
  MESSAGE(FATAL_ERROR "The compiler does not support Thread-local storage.")
endif()


if(NOT CUSTOM_CFLAGS)
  if(BUILD_SSE2_CODEPATHS)
    #we MUST always specify our required instruction set, native might not detect it
    set(DT_REQ_INSTRUCTIONS "-msse2")
  endif()

  include(march-mtune)

  #if(NOT BUILD_SSE2_CODEPATHS)
  #  set(MARCH "${MARCH} -mno-sse2 -D__DISABLE_SSE2__ -U__SSE2__ -D__DISABLE_SSE__ -U__SSE__")
  #endif()

  #-g MUST be set for ALL builds, or there will be no support for them when bugs happen
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${MARCH} ${DT_REQ_INSTRUCTIONS} -g")
  set(CMAKE_C_FLAGS_RELWITHDEBINFO "${CMAKE_C_FLAGS_RELWITHDEBINFO} -O2 -ftree-vectorize")
  set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O3 -ffast-math -fno-finite-math-only")
  if(CMAKE_COMPILER_IS_GNUCC)
    if(BUILD_SSE2_CODEPATHS)
      set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -mfpmath=sse")
    endif()

    set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O0 -g3 -ggdb3")
    set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -fexpensive-optimizations")
  else()
    set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O0")
  endif()

  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${MARCH} ${DT_REQ_INSTRUCTIONS} -g")
  set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "${CMAKE_CXX_FLAGS_RELWITHDEBINFO} -O2 -ftree-vectorize")
  set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3 -ffast-math -fno-finite-math-only")
  if(CMAKE_COMPILER_IS_GNUCXX)
    if(BUILD_SSE2_CODEPATHS)
      set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -mfpmath=sse")
    endif()

    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0 -g3 -ggdb3")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -fexpensive-optimizations")
  else()
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0")
  endif()
endif(NOT CUSTOM_CFLAGS)

if(WIN32)
  set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,--enable-runtime-pseudo-reloc -municode")
  set(CMAKE_MODULE_LINKER_FLAGS "${CMAKE_MODULE_LINKER_FLAGS} -Wl,--enable-runtime-pseudo-reloc")
  set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -Wl,--enable-runtime-pseudo-reloc")

  SET(CMAKE_SHARED_LIBRARY_LINK_C_FLAGS "-Wl,--no-undefined -static-libgcc -Wl,-O1 -Wl,--as-needed -Wl,--sort-common")
  SET(CMAKE_SHARED_LIBRARY_LINK_CXX_FLAGS "-Wl,--no-undefined -static-libgcc -Wl,-O1 -Wl,--as-needed -Wl,--sort-common")

  list(APPEND LIBS psapi) # Needed for GetProcessMemoryInfo()
  list(APPEND LIBS exchndl) # Needed for exception handling and backtrace()
endif(WIN32)

set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -D_DEBUG")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -D_DEBUG")

#
# Generate config.h
#
list(REMOVE_DUPLICATES DT_SUPPORTED_EXTENSIONS)
string(REPLACE ";" "\", \"" DT_SUPPORTED_EXTENSIONS_STRING "${DT_SUPPORTED_EXTENSIONS}")
configure_file("${CMAKE_CURRENT_SOURCE_DIR}/config.cmake.h" "${DARKTABLE_BINDIR}/config.h" @ONLY)


#
# Build external deps
#
if(USE_LUA)
  find_package(Lua54 5.4)
  if(Lua54_FOUND)
    message(STATUS "Lua support: Enabled")
    include_directories(SYSTEM ${Lua54_INCLUDE_DIRS})
    list(APPEND LIBS ${Lua54_LDFLAGS})
  else()
    if(DONT_USE_INTERNAL_LUA)
      message(STATUS "Lua support: System library for lua 5.4 not found (to use darktable's version use -DDONT_USE_INTERNAL_LUA=Off)")
      set(USE_LUA OFF)
    else(DONT_USE_INTERNAL_LUA)
      message(STATUS "Lua support: System library not found (using darktable's version)")
      include_directories(${CMAKE_CURRENT_SOURCE_DIR}/external/lua/src)
      add_subdirectory(external/lua)
      list(APPEND LIBS lua)
    endif(DONT_USE_INTERNAL_LUA)
  endif(Lua54_FOUND)

  if(USE_LUA)
    add_definitions("-DUSE_LUA")
    FILE(GLOB SOURCE_FILES_LUA
      "lua/cairo.c"
      "lua/call.c"
      "lua/configuration.c"
      "lua/database.c"
      "lua/events.c"
      "lua/film.c"
      "lua/format.c"
      "lua/gettext.c"
      "lua/glist.c"
      "lua/gui.c"
      "lua/guides.c"
      "lua/image.c"
      "lua/init.c"
      "lua/lib.c"
      "lua/lua.c"
      "lua/lualib.c"
      "lua/luastorage.c"
      "lua/modules.c"
      "lua/password.c"
      "lua/preferences.c"
      "lua/print.c"
      "lua/storage.c"
      "lua/styles.c"
      "lua/tags.c"
      "lua/types.c"
      "lua/util.c"
      "lua/view.c"
      "lua/widget/box.c"
      "lua/widget/button.c"
      "lua/widget/check_button.c"
      "lua/widget/combobox.c"
      "lua/widget/container.c"
      "lua/widget/entry.c"
      "lua/widget/file_chooser.c"
      "lua/widget/label.c"
      "lua/widget/section_label.c"
      "lua/widget/separator.c"
      "lua/widget/slider.c"
      "lua/widget/stack.c"
      "lua/widget/text_view.c"
      "lua/widget/widget.c"
      )
    set(SOURCES ${SOURCES} ${SOURCE_FILES_LUA})
  endif(USE_LUA)
else(USE_LUA)
  message(STATUS "Lua support: Disabled")
endif(USE_LUA)

if(USE_LUA)
  if(NOT Lua54_FOUND)
    list(APPEND LIB_DEPS lua) # 2nd half of the ugliness :/
  endif(NOT Lua54_FOUND)
  # liblautoc for lua automated interface generation
  add_library(lautoc_static STATIC IMPORTED)
  set_target_properties(lautoc_static PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_BINARY_DIR}/external/LuaAutoC/liblautoc.a POSITION_INDEPENDENT_CODE True)
  include_directories(${CMAKE_CURRENT_SOURCE_DIR}/external/LuaAutoC/)
  add_subdirectory(external/LuaAutoC)
  list(APPEND LIB_DEPS lautoc)
  list(APPEND STATIC_LIBS lautoc_static)
endif(USE_LUA)

find_package(Pugixml 1.5 REQUIRED)
include_directories(SYSTEM ${Pugixml_INCLUDE_DIRS})
list(APPEND LIBS ${Pugixml_LIBRARIES})

if(NOT SOURCE_PACKAGE)
  add_definitions(-Werror -Wfatal-errors )
endif()

if(CMAKE_CXX_COMPILER_ID STREQUAL "AppleClang" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
  # do not error out on "loop not vectorized" clang OpenMP warnings
  add_definitions("-Wno-error=pass-failed")
endif()

# osm gps map library
if(USE_MAP)
  find_package(OSMGpsMap)
  if(OSMGpsMap_FOUND)
    message(STATUS "Map mode: enabled")
    add_definitions("-DHAVE_MAP")
    if(NOT OSMGpsMap_VERSION VERSION_LESS 1.1.0)
      add_definitions("-DHAVE_OSMGPSMAP_110_OR_NEWER")
    endif()
    if(OSMGpsMap_VERSION VERSION_GREATER 1.1.0)
      add_definitions("-DHAVE_OSMGPSMAP_NEWER_THAN_110")
    endif()
    include_directories(SYSTEM ${OSMGpsMap_INCLUDE_DIRS})
    list(APPEND LIBS ${OSMGpsMap_LIBRARIES})
    add_definitions(${OSMGpsMap_DEFINITIONS})
  else(OSMGpsMap_FOUND)
    set(USE_MAP OFF)
    message(STATUS "Map mode: disabled, please install libosmgpsmap")
  endif(OSMGpsMap_FOUND)

else(USE_MAP)
  message(STATUS "Map mode: disabled")
endif(USE_MAP)

# libcolord-gtk:
if(USE_COLORD)
  find_package(Colord)
  if(Colord_FOUND)
    find_package(ColordGTK)
    if(ColordGTK_FOUND)
      # We might make use of colord directly so link against it explicitly. just in case. move up if it is used without colord-gtk, too.
      include_directories(SYSTEM ${Colord_INCLUDE_DIRS})
      list(APPEND LIBS ${Colord_LIBRARIES})
      add_definitions(${Colord_DEFINITIONS})

      # ... and also against libcolord-gtk to get the display profile
      include_directories(SYSTEM ${ColordGTK_INCLUDE_DIRS})
      list(APPEND LIBS ${ColordGTK_LIBRARIES})
      add_definitions(${ColordGTK_DEFINITIONS})
      add_definitions("-DUSE_COLORDGTK")
    else(ColordGTK_FOUND)
      message(STATUS "No libcolord-gtk found, this build will lack the ability to get the screen profile from colord")
      set(USE_COLORD OFF)
    endif(ColordGTK_FOUND)
  else(Colord_FOUND)
    message(STATUS "No libcolord found, this build will lack the ability to get the screen profile from colord")
    set(USE_COLORD OFF)
  endif(Colord_FOUND)
endif(USE_COLORD)

if(BUILD_PRINT)
  find_package(Cups)
  if(CUPS_FOUND)
    include_directories(SYSTEM ${CUPS_INCLUDE_DIR})
    FILE(GLOB SOURCE_FILES_PRINT
      "common/cups_print.h"
      "common/cups_print.c"
      "common/printprof.c"
      "common/printing.h"
      "common/printing.c"
      )
    set(SOURCES ${SOURCES} ${SOURCE_FILES_PRINT})
    list(APPEND LIBS ${CUPS_LIBRARIES})
    add_definitions("-DHAVE_PRINT")
    message(STATUS "Print mode: enabled")
  else(CUPS_FOUND)
    set(BUILD_PRINT OFF)
    message(STATUS "Print mode: disabled, please install CUPS dev package")
  endif(CUPS_FOUND)
else(BUILD_PRINT)
  message(STATUS "Print mode: disabled")
endif(BUILD_PRINT)

if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
  if(HAVE_EXECINFO_H)
    add_definitions("-DDT_HAVE_SIGNAL_TRACE")
    message(STATUS "Signal debug: print-trace possible")
  endif(HAVE_EXECINFO_H)
endif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")

#
# set development flags for our code
#
if(DT_CMAKE_INCLUDE_WHAT_YOU_USE)
  set(CMAKE_C_INCLUDE_WHAT_YOU_USE ${DT_CMAKE_INCLUDE_WHAT_YOU_USE})
  set(CMAKE_CXX_INCLUDE_WHAT_YOU_USE ${DT_CMAKE_INCLUDE_WHAT_YOU_USE})
endif()

#
# Setup generation of preference dialog files..
#
if(NOT ${Xsltproc_BIN} STREQUAL "Xsltproc_BIN-NOTFOUND")
  add_custom_command(
    DEPENDS ${CMAKE_SOURCE_DIR}/tools/generate_prefs.xsl ${CMAKE_SOURCE_DIR}/data/darktableconfig.dtd ${DARKTABLE_DATADIR}/darktableconfig.xml
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/preferences_gen.h
    COMMAND ${Xsltproc_BIN} --nonet --stringparam HAVE_OPENCL ${HAVE_OPENCL} ${CMAKE_SOURCE_DIR}/tools/generate_prefs.xsl ${DARKTABLE_DATADIR}/darktableconfig.xml > ${CMAKE_CURRENT_BINARY_DIR}/preferences_gen.h
    COMMENT "Generating preferences"
  )
  add_custom_command(
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/../tools/generate_darktablerc_conf.xsl ${DARKTABLE_DATADIR}/darktableconfig.dtd ${DARKTABLE_DATADIR}/darktableconfig.xml
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/conf_gen.h
    COMMAND ${Xsltproc_BIN} --nonet --stringparam HAVE_OPENCL ${HAVE_OPENCL} ${CMAKE_CURRENT_SOURCE_DIR}/../tools/generate_darktablerc_conf.xsl ${DARKTABLE_DATADIR}/darktableconfig.xml > ${CMAKE_CURRENT_BINARY_DIR}/conf_gen.h
    COMMENT "Generating configuration min/max/default/type"
  )
else(NOT ${Xsltproc_BIN} STREQUAL "Xsltproc_BIN-NOTFOUND")
  if(NOT ${Saxon_BIN} STREQUAL "Saxon_BIN-NOTFOUND")
    add_custom_command(
      DEPENDS ${CMAKE_SOURCE_DIR}/tools/generate_prefs.xsl ${CMAKE_SOURCE_DIR}/data/darktableconfig.dtd ${DARKTABLE_DATADIR}/darktableconfig.xml
      OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/preferences_gen.h
      COMMAND ${Saxon_BIN} ${DARKTABLE_DATADIR}/darktableconfig.xml ${CMAKE_SOURCE_DIR}/tools/generate_prefs.xsl HAVE_OPENCL=${HAVE_OPENCL} > ${CMAKE_CURRENT_BINARY_DIR}/preferences_gen.h
      COMMENT "Generating preferences"
    )
    add_custom_command(
      DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/../tools/generate_darktablerc_conf.xsl ${DARKTABLE_DATADIR}/darktableconfig.dtd ${DARKTABLE_DATADIR}/darktableconfig.xml
      OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/conf_gen.h
      COMMAND ${Saxon_BIN} ${DARKTABLE_DATADIR}/darktableconfig.xml ${CMAKE_CURRENT_SOURCE_DIR}/../tools/generate_darktablerc_conf.xsl HAVE_OPENCL=${HAVE_OPENCL} > ${CMAKE_CURRENT_BINARY_DIR}/conf_gen.h
      COMMENT "Generating configuration min/max/default/type"
    )
  else(NOT ${Saxon_BIN} STREQUAL "Saxon_BIN-NOTFOUND")
    message(FATAL_ERROR "Don't know how to generate preferences")
  endif(NOT ${Saxon_BIN} STREQUAL "Saxon_BIN-NOTFOUND")
endif(NOT ${Xsltproc_BIN} STREQUAL "Xsltproc_BIN-NOTFOUND")

file(GLOB darktable_STYLES
     "${DARKTABLE_DATADIR}/styles/*.dtstyle"
)

add_custom_command(
  DEPENDS ${darktable_STYLES} ${CMAKE_SOURCE_DIR}/tools/generate_styles_string.sh
  OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/styles_string.h
  COMMAND ${CMAKE_SOURCE_DIR}/tools/generate_styles_string.sh ${DARKTABLE_DATADIR}/styles ${CMAKE_CURRENT_BINARY_DIR}/styles_string.h
  COMMENT "Generating styles strings for translation"
)

add_custom_target(
  generate_styles_string ALL
  DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/styles_string.h
  WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)

add_custom_target(
  generate_preferences ALL
  DEPENDS ${CMAKE_SOURCE_DIR}/tools/generate_prefs.xsl ${CMAKE_SOURCE_DIR}/data/darktableconfig.dtd ${DARKTABLE_DATADIR}/darktableconfig.xml ${CMAKE_CURRENT_BINARY_DIR}/preferences_gen.h
  WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)
add_custom_target(
  generate_conf ALL
  DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/../tools/generate_darktablerc_conf.xsl ${DARKTABLE_DATADIR}/darktableconfig.dtd ${DARKTABLE_DATADIR}/darktableconfig.xml ${CMAKE_CURRENT_BINARY_DIR}/conf_gen.h
  WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)
if(USE_XMLLINT)
  add_dependencies(generate_preferences validate_darktableconfig_xml generate_conf)
endif(USE_XMLLINT)

#
# build libdarktable
#
add_library(lib_darktable SHARED ${DARKTABLE_BINDIR}/preferences_gen.h ${DARKTABLE_BINDIR}/version_gen.c ${SOURCES})

# cmake implicitly sets GENERATED on the source file in the directory of the custom command
# since this isn't the same directory we do have to manually set it
set_source_files_properties(${DARKTABLE_BINDIR}/version_gen.c PROPERTIES GENERATED TRUE)

add_dependencies(lib_darktable generate_styles_string)
add_dependencies(lib_darktable generate_conf)
add_dependencies(lib_darktable generate_version)
add_dependencies(lib_darktable generate_preferences)
add_dependencies(lib_darktable generate_authors_h)

if(APPLE)
  set_target_properties(lib_darktable PROPERTIES MACOSX_RPATH TRUE)
endif(APPLE)
set_target_properties(lib_darktable PROPERTIES OUTPUT_NAME darktable)
set_target_properties(lib_darktable PROPERTIES LINKER_LANGUAGE C)

#
# Link external libs
#

if(LIB_DEPS)
  add_dependencies(lib_darktable ${LIB_DEPS})
endif()

target_link_libraries(lib_darktable PUBLIC ${STATIC_LIBS})
target_link_libraries(lib_darktable PRIVATE whereami)
target_link_libraries(lib_darktable PUBLIC ${LIBS})

unset(LIBS)
unset(STATIC_LIBS)
unset(LIB_DEPS)

add_library(lib_darktable_imageio_rawspeed STATIC imageio/imageio_rawspeed.cc)
target_link_libraries(lib_darktable_imageio_rawspeed PRIVATE rawspeed)
target_link_libraries(lib_darktable PRIVATE lib_darktable_imageio_rawspeed)

#
# Install lib_darktable
#
if(WIN32)
  # Windows needs its DLLs in the same directory as the executable to find them.
  install(TARGETS lib_darktable RUNTIME DESTINATION bin COMPONENT DTApplication)
else(WIN32)
  install(TARGETS lib_darktable DESTINATION ${CMAKE_INSTALL_LIBDIR}/darktable)
endif(WIN32)

# Compile views modules
add_subdirectory(views ${DARKTABLE_LIBDIR}/views)

# Compile lighttable modules
add_subdirectory(libs ${DARKTABLE_LIBDIR}/plugins/lighttable)

# Compile darkroom modules
add_subdirectory(iop ${DARKTABLE_LIBDIR}/plugins)

# Compile export modules
add_subdirectory(imageio ${DARKTABLE_LIBDIR}/plugins/imageio)

if(HAVE_OPENCL)
  # have a small test program, to be run as root on some systems to enable the driver to run cl stuff
  add_subdirectory(cltest)
endif(HAVE_OPENCL)

# have a command line interface
add_subdirectory(cli)

# have a command line utility to generate all the thumbnails
add_subdirectory(generate-cache)

# have a small test program that verifies your color management setup
if(BUILD_CMSTEST)
  add_subdirectory(cmstest)
endif(BUILD_CMSTEST)

# have a gui tool to create CLUTs from colour chart targets
add_subdirectory(chart)

# have some test programs for unit testing, ...
if(BUILD_TESTING)
  add_subdirectory(tests)
endif(BUILD_TESTING)

#
# build darktable executable
#
add_executable(darktable ${SUBSYSTEM_MACOSX} ${SUBSYSTEM_WIN32} main.c ${RESOURCE_OBJECT})
set_target_properties(darktable PROPERTIES LINKER_LANGUAGE C)
if(APPLE)
  set_target_properties(lib_darktable PROPERTIES LINK_FLAGS "-framework Carbon -framework AppKit -framework Security")
endif(APPLE)
target_link_libraries(darktable lib_darktable)

if (WIN32)
  set_target_properties(darktable PROPERTIES LINK_FLAGS "-mconsole -mwindows -Wl,-subsystem,console")
  _detach_debuginfo (darktable bin)
  _detach_debuginfo (lib_darktable bin)
else()
    set_target_properties(darktable
                          PROPERTIES
                          INSTALL_RPATH ${RPATH_ORIGIN}/${REL_BIN_TO_LIBDIR})
endif(WIN32)

install(TARGETS darktable DESTINATION ${CMAKE_INSTALL_BINDIR} COMPONENT DTApplication)

InstallDependencyFiles()

# Tell CPack about the components and group the data components together (CPACK_COMPONENT_${COMPONENT_NAME_ALL_CAPS}_GROUP).
set(CPACK_COMPONENTS_ALL DTApplication DTDebugSymbols DTDocuments)

if(USE_LIBRAW AND NOT (DONT_USE_INTERNAL_LIBRAW AND libraw_FOUND))
  set(LIBRAW_PATH "${CMAKE_CURRENT_SOURCE_DIR}/external/LibRaw" CACHE STRING "Relative path to libraw directory (default=CMAKE_CURRENT_SOURCE_DIR)")
  if(NOT USE_OPENMP)
    set(ENABLE_OPENMP OFF CACHE BOOL "")
  endif()
  set(ENABLE_LCMS OFF CACHE BOOL "")
  set(ENABLE_JASPER OFF CACHE BOOL "")

  # LibRaw sub-module
  add_subdirectory(external/LibRaw-cmake)
  target_link_libraries(lib_darktable PRIVATE libraw::libraw)
endif()

#
# generate the authors file
#
add_custom_command(
  DEPENDS ${CMAKE_SOURCE_DIR}/tools/authors_h.sh ${CMAKE_SOURCE_DIR}/AUTHORS
  OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/tools/darktable_authors.h
  COMMAND ${CMAKE_COMMAND} -E make_directory ${CMAKE_CURRENT_BINARY_DIR}/tools/
  COMMAND bash ${CMAKE_SOURCE_DIR}/tools/authors_h.sh ${CMAKE_SOURCE_DIR}/AUTHORS ${CMAKE_CURRENT_BINARY_DIR}/tools/darktable_authors.h
  COMMENT "Generating authors.h for about dialog."
)

add_custom_target(
  generate_authors_h ALL
  DEPENDS ${CMAKE_SOURCE_DIR}/tools/authors_h.sh ${CMAKE_SOURCE_DIR}/AUTHORS ${CMAKE_CURRENT_BINARY_DIR}/tools/darktable_authors.h
  WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)
