# CMake module for build debian packages

Adds a target **deb_package** to the project that builds package(s).

## Debian control file parameters
More information about deb-control file at: http://manpages.ubuntu.com/manpages/trusty/man5/deb-control.5.html

**Required parameters:**

* **DEB_PACKAGE_NAME** - Package name
* **DEB_PACKAGE_VERSION** - Version
* **DEB_PACKAGE_DESRCIPTION** - Description
* **DEB_PACKAGE_MAINTAINER** - Maintainer

**Optional parameters:**

* **DEB_PACKAGE_ARCH** - Architecture
* **DEB_PACKAGE_SECTION** - Section
* **DEB_PACKAGE_ORIGIN** - Origin
* **DEB_PACKAGE_BUGS** - Bugs
* **DEB_PACKAGE_HOMEPAGE** - Homepage
* **DEB_PACKAGE_DEPENDS** - Depends
* **DEB_PACKAGE_PREDEPENDS** - Pre-Depends
* **DEB_PACKAGE_RECOMMENDS** - Recommends
* **DEB_PACKAGE_SUGGESTS** - Suggests
* **DEB_PACKAGE_BREAKS** - Breaks
* **DEB_PACKAGE_CONFLICTS** - Conflicts
* **DEB_PACKAGE_REPLACES** - Replaces
* **DEB_PACKAGE_PROVIDES** - Provides

## Module parameters

* **DEB_PACKAGE_CONTROL_FILES** - additional debian control files (postint, prerm, etc)
* **DEB_PACKAGE_COMPONENTS** - cmake components to build as separate packages. If is set, deb-control parameters should be changed to **DEB_PACKAGE_COMPOTENT_PARAMETER**


## Single package example:

```cmake
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
```
**Building:**

```bash
cd examples/single-package
mkdir build
cd build
cmake ..
make deb_package
```

## Multiple packages example:

```cmake
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
```
**Building:**

```bash
cd examples/multiple-packages
mkdir build
cd build
cmake ..
make deb_package
```
