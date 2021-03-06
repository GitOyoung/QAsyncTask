cmake_minimum_required(VERSION 2.8.3)
project(QAsyncTask)

add_definitions(-std=c++11)
set(CMAKE_CXX_FLAGS "-g")
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt5Widgets REQUIRED)
#find_package(Qt5Network REQUIRED)
include_directories(
		${PROJECT_SOURCE_DIR}/include
		${Qt5Widgets_INCLUDE_DIRS}
		${Qt5Network_INCLUDE_DIRS}
)

link_directories(/usr/local/lib)


aux_source_directory(src SRC_LIST)
set(INC_LIST
	include/qasynctaskcreator.h
	include/qasynctaskcreator.h  
	include/qasynctaskresponseevent.h
	include/qasynctaskevent.h    
	include/qasynctaskreactor.h  
	include/qasynctaskresult.h
)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)

set(QASYNC_SRC_LIST ${SRC_LIST} ${INC_LIST})

add_library(qasync  ${QASYNC_SRC_LIST})
target_link_libraries(qasync
		Qt5::Widgets
#		Qt5::Network
		)

add_executable(main
		demo/mainwindow.ui
		demo/mainwindow.h
		demo/mainwindow.cc
		demo/main.cc

		)
target_link_libraries(main qasync pthread)
