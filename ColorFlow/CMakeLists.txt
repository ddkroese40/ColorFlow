cmake_minimum_required(VERSION 3.16)

project(ColorFlow VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SOURCE_FILES
        gamelogic.cpp
        gamelogic.h
        gamesolver.cpp
        gamesolver.h
        main.cpp)

#find_package(Qt6 6.2 COMPONENTS Quick REQUIRED)
find_package(Qt6 6.2  COMPONENTS Qml Core Quick Widgets Gui REQUIRED)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Instruct CMake to run tools automatically when needed.
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

qt_add_executable(appColorFlow
    main.cpp
    gamelogic.cpp
    gamelogic.h
    gamesolver.cpp
    gamesolver.h
)

qt_add_qml_module(appColorFlow
    URI ColorFlow
    VERSION 1.0
    QML_FILES BoardCircle.qml
    QML_FILES BoardGrid.qml
    QML_FILES BoardLine.qml
    QML_FILES ClickableSquare.qml
    QML_FILES FollowMouseCircle.qml
    QML_FILES GameBoard.qml
    QML_FILES HelpDialog.qml
    QML_FILES main.qml
    QML_FILES MainView.qml
)

set_target_properties(appColorFlow PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(appColorFlow
    PRIVATE Qt6::Quick)

install(TARGETS appColorFlow
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
