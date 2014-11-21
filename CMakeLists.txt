IF(BIICODE)
  include(${CMAKE_HOME_DIRECTORY}/biicode.cmake)
  # Initializes block variables
  INIT_BIICODE_BLOCK()
  # Include base block directory
  ADD_BIICODE_TARGETS()
  TARGET_INCLUDE_DIRECTORIES(${BII_LIB_TARGET} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
  TARGET_COMPILE_DEFINITIONS(${BII_LIB_TARGET} PUBLIC -DESTD_HAS_EXCEPTIONS)
  TARGET_COMPILE_OPTIONS(${BII_LIB_TARGET} PUBLIC -Wall -pedantic)
ELSE()
	#Previous CMakeLists.txt goes herecmake_minimum_required(VERSION 2.8.4)
	project(estl)

	#set(CMAKE_CXX_FLAGS "-Wall -std=c++98")
	set(CMAKE_CXX_FLAGS "-Wall -pedantic")

	#add_definitions(-DGTEST_LANG_CXX11=0)
	add_definitions(-DESTD_HAS_EXCEPTIONS)

	include_directories(
	    include
	)

	set(LIB_FILES
	    src/estd/assert.cpp
	)
	add_library(estl STATIC ${LIB_FILES})

	add_executable(vector1 examples/estd/vector1.cpp)
	add_executable(vector2 examples/estd/vector2.cpp)
	add_executable(vector3 examples/estd/vector3.cpp)

	target_link_libraries(vector1 estl)
	target_link_libraries(vector2 estl)
	target_link_libraries(vector3 estl)
ENDIF()
