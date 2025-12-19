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

bnes

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

desmume2015 (PR https://github.com/libretro/desmume2015/pull/143)

dinothawr (PR merged 12/12/2025)

dosbox_pure

dosbox_svn

dosbox (PR https://github.com/libretro/dosbox-libretro/pull/148)

doukutsu-rs

```
export CC_armv7_unknown_linux_gnueabi="$SDK_PATH/bin/arm-webos-linux-gnueabi-gcc"

# for Cargo
export CARGO_TARGET_ARMV7_UNKNOWN_LINUX_GNUEABI_LINKER="$SDK_PATH/arm-webos-linux-gnueabi_sdk-buildroot/bin/arm-webos-linux-gnueabi-gcc"

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

gearboy

gearcoleco

gearsystem

genesis_plus_gx_wide

gme (PR https://github.com/libretro/libretro-gme/pull/38)

gong

gpsp (PR https://github.com/libretro/gpsp/pull/278)

jaxe

jumpnbump

lowresnx

mame2003_midway (needs https://github.com/libretro/mame2003_midway/pull/13 merged)

mame2003_plus

mame2010 (PR https://github.com/libretro/mame2010-libretro/pull/166)

mednafen_psx_hw (PR https://github.com/libretro/beetle-psx-libretro/pull/937)

mednafen_saturn

melonds (PR https://github.com/libretro/melonDS/pull/207)

mame2015 (PR submitted, plus waiting on https://github.com/libretro/mame2015-libretro/pull/98)

mame2016 (PR https://github.com/libretro/mame2016-libretro/pull/65)

mednafen_snes

mednafen_supafaust

mednafen_ngp

mesen

mrboom

mupen64plus_next (PR - https://github.com/libretro/mupen64plus-libretro-nx/pull/609)

neocd (PRs https://github.com/openlgtv/buildroot-nc4/pull/62 and https://github.com/libretro/neocd_libretro/pull/97)

np2kai (PR - https://github.com/libretro/NP2kai/pull/63)

oberon

opera

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

scummvm

snes9x2005_plus

stella2014

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

xrick (PR https://github.com/libretro/xrick-libretro/pull/29)

## Cores Needing Investigation

desmume: (PR https://github.com/libretro/desmume/pull/121)

```
(also needs libpcap added to buildroot-nc4)
```

dosbox_core:
```
checking whether we are cross compiling... configure: error: in `libretro-super/libretro-dosbox_core/libretro/deps_bin/flac_build'
configure: error: cannot run C compiled programs.
```
easyrpg - needs liblcf?

fsuae (requires glib adding to buildroot-nc4?)

hbmame (broken, old core needs some TLC)

holani:
```
error: linking with `cc` failed: exit status: 1
  |
  = note:  "cc" "-Wl,--version-script=/tmp/rustcylV6Sl/list" "-Wl,--no-undefined-version" "/tmp/rustcylV6Sl/symbols.o" "<49 object files omitted>" "-Wl,--as-needed" "-Wl,-Bstatic" "<sysroot>/lib/rustlib/armv7-unknown-linux-gnueabi/lib/{libcompiler_builtins-*}.rlib" "-Wl,-Bdynamic" "-lgcc_s" "-lutil" "-lrt" "-lpthread" "-lm" "-ldl" "-lc" "-L" "/tmp/rustcylV6Sl/raw-dylibs" "-Wl,--eh-frame-hdr" "-Wl,-z,noexecstack" "-L" "<sysroot>/lib/rustlib/armv7-unknown-linux-gnueabi/lib" "-o" "/home/xx/Developer/libretro-super/libretro-holani/target/armv7-unknown-linux-gnueabi/release/deps/libholani.so" "-Wl,--gc-sections" "-shared" "-Wl,-z,relro,-z,now" "-Wl,-O1" "-Wl,--strip-debug" "-nodefaultlibs"
  = note: some arguments are omitted. use `--verbose` to show all linker arguments
  = note: /usr/bin/ld: /home/xx/Developer/libretro-super/libretro-holani/target/armv7-unknown-linux-gnueabi/release/deps/holani.7kdhjmn7okn82er0zxbk2way8.rcgu.o: relocations in generic ELF (EM: 40)
```

mame (PR submitted https://github.com/libretro/mame/pull/543) - but fails linking with:

```
ld: BFD (GNU Binutils) 2.43.1 assertion fail elf32-arm.c:9889
```

gb, nes, sms ? no relevant Makefile

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

x1:
```
arm-webos-linux-gnueabi/bin/ld: unrecognized option '--export-all-symbols'
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

pcem (x86/64 only?)

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
