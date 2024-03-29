### CMakeLists automatically created with AutoVala
### Do not edit

project (cronopete)
cmake_minimum_required (VERSION 2.6)
cmake_policy (VERSION 2.8)
list (APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
enable_testing ()

option(ICON_UPDATE "Update the icon cache after installing" ON)
option(BUILD_VALADOC "Build API documentation if Valadoc is available" OFF)
option(NO_APPINDICATOR "NO_APPINDICATOR" OFF)
option(USE_GTK2 "USE_GTK2" OFF)

set(HAVE_VALADOC OFF)
if(BUILD_VALADOC)
	find_package(Valadoc)
	if(VALADOC_FOUND)
		set(HAVE_VALADOC ON)
		include(Valadoc)
	else()
		message("Valadoc not found, will not build documentation")
	endif()
endif()

find_package(PkgConfig)

set(MODULES_TO_CHECK ${MODULES_TO_CHECK} gee-1.0)
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} cairo)
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} gsl)
IF ((NOT NO_APPINDICATOR) AND (NOT USE_GTK2))
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} appindicator3-0.1)
ENDIF()
IF ((NOT NO_APPINDICATOR) AND (USE_GTK2))
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} appindicator-0.1)
ENDIF()
IF (USE_GTK2)
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} gtk+-2.0)
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} gdk-2.0)
ELSE()
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} gtk+-3.0)
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} gdk-3.0)
set(MODULES_TO_CHECK ${MODULES_TO_CHECK} glib-2.0)
ENDIF()


pkg_check_modules(DEPS REQUIRED ${MODULES_TO_CHECK})

add_subdirectory(doc)
add_subdirectory(src)
add_subdirectory(po)
add_subdirectory(data/pixmaps)
add_subdirectory(data/interface2)
add_subdirectory(data)
add_subdirectory(data/icons)
add_subdirectory(data/interface)
