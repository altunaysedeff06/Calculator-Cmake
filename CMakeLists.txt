cmake_minimum_required(VERSION 3.16)
project(QtCalc LANGUAGES CXX)

# Qt6 varsa onu, yoksa Qt5'i deneyelim
find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets)

set(CMAKE_CXX_STANDARD 17)

target_sources(HesapMakinesi
  PRIVATE
    qml.qrc
    style.qss
    style.qrc
)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(PROJECT_SOURCES
    src/main.cpp
    src/mainwindow.cpp
    src/mainwindow.h
    src/mainwindow.ui
    resources/styles.qss
    qml.qrc
)

qt_add_resources(APP_QRC qml.qrc)

if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_executable(QtCalc
        MANUAL_FINALIZATION
        ${PROJECT_SOURCES}
        ${APP_QRC}
    )
else()
    add_executable(QtCalc
        ${PROJECT_SOURCES}
        ${APP_QRC}
    )
    target_link_libraries(QtCalc PRIVATE Qt${QT_VERSION_MAJOR}::Widgets)
endif()

target_link_libraries(QtCalc PRIVATE Qt${QT_VERSION_MAJOR}::Widgets)

if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_executable(QtCalc)
endif()
