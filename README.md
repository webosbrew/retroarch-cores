This hosts the cores for retroarch, compiled for webos (armv7).

Currently based on retroarch 1.21.0. 130 cores built.

Current build status:

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

Manually built:

vitaquake2 (needs OPENGL changing to GLES in Makefile)
vice (core has in name x64 so need to check this)
a5200
atari800
bk (windows only?)
bsnes2014_performance
cannonball
desmume2015 (needed to alter platform in Makefile.libretro)
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
mednafen_pce
mednafen_saturn
melonds (GLES)
mesen
mrboom
mupen64plus_next (GLES)
np2kai
oberon
puae
puae2021
px68k
quasi88
race
reminiscence
remotejoy
retro8
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
dolphin_launcher
dosbox_pure
dosbox_svn
ecwolf
jumpnbump
lowresnx
mednafen_supafaust
pcem
pocketcdg
pokemini
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

Compile errors with bundled GLIBC (in repo, newer GLIBC was used for these):

AT_HWCAP2:
fbneo
neocd
picodrive
pcsx_rearmed

Cores not building requiring more investigation:

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

dolphin:
```
You're building on an unsupported platform: 'armv7l' with 4-byte pointers.
  Enable generic build if you really want a JIT-less binary.
```
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

mame2010
```
error: size ‘-3’ of array ‘your_ptr64_flag_is_wrong’ is negative
needs  -Wno-error=narrowing
then fails with arm-webos-linux-gnueabi/bin/ld: obj/libexpat.a: error adding symbols: archive has no index; run ranlib to add one
```

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
parallel_n64:
```
s16_to_float.c:(.text+0x1f8): undefined reference to `convert_s16_float_asm'
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
scummvm
snes9x2002
squirreljme
pcsx2
ppsspp (uses cmake, requires X11 libs)

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
