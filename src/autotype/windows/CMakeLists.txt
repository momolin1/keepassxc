set(autotype_win_SOURCES AutoTypeWindows.cpp)

add_library(keepassxc-autotype-windows MODULE ${autotype_win_SOURCES})

# This section ensures Windows Hello symbols are found during the link phase
if(WINSDK)
    target_link_libraries(keepassxc-autotype-windows ${WINSDK})
endif()

if(MSVC)
    # Necessary for WinRT/Biometric communication
    target_link_libraries(keepassxc-autotype-windows runtimeobject.lib)
endif()

# Links to the core library and Qt
target_link_libraries(keepassxc-autotype-windows keepassx_core ${autotype_LIB} Qt5::Core Qt5::Widgets)

install(TARGETS keepassxc-autotype-windows
        BUNDLE DESTINATION . COMPONENT Runtime
        LIBRARY DESTINATION ${PLUGIN_INSTALL_DIR} COMPONENT Runtime)
