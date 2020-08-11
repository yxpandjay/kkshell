cmake_minimum_required(VERSION 3.5)

project(kkshell LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
include_directories(.)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt5 COMPONENTS Core Widgets LinguistTools REQUIRED)

add_subdirectory(thirdparty)
add_subdirectory(common)
add_subdirectory(terminal)

set(TS_FILES resources/lang/kkshell_zh_CN.ts)
set(FORM_FILES resources/forms/mainwindow.ui resources/forms/settings.ui resources/forms/session_manager.ui)
set(QRC_FILES resources/resources.qrc)
set(SRC_FILES main.cpp mainwindow.cpp widget/command_button.cpp settings.cpp session_manager.cpp)

add_executable(kkshell
        ${SRC_FILES}
        ${FORM_FILES}
        ${TS_FILES}
        ${QRC_FILES}
        )

set(THIRD_PARTY_LIBS simpleini)
set(PROJECT_LIBS config terminals)

target_link_libraries(kkshell PRIVATE Qt5::Core Qt5::Widgets ${THIRD_PARTY_LIBS} ${PROJECT_LIBS})

qt5_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})