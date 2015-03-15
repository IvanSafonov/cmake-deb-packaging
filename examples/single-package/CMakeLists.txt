project(single-package)
cmake_minimum_required(VERSION 2.8)

install(FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/single-package.file
    ${CMAKE_CURRENT_SOURCE_DIR}/single-package.conf
    DESTINATION /opt/single-package
)

set(DEB_PACKAGE_NAME ${CMAKE_PROJECT_NAME})
set(DEB_PACKAGE_VERSION "0.2.2")
set(DEB_PACKAGE_SECTION "utils")
set(DEB_PACKAGE_DESRCIPTION "Test package")
set(DEB_PACKAGE_MAINTAINER "Foo Bar <foobar@foo.bar>")
set(DEB_PACKAGE_ARCH "all")
set(DEB_PACKAGE_CONTROL_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/debian/postinst
    ${CMAKE_CURRENT_SOURCE_DIR}/debian/conffiles
)

include(../../deb_packaging.cmake)
