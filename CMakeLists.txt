cmake_minimum_required(VERSION 3.9)
set(TARGET arauwyr)
set(arauwyr_VERSION 0.0.1)

set(QT_MODULES Widgets)
find_qt_modules("${QT_MODULES}") # MUST USE QUOTES TOO!!!

set(project_SRCS
	
)

SET(project_MOC_HDRS
	
)

SET(project_UIS
	
)

SET(project_HDRS
	
)

set(RESOURCE
	
)

qt5_add_resources(RESOURCE_ADDED ${RESOURCE})

QT5_WRAP_CPP(project_MOC_SRCS ${project_MOC_HDRS} OPTIONS ${MOC_OPTIONS})
QT5_WRAP_UI(project_UIS_H ${project_UIS})

# Don't forget to include output directory, otherwise the MOC and UI header won't be found
include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_executable(${TARGET} ${project_SRCS} ${project_MOC_SRCS} ${project_UIS_H} ${project_HDRS} ${RESOURCE_ADDED})
target_link_libraries(${TARGET})
qt5_use_modules(${TARGET}${QT_MODULES})

if(DEFINED ENV{BUILDCOUNTER})
	SET( VERSION_STRING ${arauwyr_VERSION}.$ENV{BUILDCOUNTER} )
else()
	SET( VERSION_STRING ${arauwyr_VERSION}.dev )
endif()

set_target_properties(${TARGET} PROPERTIES VERSION ${VERSION_STRING})