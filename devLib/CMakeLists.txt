cmake_minimum_required(VERSION 3.13)

project(devLib)

# Must use GNUInstallDirs to install libraries into correct locations on all platforms.
include(GNUInstallDirs)

set(SRC_FILES
        ds1302.c
        gertboard.c
        lcd.c
        lcd128x64.c
        maxdetect.c
        piFace.c
        piGlow.c
        piNes.c
        scrollPhat.c
)

SET(HEADER_FILES
        ds1302.h
        font.h
        gertboard.h
        lcd.h
        lcd128x64.h
        maxdetect.h
        piFace.h
        piGlow.h
        piNes.h
        scrollPhat.h
        scrollPhatFont.h
)

add_library(wiringPiDev SHARED ${SRC_FILES})
set_target_properties(wiringPiDev PROPERTIES OUTPUT_NAME "wiringPiDev")
target_include_directories(wiringPiDev PUBLIC
       ${PROJECT_SOURCE_DIR}/../wiringPi
)

install(FILES ${HEADER_FILES} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(TARGETS wiringPiDev EXPORT rpi
    ARCHIVE  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY  DESTINATION ${CMAKE_INSTALL_LIBDIR}
)
