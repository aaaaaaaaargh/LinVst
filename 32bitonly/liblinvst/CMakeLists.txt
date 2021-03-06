
# Compile Flags.
################
SET(STATIC_LINKING FALSE )

set( CMAKE_CXX_STANDARD 14 )
set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pipe -fPIC -O2 -DLVRT -DEMBED -DVST32 -DEMBEDDRAG -DWAVES -DVESTIGE ")

# Project Path.
###############
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)

link_directories(${CMAKE_LIBRARY_OUTPUT_DIRECTORY})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

set( CMAKE_CXX_COMPILER /usr/bin/c++ )

set( LINVST_SO_SRC SHARED
  ../../linvst.cpp
  ../../remotevstclient.cpp
  ../../remotepluginclient.cpp
  ../../paths.cpp
  )

add_library(linvst-i386 ${LINVST_SO_SRC} )
set_target_properties(linvst-i386 PROPERTIES PREFIX "")
target_link_libraries( linvst-i386 pthread dl X11 rt )

install( TARGETS linvst-i386 DESTINATION share/LinVst )
