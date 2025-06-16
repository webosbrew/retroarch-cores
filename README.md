**This hosts the cores for retroarch, compiled for webos (armv7).**

Currently based on retroarch 1.21.0. 130 cores built.

**Current build status:**

52 core(s) successfully processed:
	bluemsx dosbox snes9x2005 chimerasnes fceumm fmsx gambatte
	handy stella nestopia numero nxengine prboom quicknes snes9x2010
	tyrquake vba_next vecx mgba genesis_plus_gx bsnes_cplusplus98
	mame2003 mednafen_gba mednafen_lynx mednafen_ngp mednafen_pce_fast
	mednafen_supergrafx mednafen_vb mednafen_wswan mu gw prosystem
	81 fuse lutro tgbdual gpsp o2em opera virtualjaguar snes9x vbam
	mednafen_pcfx mednafen_psx hatari meteor bsnes2014_accuracy
	bsnes2014_balanced bsnes2014_performance bsnes_mercury_accuracy
	bsnes_mercury_balanced bsnes_mercury_performance

**Manually built:**

vitaquake2 (needs OPENGL changing to GLES in Makefile)

vice (core has in name x64 so need to check this)

a5200

atari800

bk (windows only?)
bsnes2014_performance

cannonball

desmume2015 (needed to alter platform in Makefile.libretro)

doukutsu

```
export CC_armv7_unknown_linux_gnueabi=$(SDK_PATH)$/bin/arm-webos-linux-gnueabi-gcc

# for Cargo
export CARGO_TARGET_ARMV7_UNKNOWN_LINUX_GNUEABI_LINKER=$(SDK_PATH)/arm-webos-linux-gnueabi_sdk-buildroot/bin/arm-webos-linux-gnueabi-gcc

rustup default stable
rustup target add armv7-unknown-linux-gnueabi

edit Makefile to use it:
cargo build --target=armv7-unknown-linux-gnueabi

must rename core to doukutsu_rs_libretro.so
```

ep128emu

fbalpha2012

fbalpha2012_cps1

fbalpha2012_cps2

fbalpha2012_cps3

fixgb

fixnes

freeintv

frodo

galaxy

gearboy

gearcoleco

gearsystem

genesis_plus_gx_wide

gme

gong (but was a dll)

gpsp

mame2003_midway

mame2003_plus

mame2010

```
Apply this patch and compile with _make platform=armv-cortexa9-neon-softfloat_

diff --git a/Makefile b/Makefile
index e0f8c43..49e66d8 100644
--- a/Makefile
+++ b/Makefile
@@ -465,10 +465,12 @@ else ifneq (,$(findstring armv,$(platform)))
    TARGETLIB := $(TARGET_NAME)_libretro.so
    SHARED := -shared -Wl,--no-undefined
    fpic = -fPIC
-   CC = g++
+#   CC = g++
    LDFLAGS +=  $(SHARED)
    ARM_ENABLED = 1
    X86_SH2DRC = 0
+   FORCE_DRC_C_BACKEND = 1
+   PTR64 = 0
 ifneq (,$(findstring cortexa8,$(platform)))
    CCOMFLAGS += -marm -mcpu=cortex-a8
    ASFLAGS += -mcpu=cortex-a8
```

mednafen_pce

mednafen_saturn

melonds (GLES)

mesen

mrboom

mupen64plus_next (GLES)

np2kai

oberon

parallel_n64

```
Apply this patch and compile with _make platform=webos_

diff --git a/Makefile b/Makefile
index bca3454e..fc2885de 100644
--- a/Makefile
+++ b/Makefile
@@ -60,6 +60,8 @@ else ifneq (,$(findstring rpi,$(platform)))
    override platform += unix
 else ifneq (,$(findstring odroid,$(platform)))
    override platform += unix
+else ifneq (,$(findstring webos,$(platform)))
+   override platform += unix
 endif

 # system platform
@@ -192,7 +194,17 @@ ifneq (,$(findstring unix,$(platform)))
       endif
    endif

-
+   # webOS
+   ifneq (,$(findstring webos,$(platform)))
+      GLES = 1
+      GL_LIB := -lGLESv2
+      CPUFLAGS += -DNO_ASM -DARM -D__arm__ -DARM_ASM -D__NEON_OPT -DNOSSE -DARM_FIX
+      CPUFLAGS += -marm -mfloat-abi=softfp
+      HAVE_NEON = 1
+      WITH_DYNAREC=arm
+      CPUFLAGS += -mcpu=cortex-a9 -mfpu=neon
+   endif
+
    # Classic Platforms ####################
    # Platform affix = classic_<ISA>_<µARCH>
    # Help at https://modmyclassic.com/comp
```

puae

puae2021

px68k

quasi88

race

reminiscence

remotejoy

retro8

unx

scummvm

