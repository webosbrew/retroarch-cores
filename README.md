# RetroArch WebOS Cores (ARMv7)

This repository hosts RetroArch cores compiled for WebOS (armv7).  
Currently rebuilt on December 2025 with over **130 cores built**.

---

## Table of Contents
- [Built with Script](#built-with-script)
- [Built with webOS Script](#built-with-webos-script)
- [Manual Builds](#manual-builds)
- [Cores Needing Investigation](#cores-needing-investigation)
- [Cores Not supported](#cores-not-supported)
- [Developer Notes](#developer-notes)

## Built with default script

The following cores are built using the standard build script.

`./libretro-build.sh`:

52 core(s) successfully processed:
	2048 bluemsx snes9x2005 chimerasnes clownmdemu fceumm fmsx
	gambatte handy stella nestopia numero nxengine quicknes snes9x2010
	tyrquake vba_next mgba genesis_plus_gx bsnes_cplusplus98 mame2003
	mednafen_gba mednafen_lynx mednafen_ngp mednafen_pce_fast
	mednafen_supergrafx mednafen_vb mednafen_wswan mu gw prosystem
	81 fuse lutro tgbdual o2em opera virtualjaguar snes9x vbam
	mednafen_psx mednafen_snes hatari meteor bsnes2014_accuracy
	bsnes2014_balanced bsnes2014_performance bsnes_mercury_accuracy
	bsnes_mercury_balanced bsnes_mercury_performance pcsx_rearmed bnes

26 core(s) failed:
   dosbox fbneo prboom vecx gpsp desmume desmume2015 picodrive 3dengine
   scummvm mednafen_pcfx mednafen_psx_hw yabause mame2010 dinothawr
   mame2015 mame2016 mame emux_chip8 emux_gb emux_nes emux_sms ffmpeg
   ppsspp testgl test

## Built with webOS script
Built using `./libretro-build-webos.sh`:

- parallel_n64
- unx
- scummvm
- vitaquake2
- 3dengine (PR https://github.com/libretro/libretro-3dengine/pull/15)
- fbneo (PR pending to glibc/buildroot-nc4)

## Manual Builds
Some cores required manual compilation (e.g. using make, cmake etc.):

2048

BennuGD_libretro

a5200

atari800

bk

bluemsx

bnes (PR https://github.com/libretro/bsnes-libretro/pull/48)

bsnes2014_performance

bsnes_hd_beta (PR https://github.com/DerKoun/bsnes-hd/pull/141)

cannonball

cap32

chailove

chimerasnes

citra, citra_canary (PR https://github.com/libretro/citra/pull/133)

citra2018 (PR https://github.com/libretro/citra2018/pull/8)

craft (PR https://github.com/libretro/Craft/pull/42)

crocods

daphne (PR https://github.com/libretro/daphne/pull/51)

desmume: (PR https://github.com/libretro/desmume/pull/121)

```
(also needs libpcap added to buildroot-nc4)
```

desmume2015 (PR https://github.com/libretro/desmume2015/pull/143)

dinothawr (PR merged 12/12/2025)

dosbox_core (PR https://github.com/realnc/dosbox-core/pull/69)
```
make deps
make -j16
```

dosbox_pure

dosbox_svn

dosbox (PR https://github.com/libretro/dosbox-libretro/pull/148)

doukutsu-rs

```
export CC_armv7_unknown_linux_gnueabi="$SDK_PATH/bin/arm-webos-linux-gnueabi-gcc"

# for Cargo
export CARGO_TARGET_ARMV7_UNKNOWN_LINUX_GNUEABI_LINKER="$SDK_PATH/bin/arm-webos-linux-gnueabi-gcc"

rustup default stable
rustup target add armv7-unknown-linux-gnueabi

build it:
cargo build --release --target=armv7-unknown-linux-gnueabi

must rename core to doukutsu_rs_libretro.so
```

ecwolf

emux_chip8 (PR https://github.com/libretro/emux/pull/6)

ffmpeg (PR https://github.com/libretro/RetroArch/pull/18521):

```
git clone https://github.com/FFmpeg/FFmpeg.git
./configure \
          --prefix="/usr" \
          --pkg-config-flags="--static" \
          --extra-cflags="-fPIC" \
          --extra-ldflags="-static" \
          --enable-static \
          --disable-shared \
          --disable-programs \
          --disable-doc \
          --disable-debug \
          --enable-pic \
          --enable-gpl \
          --enable-nonfree \
          --disable-autodetect \
          --enable-protocol=file \
          --enable-demuxer=mov,matroska,avi,mp3,aac,ogg,wav,flac \
          --enable-decoder=mp3,aac,vorbis,flac,h264,hevc,pcm_s16le \
          --enable-swresample \
          --enable-swscale \
          --cross-prefix=arm-webos-linux-gnueabi-
          --arch=arm
          --target-os=linux
```

then make install:

```
make install DESTDIR=~/Developer/FFmpeg/workspace/ffmpeg-static
```

then compile the core (Retroarch/cores/libretro-ffmpeg)
```
make \
    STATIC_LINK_FFMPEG=1 \
    FFMPEG_DIR="~/Developer/FFmpeg/workspace/ffmpeg-static" \
    FFMPEG_CFLAGS="-I~/Developer/FFmpeg/workspace/ffmpeg-static/include" \
    FFMPEG_LDFLAGS="$(pkg-config --static --libs libavcodec libavformat libavutil libswresample libswscale)"
```

flycast (PR https://github.com/flyinghead/flycast/pull/2167)

ep128emu_core

fbalpha2012

fbalpha2012_cps1

fbalpha2012_cps2

fbalpha2012_cps3

fixgb

fixnes

freeintv

frodo

galaxy

gb, nes, sms:

```
make -f Makefile.webos MACHINE=gb
make -f Makefile.webos MACHINE=nes
make -f Makefile.webos MACHINE=sms
```

gearboy

gearcoleco

gearsystem

genesis_plus_gx_wide

gme (PR https://github.com/libretro/libretro-gme/pull/38)

gong

gpsp (PR https://github.com/libretro/gpsp/pull/278)

holani:
```
export CARGO_TARGET_ARMV7_UNKNOWN_LINUX_GNUEABI_LINKER="$SDK_PATH/bin/arm-webos-linux-gnueabi-gcc"

cargo build --release --target=armv7-unknown-linux-gnueabi
```

jaxe

jumpnbump

lowresnx

mame (PR submitted https://github.com/libretro/mame/pull/543)

mame2003_midway (needs https://github.com/libretro/mame2003_midway/pull/13 merged)

mame2003_plus

mame2010 (PR https://github.com/libretro/mame2010-libretro/pull/166)

mame2015 (PR submitted, plus waiting on https://github.com/libretro/mame2015-libretro/pull/98)

mame2016 (PR https://github.com/libretro/mame2016-libretro/pull/65)

mednafen_psx_hw (PR https://github.com/libretro/beetle-psx-libretro/pull/937)

mednafen_saturn

mednafen_snes

mednafen_supafaust

mednafen_ngp

melonds (PR https://github.com/libretro/melonDS/pull/207)

mesen

mrboom

mupen64plus_next (PR - https://github.com/libretro/mupen64plus-libretro-nx/pull/609)

neocd (PRs https://github.com/openlgtv/buildroot-nc4/pull/62 and https://github.com/libretro/neocd_libretro/pull/97)

np2kai (PR - https://github.com/libretro/NP2kai/pull/63)

oberon

opera

parallext (PR https://github.com/libretro/paraLLeXT/pull/5)

pcsx_rearmed (PR https://github.com/openlgtv/buildroot-nc4/pull/62)

picodrive (PRs https://github.com/openlgtv/buildroot-nc4/pull/62 and https://github.com/libretro/picodrive/pull/259)

pocketcdg

pokemini

ppsspp: (PR https://github.com/hrydgard/ppsspp/pull/21071 and https://github.com/hrydgard/ppsspp-ffmpeg/pull/77)

prboom (PR https://github.com/libretro/libretro-prboom/pull/199)

sameboy

sameduck

smsplus

superbroswar (https://github.com/libretro/superbroswar-libretro/issues/14)

swanstation

puae

puae2021

px68k

quasi88

race

reminiscence

remotejoy

retro8

rustation (https://gitlab.com/flio/rustation-ng/)

```
cargo build --release --target=armv7-unknown-linux-gnueabi
```

scummvm

snes9x2002

snes9x2005_plus

stella2014

squirreljme

```
add to nanocoat/CMakeLists.txt:
target_link_libraries(SquirrelJME PRIVATE Threads::Threads)
```

tamalibretro

tgbdual

theodore

thepowdertoy

tic80

tyrquake

vemulator

vice

yabause (PR https://github.com/libretro/yabause/pull/317)

yabasanshiro (PR merged - https://github.com/libretro/yabause/pull/316)

vecx (PR https://github.com/libretro/libretro-vecx/pull/64)

uw8

uzem

vaporspec

xrick (PR https://github.com/libretro/xrick-libretro/pull/29)

x1

## Cores Needing Investigation

easyrpg (needs inih)

```
cmake .. -DPLAYER_TARGET_PLATFORM=libretro -DBUILD_SHARED_LIBS=ON -DPLAYER_BUILD_LIBLCF=ON
```

fsuae (GCC 14 build is broken)

hbmame (needs a core rebase as broken cross compilation)

openlara:
```
/arm-webos-linux-gnueabi/bin/ld: ./main.o:(.bss+0xd6c): multiple definition of `__rglgen_glGenVertexArraysOES'; ./libretro-common/glsym/glsym_es2.o:(.bss+0x22c): first defined here
collect2: error: ld returned 1 exit status
gmake: *** [Makefile:209: openlara_libretro.so] Error 1
```

samecdi (also probably due to GCC 14 fixes needed)
```
3rdparty/genie/bin/linux/genie: 1: Syntax error: word unexpected (expecting ")")
```

## Cores Not Supported

blastem (this is x86 ONLY at present)

boom3 (does not support GLES)

dolphin/:
Need a 64-bit compile which is feasible however there would be no graphics as graphics libs provided
by LG are 32-bit only.
```
You're building on an unsupported platform: 'armv7l' with 4-byte pointers.
  Enable generic build if you really want a JIT-less binary.
```

dolphin_launcher: (removed as launches standalone dolphin which is not currently supported)

ishiiruka (dolphin fork, not planned)

kronos (does not support GLES)

pcsx2 (no 32-bit ARM JIT)

tempgba (archived, no longer developed, so use gpsp instead):
```
arm-webos-linux-gnueabi-gcc.br_real: error: unrecognized command-line option ‘-mlong32’
gmake: *** [Makefile:65: zip.o] Error 1
```

pcem (x86/64 only?)

video_processor:
```
video_processor_v4l2.c:44:10: fatal error: libv4l2.h: No such file or directory
```

vitaquake3 (does not support GLES)

vitavoyager:
does not support GLES

## Developer Notes

To generate .index-extended use this script (for new cores only) and add to the existing .index-extended:

```
arm-webos-linux-gnueabi-strip file_to_strip
zip archive_name.zip file_to_compress
for f in *.zip ; do echo "$(stat -c '%y' $f | cut -f 1 -d ' ') $(crc32 $f) $f"; done > .index-extended
```
