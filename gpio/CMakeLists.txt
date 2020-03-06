cmake_minimum_required(VERSION 3.13)

project(gpio)

# Must use GNUInstallDirs to install libraries into correct locations on all platforms.
include(GNUInstallDirs)

include_directories(${PROJECT_SOURCE_DIR}/devLib)
include_directories(${PROJECT_SOURCE_DIR}/wiringPi)

set(SRC_FILES
	gpio.c readall.c
)

add_executable(gpio ${SRC_FILES})
target_include_directories(gpio PUBLIC
       ${PROJECT_SOURCE_DIR}/../devLib
)
target_link_libraries(gpio wiringPi wiringPiDev pthread m crypt rt)

# 'make install' to the correct locations (provided by GNUIns    tallDirs).
install(TARGETS gpio EXPORT rpi
    ARCHIVE  DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY  DESTINATION ${CMAKE_INSTALL_BINDIR}
    RUNTIME  DESTINATION ${CMAKE_INSTALL_BINDIR}
)
