This hosts the cores for retroarch, compiled for webos (armv7).

Currently based on retroarch 1.17.

Current build status:

64 core(s) successfully processed:
	2048 bluemsx dosbox snes9x2005 chimerasnes fbneo fceumm fmsx
	gambatte handy stella nestopia numero nxengine prboom quicknes
	snes9x2010 tyrquake vba_next vecx mgba genesis_plus_gx
	bsnes_cplusplus98 mame2003 mednafen_gba mednafen_lynx
	mednafen_ngp mednafen_pce_fast mednafen_supergrafx mednafen_vb
	mednafen_wswan mu gw prosystem 81 fuse lutro tgbdual gpsp
	o2em opera desmume2015 picodrive virtualjaguar 3dengine
	snes9x vbam mednafen_pcfx mednafen_psx mednafen_psx_hw
	yabause hatari meteor mame2010 dinothawr bsnes2014_accuracy
	bsnes2014_balanced bsnes2014_performance bsnes_mercury_accuracy
	bsnes_mercury_balanced bsnes_mercury_performance mame pcsx_rearmed
	bnes
 
11 core(s) failed:
   desmume mame2015 mame2016 emux_chip8 emux_gb emux_nes
   emux_sms ffmpeg ppsspp testgl test

Manually built:
   mednafen_snes

TBD:

desmume:
```
pcap.h not found
```

mame2015:
```
Generating mcs96 source file...
Cannot read opcodes file src/emu/cpu/mcs96/mcs96ops.lst [invalid mode: 'rU']
gmake: *** [src/emu/cpu/cpu.mak:1041: obj/emu/cpu/mcs96/mcs96.inc] Error 1
```

mame2016:
```
gmake platform="unix" -j16 CC="arm-webos-linux-gnueabi-gcc" CXX="arm-webos-linux-gnueabi-g++" 
GCC 12.2.0 detected
makefile:876: *** Python is not available in path.  Stop.
```

emux_chip8
```
gmake platform="unix" -j16 CC="arm-webos-linux-gnueabi-gcc" CXX="arm-webos-linux-gnueabi-g++" 
gmake: *** No targets specified and no makefile found.  Stop.
```

ppspp:
```
In file included from ../Common/GPU/Vulkan/VulkanLoader.h:34,
                 from ../ext/vma/vk_mem_alloc.cpp:10:
../ext/vulkan/vulkan.h:58:10: fatal error: X11/Xlib.h: No such file or directory
   58 | #include <X11/Xlib.h>
      |          ^~~~~~~~~~~~
compilation terminated.
```
