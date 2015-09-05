# CMakeLists.txt
#
# Copyright 2013, 2014 by
# David Turner, Robert Wilhelm, and Werner Lemberg.
#
# Written by John Cary <cary@txcorp.com>
# Modified by Borislav Stanimirov
#
# This file is part of the FreeType project, and may only be used, modified,
# and distributed under the terms of the FreeType project license,
# LICENSE.TXT.  By continuing to use, modify, or distribute this file you
# indicate that you have read the license and understand and accept it
# fully.
#
# Simplified version of the one by John Cary
# To be used as part of other projects and not be bult or installed separately

project(freetype)

# Compiler definitions for building the library
add_definitions(-DFT2_BUILD_LIBRARY)

if(MSVC)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
endif()

# Specify library include directories
set(FREETYPE_INCLUDE_DIR
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    CACHE STRING "Freetype include path"
)
include_directories("${FREETYPE_INCLUDE_DIR}")

file(GLOB PUBLIC_HEADERS "include/*.h")
file(GLOB PUBLIC_CONFIG_HEADERS "include/config/*.h")
file(GLOB PRIVATE_HEADERS "include/internal/*.h")

set(BASE_SRCS
  src/autofit/autofit.c
  src/base/ftadvanc.c
  src/base/ftbbox.c
  src/base/ftbdf.c
  src/base/ftbitmap.c
  src/base/ftcalc.c
  src/base/ftcid.c
  src/base/ftdbgmem.c
  src/base/ftdebug.c
  src/base/ftfstype.c
  src/base/ftgasp.c
  src/base/ftgloadr.c
  src/base/ftglyph.c
  src/base/ftgxval.c
  src/base/ftinit.c
  src/base/ftlcdfil.c
  src/base/ftmm.c
  src/base/ftobjs.c
  src/base/ftotval.c
  src/base/ftoutln.c
  src/base/ftpatent.c
  src/base/ftpfr.c
  src/base/ftrfork.c
  src/base/ftsnames.c
  src/base/ftstream.c
  src/base/ftstroke.c
  src/base/ftsynth.c
  src/base/ftsystem.c
  src/base/fttrigon.c
  src/base/fttype1.c
  src/base/ftutil.c
  src/base/ftwinfnt.c
  src/base/ftxf86.c
  src/bdf/bdf.c
  src/bzip2/ftbzip2.c
  src/cache/ftcache.c
  src/cff/cff.c
  src/cid/type1cid.c
  src/gzip/ftgzip.c
  src/lzw/ftlzw.c
  src/pcf/pcf.c
  src/pfr/pfr.c
  src/psaux/psaux.c
  src/pshinter/pshinter.c
  src/psnames/psmodule.c
  src/raster/raster.c
  src/sfnt/sfnt.c
  src/smooth/smooth.c
  src/truetype/truetype.c
  src/type1/type1.c
  src/type42/type42.c
  src/winfonts/winfnt.c
)

#~ include_directories("src/truetype")
#~ include_directories("src/sfnt")
#~ include_directories("src/autofit")
#~ include_directories("src/smooth")
#~ include_directories("src/raster")
#~ include_directories("src/psaux")
#~ include_directories("src/psnames")

add_library(freetype STATIC
  ${PUBLIC_HEADERS}
  ${PUBLIC_CONFIG_HEADERS}
  ${PRIVATE_HEADERS}
  ${BASE_SRCS}
)

set(FREETYPE_LINK_DIR
    ${CMAKE_CURRENT_BINARY_DIR}
    CACHE STRING "freetype link path"
)

set(FREETYPE_LIB
    freetype
    CACHE STRING "freetype library"
)

set_target_properties(freetype PROPERTIES FOLDER ThirdParty)
