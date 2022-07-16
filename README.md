# x64 D2BS SpiderMonkey Builds

x64 builds of the very old SpiderMonkey version [D2BS](https://github.com/noah-/d2bs) uses.

The Mercurial revision of these SpiderMonkey builds is [`61f7ebb9f3d903556516bd6cbe8b84ae14c0fa33`](https://hg.mozilla.org/mozilla-central/file/61f7ebb9f3d903556516bd6cbe8b84ae14c0fa33). You can compare this version of [jsapi.h in mozilla-central](https://hg.mozilla.org/mozilla-central/file/61f7ebb9f3d903556516bd6cbe8b84ae14c0fa33/js/src/jsapi.h) vs the version of [jsapi.h in D2BS](https://github.com/noah-/d2bs/blob/master/dependencies/include/jsapi.h) and see they are the same.

## Repo Structure
There are 3 x64 builds in this repo, seperated into subdirectories under `x64`:

1. Release
2. DebugOptimized
3. Debug

Debug will be slower than DebugOptimized so use it only if you run into debugging issues with DebugOptimized.

This repo includes only dynamic libraries. This version of SpiderMonkey required building with VS2012, so VS2012 must be used to compile with the produced static libraries, which is why they are excluded - nobody wants to use VS2012!

## How to Use

1. Choose from the Release, DebugOptimized, or Debug builds in this repo
1. (Optional) Add or copy the `include` directory to to the include path, or you can rely on the header files already present in D2BS (they are the same versions as in this repo)
1. Add the `mozjs.lib` dynamic library
1. Set the `JS_USE_JSID_STRUCT_TYPES` preprocessor macro for DebugOptimized or Debug builds to avoid linker errors
1. `LoadLibrary` or otherwise load `mozjs.dll` into the process before using any SpiderMonkey features

## FAQ
**Q: Why is there an `include` folder per build instead of one in common?**

A: The files in each build's `include` folder are identical except for `js-config.h`, which sets `JS_GC_ZEAL` for DebugOptimized and Debug builds. Note that the SpiderMonkey headers included in D2BS are the debug headers, as its [`js-config.h` sets `JS_GC_ZEAL`](https://github.com/noah-/d2bs/blob/master/dependencies/include/js-config.h#L23) even in release mode.