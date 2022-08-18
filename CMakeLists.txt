cmake_minimum_required (VERSION 3.8.2)
set(PROJECT lumina-config)
project(${PROJECT})

# Find includes in the build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Turn on automatic invocation of the MOC, UIC & RCC
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

# Add a compiler flag
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

#Find pkgconfig
find_package(PkgConfig REQUIRED)

# Dependencies
find_package(Qt5 REQUIRED COMPONENTS Widgets X11Extras Network)
pkg_check_modules(LUMINA REQUIRED lumina)

# Tell CMake to create the executable
add_executable(${PROJECT}
 main.cpp
 mainWindow.cpp
 LPlugins.cpp
 ColorDialog.cpp
 ThemeDialog.cpp
 GetPluginDialog.cpp
 ScriptDialog.cpp
 pages/PageWidget.h
 globals.h
 AppDialog.h
 PanelWidget.cpp
 pages/getPage.cpp
 pages/page_main.cpp
 pages/page_wallpaper.cpp
 pages/page_autostart.cpp
 pages/page_defaultapps.cpp
 pages/page_fluxbox_keys.cpp
 pages/page_fluxbox_settings.cpp
 pages/page_interface_desktop.cpp
 pages/page_interface_menu.cpp
 pages/page_interface_panels.cpp
 pages/page_session_locale.cpp
 pages/page_session_options.cpp
 pages/page_compton.cpp
 pages/page_soundtheme.cpp
)

# Add the dependencies for linking
target_link_libraries(${PROJECT}
 Qt5::Widgets
 Qt5::X11Extras
 Qt5::Network
 ${LUMINA_LIBRARIES}
)

# Include header files
include_directories(
    ${LUMINA_INCLUDE_DIRS}
)

install(TARGETS ${PROJECT} RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}")
install(FILES "resources/lumina-config.desktop" DESTINATION "${CMAKE_INSTALL_DATADIR}/applications")

