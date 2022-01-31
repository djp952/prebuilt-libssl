#LIBSSL 3.0.1
[https://www.openssl.org/](https://www.openssl.org/)   
  
**TARGETS**   
* windows-win32-v141   
* windows-x64-v141   
* uwp-win32-v141   
* uwp-x64-v141   
* uwp-arm-v141   
* linux-i686 (gcc-4.9)   
* linux-x86_64 (gcc-4.9)   
* linux-armel (gcc-4.9)   
* linux-armhf (gcc-4.9)   
* linux-aarch64 (gcc-4.9)   
* android-21-armeabi-v7a (ndk-r20b/api-21)   
* android-21-arm64-v8a (ndk-r20b/api-21)  
* android-21-x86 (ndk-r20b/api-21)  
* android-21-x86_64 (ndk-r20b/api-21)  
* rasbpian-armhf (gcc-4.8.3)   
* osx-x86_64 (apple-darwin15)   
   
**BUILD ENVIRONMENT**  
* Windows 10 x64 20H2 (19042) or later   
* Visual Studio 2022 Community Edition or higher with:    
     * Desktop Development with C++
     * Universal Windows Platform Development
     * Windows 10 SDK (10.0.18362.0)   
     * C++ v141 Universal Windows Platform Tools   

* [Strawberry PERL for Windows](https://strawberryperl.com/)   
* [Netwide Assembler (NASM)](https://www.nasm.us/)   
* [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (WSL v1 recommended)   
* [WSL Ubuntu 18.04 LTS Distro](https://www.microsoft.com/store/productId/9N9TNGVNDL3Q)   
   
**CONFIGURE UBUNTU ON WINDOWS**   
* Open "Ubuntu 18.04 LTS"   
```
sudo dpkg --add-architecture i386
sudo add-apt-repository 'deb http://archive.ubuntu.com/ubuntu/ xenial main universe'
sudo apt-get update
sudo apt-get install gcc-4.9 g++-4.9 libc6-dev:i386 libstdc++-4.9-dev:i386 lib32gcc-4.9-dev
sudo apt-get install gcc-4.9-arm-linux-gnueabihf g++-4.9-arm-linux-gnueabihf gcc-4.9-arm-linux-gnueabi g++-4.9-arm-linux-gnueabi gcc-4.9-aarch64-linux-gnu g++-4.9-aarch64-linux-gnu
sudo apt-get install autoconf libtool make p7zip-full python
```
   
**CONFIGURE ANDROID TOOLCHAINS**   
* Open "Ubuntu 18.04 LTS"   
```
wget https://dl.google.com/android/repository/android-ndk-r20b-linux-x86_64.zip
7z x android-ndk-r20b-linux-x86_64.zip
```
  
**CONFIGURE OSXCROSS CROSS-COMPILER**   
* Generate the MAC OSX 10.11 SDK Package for OSXCROSS by following the instructions provided at [PACKAGING THE SDK](https://github.com/tpoechtrager/osxcross#packaging-the-sdk).  The suggested version of Xcode to use when generating the SDK package is Xcode 7.3.1 (May 3, 2016).
* Open "Ubuntu 18.04 LTS"   
```
sudo apt-get install cmake clang llvm-dev libxml2-dev uuid-dev libssl-dev libbz2-dev zlib1g-dev
git clone https://github.com/tpoechtrager/osxcross --depth=1
cp {MacOSX10.11.sdk.tar.bz2} osxcross/tarballs/
UNATTENDED=1 osxcross/build.sh
osxcross/build_compiler_rt.sh
sudo mkdir -p /usr/lib/llvm-6.0/lib/clang/6.0.0/include
sudo mkdir -p /usr/lib/llvm-6.0/lib/clang/6.0.0/lib/darwin
sudo cp -rv $(pwd)/osxcross/build/compiler-rt/compiler-rt/include/sanitizer /usr/lib/llvm-6.0/lib/clang/6.0.0/include
sudo cp -v $(pwd)/osxcross/build/compiler-rt/compiler-rt/build/lib/darwin/*.a /usr/lib/llvm-6.0/lib/clang/6.0.0/lib/darwin
sudo cp -v $(pwd)/osxcross/build/compiler-rt/compiler-rt/build/lib/darwin/*.dylib /usr/lib/llvm-6.0/lib/clang/6.0.0/lib/darwin
```
   
**BUILD LIBSSL (windows-win32-v141)**   
Open "Command Prompt"   
```
"C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvarsall.bat" x86 -vcvars_ver=14.1
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
cd openssl
perl Configure VC-WIN32 no-zlib no-tests
nmake
```
   
Get header files from openssl\\include   
Get libssl_static.lib, libcrypto_static.lib, and ossl_static.pdb from openssl  
      
**BUILD LIBSSL (windows-x64-v141)**   
Open "Command Prompt"   
```
"C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvarsall.bat" x64 -vcvars_ver=14.1
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
cd openssl
perl Configure VC-WIN64A no-zlib no-tests
nmake
```
   
Get header files from openssl\\include   
Get libssl_static.lib, libcrypto_static.lib, and ossl_static.pdb from openssl  
      
**BUILD LIBSSL (uwp-win32-v141)**   
Open "Command Prompt"   
```
"C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvarsall.bat" x86 uwp -vcvars_ver=14.1
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
cd openssl
perl Configure VC-WIN32-UWP no-zlib no-tests no-secure-memory
nmake
```
   
Get header files from openssl\\include   
Get libssl_static.lib, libcrypto_static.lib, and ossl_static.pdb from openssl  
      
**BUILD LIBSSL (uwp-x64-v141)**   
Open "Command Prompt"   
```
"C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvarsall.bat" x64 uwp -vcvars_ver=14.1
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
cd openssl
perl Configure VC-WIN64A-UWP no-zlib no-tests no-secure-memory
nmake
```
   
Get header files from openssl\\include   
Get libssl_static.lib, libcrypto_static.lib, and ossl_static.pdb from openssl  
      
**BUILD LIBSSL (uwp-arm-v141)**   
Open "Command Prompt"   
```
"C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvarsall.bat" x86_arm uwp -vcvars_ver=14.1
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
cd openssl
perl Configure VC-WIN32-ARM-UWP no-zlib no-tests no-secure-memory
nmake
```
   
Get header files from openssl\\include   
Get libssl_static.lib, libcrypto_static.lib, and ossl_static.pdb from openssl  
      
**BUILD LIBSSL (linux-i686)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export CC=gcc-4.9
export AR=gcc-ar-4.9
export RANLIB=gcc-ranlib-4.9
export CFLAGS="-m32 -I/usr/include/i386-linux-gnu"
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests linux-x86 -fPIC
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl   

**BUILD LIBSSL (linux-x86_64)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export CC=gcc-4.9
export AR=gcc-ar-4.9
export RANLIB=gcc-ranlib-4.9
export CFLAGS="-I/usr/include/x86_64-linux-gnu"
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests linux-x86_64 -fPIC
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl   
   
**BUILD LIBSSL (linux-armel)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export CC=arm-linux-gnueabi-gcc-4.9
export AR=arm-linux-gnueabi-gcc-ar-4.9
export RANLIB=arm-linux-gnueabi-gcc-ranlib-4.9
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests linux-generic32 -fPIC
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl   
   
**BUILD LIBSSL (linux-armhf)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export CC=arm-linux-gnueabihf-gcc-4.9
export AR=arm-linux-gnueabihf-gcc-ar-4.9
export RANLIB=arm-linux-gnueabihf-gcc-ranlib-4.9
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests linux-generic32 -fPIC
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl   
   
**BUILD LIBSSL (linux-aarch64)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export CC=aarch64-linux-gnu-gcc-4.9
export AR=aarch64-linux-gnu-gcc-ar-4.9
export RANLIB=aarch64-linux-gnu-gcc-ranlib-4.9
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests linux-aarch64 -fPIC
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl   
   
**BUILD LIBSSL (android-21-armeabi-v7a)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export ANDROID_NDK_ROOT=$(pwd)/android-ndk-r20b
export PATH=$ANDROID_NDK_ROOT/toolchains/llvm/prebuilt/linux-x86_64/bin:$ANDROID_NDK_ROOT/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin:$PATH
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests android-arm -fPIC -D__ANDROID_API__=21
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl    
   
**BUILD LIBSSL (android-21-arm64-v8a)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export ANDROID_NDK_ROOT=$(pwd)/android-ndk-r20b
export PATH=$ANDROID_NDK_ROOT/toolchains/llvm/prebuilt/linux-x86_64/bin:$ANDROID_NDK_ROOT/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin:$PATH
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests android-arm64 -fPIC -D__ANDROID_API__=21
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl    
   
**BUILD LIBSSL (android-21-x86)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export ANDROID_NDK_ROOT=$(pwd)/android-ndk-r20b
export PATH=$ANDROID_NDK_ROOT/toolchains/llvm/prebuilt/linux-x86_64/bin:$ANDROID_NDK_ROOT/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin:$PATH
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests android-x86 -latomic -fPIC -D__ANDROID_API__=21
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl    
   
**BUILD LIBSSL (android-21-x86_64)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export ANDROID_NDK_ROOT=$(pwd)/android-ndk-r20b
export PATH=$ANDROID_NDK_ROOT/toolchains/llvm/prebuilt/linux-x86_64/bin:$ANDROID_NDK_ROOT/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin:$PATH
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests android-x86_64 -latomic -fPIC -D__ANDROID_API__=21
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl    
   
**BUILD LIBSSL (raspbian-armhf)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export PATH=$(pwd)/raspberrypi/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin:$PATH
export CC=arm-linux-gnueabihf-gcc
export AR=arm-linux-gnueabihf-gcc-ar
export RANLIB=arm-linux-gnueabihf-gcc-ranlib
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests linux-generic32 -fPIC
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl   
   
**BUILD LIBSSL (osx-x86_64)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/openssl/openssl.git -b openssl-3.0.1 --depth=1
export PATH=$(pwd)/osxcross/target/bin:$PATH
export CC=x86_64-apple-darwin15-clang
export AR=x86_64-apple-darwin15-ar
export RANLIB=x86_64-apple-darwin15-ranlib
export CFLAGS="-mmacosx-version-min=10.9 -stdlib=libc++"
export CPPFLAGS="-I$(pwd)/prebuilt-libz/osx-x86_64/include"
export LDFLAGS="-L$(pwd)/prebuilt-libz/osx-x86_64/lib" 
export LIBS=-ldl
cd openssl
./Configure no-shared no-zlib no-tests darwin64-x86_64-cc -fPIC
make
```
   
Get header files from openssl/include   
Get libssl.a and libcrypto.a from openssl   
   