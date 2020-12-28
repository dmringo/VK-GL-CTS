dEQP README
===========

This repository contains a GPU testing suite called dEQP (drawElements Quality Program).
dEQP contains tests for several graphics APIs, including OpenGL ES, EGL, and Vulkan.

Documentation
-------------



Up-to-date documentation for the dEQP is available at
[Android Open Source Project site](http://source.android.com/devices/graphics/testing.html).

The .qpa logs generated by the conformance tests may contain embedded PNG images of the results.
These can be viewed with `scripts/qpa_image_viewer.html`, by opening the file
with a web browser and following its instructions, or using the
[Cherry](https://android.googlesource.com/platform/external/cherry/+/master)
tool.

Khronos Vulkan Conformance Tests
--------------------------------

This repository includes Khronos Vulkan CTS under `external/vulkancts` directory.
For more information see [Vulkan CTS README](external/vulkancts/README.md).

Khronos OpenGL / OpenGL ES Conformance Tests
--------------------------------

This repository includes Khronos OpenGL / OpenGL ES CTS under `external/openglcts` directory.
For more information see [OpenGL / OpenGL ES CTS README](external/openglcts/README.md).

ANGLE for Android
--------------------------------

ANGLE can be built for Android by following the instructions
[here](https://chromium.googlesource.com/angle/angle.git/+/HEAD/doc/DevSetup.md#building-angle-for-android).

The resulting ANGLE shared object libraries can be linked against and embedded into `dEQP.apk` with
the `--angle-path` option.   This will cause `dEQP.apk` to use the ANGLE libraries for OpenGL ES
calls, rather than the native drivers.

An ABI must be specified and the directory structure containing the ANGLE shared objects must match
it so the build system can find the correct `*.so` files.

Assuming ANGLE shared objects are generated into `~/chromium/src/out/Release/` and `dEQP.apk` will
be generated with `--abis arm64-v8a`, issue the following commands:

	cd ~/chromium/src/out/Release/
	mkdir arm64-v8a && cd arm64-v8a
	cp ../lib*_angle.so .

The `--angle-path ~/chromium/src/out/Release/` option can then be used to link against and embed the
ANGLE shared object files.   The full command would be:

	python scripts/android/build_apk.py --sdk <path to Android SDK> --ndk <path to Android NDK> --abis arm64-v8a --angle-path ~/chromium/src/out/Release/
