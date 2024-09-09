# CMakeLists.txt for SQLite3
#
#
cmake_minimum_required(VERSION 3.8)

project(SQLite3
    LANGUAGES C
    VERSION 3.46.1
)

set(BUILD_SHARED_LIBS ON)

add_definitions(-DSQLITE_ENABLE_RTREE)
add_definitions(-DSQLITE_ENABLE_FTS3)
add_definitions(-DSQLITE_ENABLE_FTS4)
add_definitions(-DSQLITE_ENABLE_FTS5)
add_definitions(-DSQLITE_ENABLE_JSON1)
add_definitions(-DSQLITE_ENABLE_RBU)
add_definitions(-DSQLITE_ENABLE_STAT4)
add_definitions(-DSQLITE_ENABLE_RTREE)
add_definitions(-DSQLITE_ENABLE_DBSTAT_VTAB)
add_definitions(-DSQLITE_ENABLE_RBU)
add_definitions(-DSQLITE_ENABLE_SESSION)

## Comment this line out for threaded variant ( Using single right now because threads gave me issues )
#add_definitions(-DSQLITE_THREADSAFE=0)

set(Sources
    src/shell.c
    src/sqlite3.c
)

set(Headers
    src/sqlite3.h
    src/sqlite3ext.h
)

set(StaticLibraries
)

set(SharedLibraries
    dl
    pthread
)

add_library(${PROJECT_NAME} ${Sources})

target_link_libraries(${PROJECT_NAME} ${Shared_Libraries} ${Static_Libraries})

target_include_directories(${PROJECT_NAME}
	PUBLIC
		$<INSTALL_INTERFACE:include>
		$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
	PRIVATE
		${CMAKE_CURRENT_SOURCE_DIR}
)

set_target_properties(${PROJECT_NAME}
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
	VERSION ${PROJECT_VERSION}
	SOVERSION ${PROJECT_VERSION_MAJOR}
)