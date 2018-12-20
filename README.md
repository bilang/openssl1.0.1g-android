`Compiling OpenSSL for Android`
===============================

No changes have been done for the OpenSSL source. 
Only android_configure_armeabi.sh, android_configure_armeabiv7.sh, android_configure_x86.sh files have been created.


Compiling OpenSSL for `armeabi`
-------------------------------

```
1) Edit the `android_configure_armeabi.sh` with proper NDK location.
2) Execute the above script file as `source ./android_configure_armeabi.sh` or `. ./android_cofigure_armeabi.sh`.
3) Configure by exeucting the command `./Configure android shared --prefix=`pwd`/../libs/armeabi --openssldir=openssl`
   Note: DON’T give RELATIVE address in the Configure. Give ONLY absolute address
	 Better to have the libs inside openssl folder itself.
	 `./Configure android shared --prefix=`pwd`/android/libs/armeabi --openssldir=openssl`
4) Run `make clean && make`
5) Run `make install`
6) Libs will be created in the `prefix` mentioned during `Configure`
```

Compiling OpenSSL for `armeabi-v7`
----------------------------------

```
1) Edit the `android_configure_armeabiv7.sh` with proper NDK location.
2) Execute the above script file as `source ./android_configure_armeabiv7.sh` or `. ./android_cofigure_armeabiv7.sh`.
3) Configure by executing the command `./Configure android-armv7 shared --prefix=`pwd`/../libs/armeabi-v7a --openssldir=openssl`
   Note: DON’T give RELATIVE address in the Configure. Give ONLY absolute address. (Highlighted in RED above)
	 Better to have the libs inside openssl folder itself.
	 `./Configure android-armv7 shared --prefix=`pwd`/android/libs/armeabi-v7a --openssldir=openssl`
	Rune “make clean”
4) Run `make clean && make`
5) Run `make install`
6) Libs will be created in the `prefix` mentioned during `Configure`
```

Compiling OpenSSL for `x86`
---------------------------
 
```
1) Edit the `android_configure_x86.sh` with proper NDK location.
2) Execute the above script file as `source ./android_configure_x86.sh` or `. ./android_cofigure_x86.sh`
3) Configure by executing the command `./Configure android-x86 shared --prefix=`pwd`/../libs/x86  --openssldir=openssl`.
   NOTE: DON’T give RELATIVE address in the Configure. Give ONLY absolute address. (Highlighted in RED above)
	 Better to have the libs inside openssl folder itself.
o	 `./Configure android-x86 shared --prefix=`pwd`/android/libs/x86  --openssldir=openssl`
4) Run `make clean && make`
5) Run `make install`
6) Libs will be created in the `prefix` mentioned during `Configure`

```

Errors while compiling the OpenSSL for Android
----------------------------------------------

```
1) Error1
    make[2]: Entering directory `/home/test/openssl-1.0.1g/apps'
    make[2]: Leaving directory `/home/test/openssl-1.0.1g/apps'
    make[2]: Entering directory `/home/test/openssl-1.0.1g'
    make[2]: *** No rule to make target `certs', needed by `rehash.time'.  Stop.
    make[2]: Leaving directory `/home/test/openssl-1.0.1g'
    make[1]: *** [openssl] Error 2
    make[1]: Leaving directory `/home/test/openssl-1.0.1g/apps'
    make: *** [build_apps] Error 1

   Solution:
   http://stackoverflow.com/questions/23384636/getting-error-no-rule-to-make-target-certs-needed-by-rehash-time-stop
   Temporary Solution: Do make again, without make clean.
```

由于openssl编译时没有android api宏，当编译的目标版本小于android m也就是23的时候，编译会报错，这时编译指定android的版本大于23即可，这样做会对兼容性产生什么影响尚未验证。

编译成功生成了.a文件之后，将其放入app的工程中，可能也会产生各种编译的错误，这里需要调整sdk的版本和最小兼容版本，具体能兼容到哪个版本待验证。
