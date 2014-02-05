cmake_minimum_required (VERSION 2.8)

FOREACH(policy CMP0012 CMP0013 CMP0014)
  IF(POLICY ${policy})
    CMAKE_POLICY(SET ${policy} NEW)
  ENDIF()
ENDFOREACH()

PROJECT(SPHINXSEARCH)

IF(WIN32)
	# override default options which affects windows builds
	set(CMAKE_USER_MAKE_RULES_OVERRIDE ${CMAKE_CURRENT_SOURCE_DIR}/cmake/c_flag_overrides.cmake)
	set(CMAKE_USER_MAKE_RULES_OVERRIDE_CXX ${CMAKE_CURRENT_SOURCE_DIR}/cmake/cxx_flag_overrides.cmake)
ENDIF(WIN32)

SET(SPHINXSEARCH_CMAKE_DIR "${SPHINXSEARCH_SOURCE_DIR}/CMake")
SET(CMAKE_MODULE_PATH ${SPHINXSEARCH_SOURCE_DIR}/cmake)

if (NOT WIN32)
# debug build has to be selected from inside VS, so is obsolete here
OPTION(DEBUG_MODE "Build with debug mode" ON)
# dlopen doesn't affect windows anyway
OPTION(DL_EXPAT "Load libexpat using dlopen" ON)
endif (NOT WIN32)

#set(CMAKE_VERBOSE_MAKEFILE true)

include (helpers)

check_veryold_gcc()
add_subdirectory (src)