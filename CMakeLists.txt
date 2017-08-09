cmake_minimum_required(VERSION 2.5)

project(arauwyr)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)

set(TARGET arauwyr)
set(arauwyr_VERSION 0.0.1)

set(project_sources
	mainwindow.cpp
	main.cpp
)

set(project_headers
	mainwindow.hpp
)

SET(project_UIS
	mainwindow.ui
)

add_executable(${TARGET} ${project_sources} ${project_headers} ${project_UIS})

set(Qt5_BASE_DIR ${CMAKE_SOURCE_DIR}/3rdparty/qt5/gcc_64 CACHE STRING
	"Qt5_BASE_DIR directory"
	FORCE)


include_directories(${CMAKE_CURRENT_DIR})
# Don't forget to include output directory, otherwise the MOC and UI header won't be found
include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# Must use like this:
# set(QT_MODULES Core Widgets)
# find_qt_modules("${QT_MODULE}") # MUST USE QUOTES HERE!!!
macro(find_qt_modules TO_FIND_MODULES)
	foreach(QT_Module ${TO_FIND_MODULES})
		set(Qt5${QT_Module}_DIR ${Qt5_BASE_DIR}/lib/cmake/Qt5${QT_Module})
		find_package(Qt5${QT_Module} REQUIRED)
	endforeach(QT_Module)
endmacro(find_qt_modules)

set(QT_MODULES Core Gui Network OpenGL PrintSupport Qml Quick Script SerialPort Test WebKit WebKitWidgets Widgets Xml)
set(QT_VERSION 5.6)

find_qt_modules("${QT_MODULES}")
qt5_use_modules( ${TARGET} ${QT_MODULES})





if(DEFINED ENV{BUILDCOUNTER})
	SET( VERSION_STRING ${arauwyr_VERSION}.$ENV{BUILDCOUNTER} )
else()
	SET( VERSION_STRING ${arauwyr_VERSION}.dev )
endif()

#set_target_properties(${TARGET} PROPERTIES VERSION ${VERSION_STRING})
