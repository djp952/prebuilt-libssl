#LIBSSL 1.0.2k
[https://www.openssl.org/](https://www.openssl.org/)   
  
**TARGETS**   
* linux-i686 (gcc-4.9)   
* linux-x86_64 (gcc-4.9)   
* android-armeabi-v7a (ndk-r12b/api-21)   
* android-arm64-v8a (ndk-r12b/api-21)  
   
**BUILD ENVIRONMENT**  
* Windows 10 x64 15025   
* Bash on Ubuntu on Windows 16.04.1 LTS   

**CONFIGURE BASH ON UBUNTU ON WINDOWS**   
Open "Bash on Ubuntu on Windows"   
```
sudo apt-get update
sudo apt-get install gcc g++ gcc-multilib g++-multilib gcc-4.9 g++-4.9 gcc-4.9-multilib g++-4.9-multilib
sudo apt-get install autoconf libtool make p7zip-full python
```

**CONFIGURE ANDROID TOOLCHAINS**   
Open "Bash on Ubuntu on Windows"   
```
wget https://dl.google.com/android/repository/android-ndk-r12b-linux-x86_64.zip
7z x android-ndk-r12b-linux-x86_64.zip
android-ndk-r12b/build/tools/make_standalone_toolchain.py --arch arm --api 21 --stl gnustl --install-dir ./arm-linux-androideabi
android-ndk-r12b/build/tools/make_standalone_toolchain.py --arch arm64 --api 21 --stl gnustl --install-dir ./aarch64-linux-android
android-ndk-r12b/build/tools/make_standalone_toolchain.py --arch x86 --api 21 --stl gnustl --install-dir ./i686-linux-android
```
  
**BUILD LIBSSL (linux-i686)**   
Open "Bash on Ubuntu on Windows"   
```
git clone https://github.com/openssl/openssl.git -b OpenSSL_1_0_2k --depth=1
export CC=gcc-4.9
export AR=gcc-ar-4.9
export RANLIB=gcc-ranlib-4.9
cd openssl
./Configure no-shared linux-generic32 -m32 -fPIC
make
```
   
Get header files from openssl/include (NOTE: Dereference symbolic links)   
Get libssl.a and libcrypto.a from openssl   

**BUILD LIBSSL (linux-x86_64)**   
Open "Bash on Ubuntu on Windows"   
```
git clone https://github.com/openssl/openssl.git -b OpenSSL_1_0_2k --depth=1
export CC=gcc-4.9
export AR=gcc-ar-4.9
export RANLIB=gcc-ranlib-4.9
cd openssl
./Configure no-shared linux-x86_64 -fPIC
make
```
   
Get header files from openssl/include (NOTE: Dereference symbolic links)   
Get libssl.a and libcrypto.a from openssl   
   
**BUILD LIBSSL (android-armeabi-v7a)**   
Open "Bash on Ubuntu on Windows"   
```
git clone https://github.com/openssl/openssl.git -b OpenSSL_1_0_2k --depth=1
export ANDROID_NDK_ROOT=$(pwd)/android-ndk-r12b
export PATH=$(pwd)/arm-linux-androideabi/bin:$PATH
export CROSS_COMPILE=arm-linux-androideabi-
cd openssl
./Configure no-shared no-asm no-zlib no-ssl2 no-ssl3 no-comp no-hw no-engine android-armv7 -fPIC -DOPENSSL_PIC -DDSO_DLFCN -DHAVE_DLFCN_H -mandroid -I$ANDROID_NDK_ROOT/platforms/android-21/arch-arm/usr/include -B$ANDROID_NDK_ROOT/platforms/android-21/arch-arm/usr/lib -O3 -fomit-frame-pointer -Wall
make depend
make
```
   
Get header files from openssl/include (NOTE: Dereference symbolic links)   
Get libssl.a and libcrypto.a from openssl    
   
**BUILD LIBSSL (android-arm64-v8a)**   
Open "Bash on Ubuntu on Windows"   
```
git clone https://github.com/openssl/openssl.git -b OpenSSL_1_0_2k --depth=1
export ANDROID_NDK_ROOT=$(pwd)/android-ndk-r12b
export PATH=$(pwd)/aarch64-linux-android/bin:$PATH
export CROSS_COMPILE=aarch64-linux-android-
cd openssl
./Configure no-shared no-asm no-zlib no-ssl2 no-ssl3 no-comp no-hw no-engine linux-generic64 -DB_ENDIAN -fPIC -DOPENSSL_PIC -DDSO_DLFCN -DHAVE_DLFCN_H -mandroid -I$ANDROID_NDK_ROOT/platforms/android-21/arch-arm64/usr/include -B$ANDROID_NDK_ROOT/platforms/android-21/arch-arm64/usr/lib -O3 -fomit-frame-pointer -Wall
make depend
make
```
   
Get header files from openssl/include (NOTE: Dereference symbolic links)   
Get libssl.a and libcrypto.a from openssl   
   
**BUILD LIBSSL (android-x86)**   
Open "Bash on Ubuntu on Windows"   
```
git clone https://github.com/openssl/openssl.git -b OpenSSL_1_0_2k --depth=1
export ANDROID_NDK_ROOT=$(pwd)/android-ndk-r12b
export PATH=$(pwd)/i686-linux-android/bin:$PATH
export CROSS_COMPILE=i686-linux-android-
cd openssl
./Configure no-shared no-asm no-zlib no-ssl2 no-ssl3 no-comp no-hw no-engine android-x86 -fPIC -DOPENSSL_PIC -DDSO_DLFCN -DHAVE_DLFCN_H -mandroid -I$ANDROID_NDK_ROOT/platforms/android-21/arch-x86/usr/include -B$ANDROID_NDK_ROOT/platforms/android-21/arch-x86/usr/lib -O3 -fomit-frame-pointer -Wall
make depend
make
```
   
Get header files from openssl/include (NOTE: Dereference symbolic links)   
Get libssl.a and libcrypto.a from openssl   
