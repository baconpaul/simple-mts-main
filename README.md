# A Simple MTS Tuning 'Master' Plugin

This is a fully free and open source MTS Tuning 'Master' (tuning provider) plugin. Once you
build it you can load an SCL/KBM combo and it will tune other MTS-ESP compatible instruments.
For more about MTS-ESP see https://oddsound.com/

MTS-ESP uses a dynamic library to bridge between plugins. The oddsound design requires this to 
be in a specific location. On windows this must live in
`%PROGRAM_FILES%\MTS-ESP\LIBMTS.dll`, on macOS in `/Library/Application Support/MTS-ESP/libMTS.dylib`
and on Linux systems in `/usr/local/lib/libMTS.so`

You have three options to get that dynamic library.

First, if you install the MTS-ESP mini or MTS-ESP software from oddsound it will install.

You may also copy the dll, which is in a binary https://github.com/ODDSound/MTS-ESP/tree/main/libMTS

Finally, if you want to use an open source implementation of this dll, you can build or contribute to
this open source version: https://github.com/baconpaul/mts-dylib-reference. 
Note the open source version does not support IPC so will not work
in 'sandboxed' environments like some Bitwig configurations. If you would like to contribute
an IPC implementation, go ahead!