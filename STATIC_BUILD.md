## Static Build CppREST

### Install vcpkg to C:\src\vcpkg

[https://github.com/Microsoft/vcpkg](https://github.com/Microsoft/vcpkg)

    > cd c:\src
    > git clone https://github.com/Microsoft/vcpkg.git
    > cd vcpkg

    PS> .\bootstrap-vcpkg.bat
    PS> .\vcpkg integrate install

Executing `.\vcpkg integrate install` will print text similar below:

    Applied user-wide integration for this vcpkg root.
    
    All MSBuild C++ projects can now #include any installed libraries.
    Linking will be handled automatically.
    Installing new libraries will make them instantly available.

    CMake projects should use: "-DCMAKE_TOOLCHAIN_FILE=C:/src/vcpkg/scripts/buildsystems/vcpkg.cmake"

### Install latest version of CMake

[https://cmake.org/download/](https://cmake.org/download/)

### Install cpprestsdk to specified directory

[https://github.com/Microsoft/cpprestsdk/wiki/How-to-build-for-Windows](https://github.com/Microsoft/cpprestsdk/wiki/How-to-build-for-Windows)

    > cd c:\src\vcpkg
    > .\vcpkg install --triplet x64-windows-static boost-system zlib openssl boost-date-time boost-regex websocketpp
    > .\vcpkg install --triplet x86-windows-static boost-system zlib openssl boost-date-time boost-regex websocketpp
    > .\vcpkg install --triplet x64-windows boost-system zlib openssl boost-date-time boost-regex websocketpp
    > .\vcpkg install --triplet x86-windows boost-system zlib openssl boost-date-time boost-regex websocketpp

Open **Developer Command Prompt for VS2019** and download cpprestsdk

    > git clone https://github.com/TangramDev/cpprestsdk.git
    > cd cpprestsdk
    > git checkout v2.10.12-static
    > mkdir build.x64v142
    > mkdir build.x64v142md
    > mkdir build.win32v142
    > mkdir build.win32v142md

### Generate VS2019 solutions and projects

Into directory build.xxx and run

    > cd build.x64v142
    > cmake ../Release -A x64 -DCMAKE_TOOLCHAIN_FILE=C:/src/vcpkg/scripts/buildsystems/vcpkg.cmake -DVCPKG_TARGET_TRIPLET=x64-windows-static -DBUILD_MULTI_THREADED_DLL=OFF
    > cd build.x64v142md
    > cmake ../Release -A x64 -DCMAKE_TOOLCHAIN_FILE=C:/src/vcpkg/scripts/buildsystems/vcpkg.cmake -DVCPKG_TARGET_TRIPLET=x64-windows-static -DBUILD_MULTI_THREADED_DLL=ON
    > cd build.win32v142
    > cmake ../Release -A Win32 -DCMAKE_TOOLCHAIN_FILE=C:/src/vcpkg/scripts/buildsystems/vcpkg.cmake -DVCPKG_TARGET_TRIPLET=x64-windows-static -DBUILD_MULTI_THREADED_DLL=OFF
    > cd build.win32v142md
    > cmake ../Release -A Win32 -DCMAKE_TOOLCHAIN_FILE=C:/src/vcpkg/scripts/buildsystems/vcpkg.cmake -DVCPKG_TARGET_TRIPLET=x64-windows-static -DBUILD_MULTI_THREADED_DLL=ON

### Build

Open `cpprestsdk.sln` with VS2019 and build `cpprest` project in Debug configuration and Release configuration.

### Find your libs

Into directory cpprestsdk/Binaries and you will find

- Debug
  - libcpprest142_2_10_md_d.lib
  - libcpprest142_2_10_d.lib
  - libcpprest142_2_10_64_md_d.lib
  - libcpprest142_2_10_64_d.lib
- Release
  - libcpprest142_2_10.lib
  - libcpprest142_2_10_64.lib
  - libcpprest142_2_10_64_md.lib
  - libcpprest142_2_10_md.lib