```
Apply this patch:

diff --git a/backends/platform/libretro/scripts/configure_engines.sh b/backends/platform/libretro/scripts/configure_engines.sh
index b04e2520..4b9b1691 100755
--- a/backends/platform/libretro/scripts/configure_engines.sh
+++ b/backends/platform/libretro/scripts/configure_engines.sh
@@ -108,7 +108,7 @@ for comp in $(get_var _components); do
 done

 # Create needed engines build files
-awk -f "engines.awk" < /dev/null > /dev/null 2>&1
+awk -f "${SCUMMVM_PATH}/engines.awk" < /dev/null > /dev/null 2>&1

 mkdir -p "engines"
```

snes9x2005_plus

stella2014

vemulator

yabasanshiro

dosbox (Makefile.libretro: CXX += -std=c++14)

mednafen_ngp (thinks output is a DLL)

tgbdual (thinks its windows)

vecx (Makefile.libretro: HAS_GLES=1)

opera

mednafen_snes

bnes

2048 (win only?)

bluemsx

bnes

cap32

chailove

chimerasnes

craft

crocods

daphne

dosbox_pure

dosbox_svn

ecwolf

jumpnbump

lowresnx

mednafen_supafaust

pcem

pocketcdg

pokemini

ppsspp: (need to edit CMakeLists.txt and change USING_X11_VULKAN to OFF, edit config to use -mfloat-abi=softfp -marm -mfpu=neon -mcpu=cortex-a9 -mtune=cortex-a53, then edit ffmpeg/linux_arm.sh to build softfp binaries, rebuild those, then run ./b.sh --gles --libretro)

sameboy

sameduck

smsplus

superbroswar

swanstation

tamalibretro

theodore

thepowdertoy

tic80

tyrquake

uw8

**Compile errors with bundled GLIBC (in repo, newer GLIBC was used for these):**

AT_HWCAP2:
fbneo
neocd
picodrive
pcsx_rearmed

**Cores not building requiring more investigation:**

3dengine (insists on using opengl)
blastem
boom3 (needs GL)
bsnes_hd_beta

citra, citra_canary
```
Makefile.common:446: *** Bad architecture used with libressl: arm.  Stop.
```

citra2018 (cmake)

desmume:
```
libretro-desmume/desmume/src/frontend/libretro
(needs libpcap added to buildroot-nc4)
```
ffmpeg: needs GL

dolphin/:
Need a 64-bit compile which is feasible however there would be no graphics as graphics libs provided
by LG are 32-bit only.
```
You're building on an unsupported platform: 'armv7l' with 4-byte pointers.
  Enable generic build if you really want a JIT-less binary.
```

dolphin_launcher: (removed as pointless without dolphin)

dosbox_core:
```
checking whether we are cross compiling... configure: error: in `libretro-super/libretro-dosbox_core/libretro/deps_bin/flac_build'
configure: error: cannot run C compiled programs.
```
easyrpg
flycast
fsuae
hbmame
ishiiruka
jaxe
kronos
mame

dinothawr:
```
s16_to_float.c:(.text+0x8c): undefined reference to `convert_s16_float_asm'
```

mame2015
```
needs gcc: error: unrecognized command-line option ‘-mstructure-size-boundary=32’ removing from Makefile
then dies at arm-webos-linux-gnueabi/bin/ld: obj/libexpat.a: error adding symbols: archive has no index; run ranlib to add one
```

mame2016
mame:
both have cross compile detection issues

emux_chip8, gb, nes, sms ? no relevant Makefile

neokops
```
arm-webos-linux-gnueabi-g++.br_real: error: unrecognized command-line option ‘-mno-ms-bitfields’) and (arm-webos-linux-gnueabi/12.2.0/../../../../arm-webos-linux-gnueabi/bin/ld: cannot find -lwinmm: No such file or directory
```
openlara:
```
/arm-webos-linux-gnueabi/bin/ld: ./main.o:(.bss+0xd6c): multiple definition of `__rglgen_glGenVertexArraysOES'; ./libretro-common/glsym/glsym_es2.o:(.bss+0x22c): first defined here
collect2: error: ld returned 1 exit status
gmake: *** [Makefile:209: openlara_libretro.so] Error 1
```
parallext:
```
s16_to_float.c:(.text+0x1c0): undefined reference to `convert_s16_float_asm'
```
rustation

samecdi
```
3rdparty/genie/bin/linux/genie: 1: Syntax error: word unexpected (expecting ")")
```
snes9x2002
squirreljme
pcsx2

tempgba:
```
arm-webos-linux-gnueabi-gcc.br_real: error: unrecognized command-line option ‘-mlong32’
gmake: *** [Makefile:65: zip.o] Error 1
```

uzem:
```
arm-webos-linux-gnueabi-g++.br_real: error: unrecognized command-line option ‘-mno-ms-bitfields’
```

vaporspec

video_processor:
```
video_processor_v4l2.c:44:10: fatal error: libv4l2.h: No such file or directory
```

vitavoyager:
needs GL

x1:
```
arm-webos-linux-gnueabi/bin/ld: unrecognized option '--export-all-symbols'
```

xrick
vitaquake3 (needs GL)

**Developer note**:
To generate .index-extended use this script (for new cores only) and add to the existing .index-extended:

```
for f in *.zip ; do echo "$(stat -c '%y' $f | cut -f 1 -d ' ') $(crc32 $f) $f"; done > .index-extended
```
