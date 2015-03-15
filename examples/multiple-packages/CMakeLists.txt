project(multiple-package)
cmake_minimum_required(VERSION 2.8)

install(FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/multiple-packages.bin
    ${CMAKE_CURRENT_SOURCE_DIR}/multiple-packages.conf
    DESTINATION /opt/multiple-packages
    COMPONENT bin
)

install(FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/multiple-packages.lib
    DESTINATION /opt/multiple-packages
    COMPONENT lib
)

set(DEB_PACKAGE_COMPONENTS "bin" "lib")

set(DEB_PACKAGE_bin_NAME "${CMAKE_PROJECT_NAME}-bin")
set(DEB_PACKAGE_bin_VERSION "0.1.1")
set(DEB_PACKAGE_bin_SECTION "utils")
set(DEB_PACKAGE_bin_CONFLICTS "single-package")
set(DEB_PACKAGE_bin_DEPENDS "${CMAKE_PROJECT_NAME}-lib")
set(DEB_PACKAGE_bin_DESRCIPTION "Test package")
set(DEB_PACKAGE_bin_MAINTAINER "Foo Bar <foobar@foo.bar>")
set(DEB_PACKAGE_bin_CONTROL_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/debian/postinst
    ${CMAKE_CURRENT_SOURCE_DIR}/debian/conffiles
)

set(DEB_PACKAGE_lib_NAME "${CMAKE_PROJECT_NAME}-lib")
set(DEB_PACKAGE_lib_VERSION "0.4.12")
set(DEB_PACKAGE_lib_SECTION "utils")
set(DEB_PACKAGE_lib_DESRCIPTION "Test package")
set(DEB_PACKAGE_lib_MAINTAINER "Foo Bar <foobar@foo.bar>")

include(../../deb_packaging.cmake)
