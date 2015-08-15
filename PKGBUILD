# Maintainer: ying
# Contributer: ying
pkgname=crossover-games
pkgver=10.3.0
pkgrel=1
pkgdesc="Play Windows Games on Linux"
arch=('i686' 'x86_64')

makedepends=('binutils' 'tar')

if [ $CARCH = 'i686' ] ;
then

depends=('alsa-lib' 'libsm' 'libxext' 'libxrandr' 'libice' 'pygtk' 'desktop-file-utils' 'fontconfig' 'libxcursor' 'libxdamage' 'libxxf86dga' 'mesa')
optdepends=('libxcursor: coloured mouse pointer support' 
  'libxi: enables joystick and tablet support' 
  'libxinerama: enables spanning multiple screens' 
  'openssl:  support for secure Internet communication' 
  'libcups: printing support'
  'libpng: enable PNG images' 
  'libjpeg: enable JPEG images' 
  'libxxf86vm: perform gamma adjustments' 
  'hal: automatically detect CD-ROMs, DVDs, and USB keys' 
  'unzip: required to install Guild Wars, automatic installer extraction'
  ) 

else 

depends=('fontconfig' 'desktop-file-utils' 'alsa-lib' 'lib32-alsa-lib' 'lib32-fontconfig' 'lib32-libxcursor' 'libxxf86dga' 'libxrandr' 'libxdamage' 'lib32-libxdamage' 'lib32-libxxf86dga' 'mesa' 'lib32-mesa' 'lib32-glibc' 'libxcursor' 'lib32-libsm' 'lib32-libxext' 'lib32-zlib' 'lib32-gcc-libs' 'lib32-libxrandr' 'lib32-libice' 'lib32-util-linux-ng' 'lib32-e2fsprogs' 'pygtk')
optdepends=('lib32-nvidia-utils: enables 3D under nvidia cards' 
  'lib32-catalyst-utils: enables 3D under ati cards' 
  'lib32-libxcursor: coloured mouse pointer support' 
  'lib32-libxinerama: enables spanning multiple screens' 
  'lib32-openssl:  support for secure Internet communication' 
  'lib32-libcups: printing support' 
  'lib32-libxxf86vm: perform gamma adjustments' 
  'lib32-libxi: enables joystick and tablet support' 
  'lib32-libpng: enable PNG images' 
  'lib32-libjpeg: enable JPEG images' 
  'lib32-hal: automatically detect CD-ROMs, DVDs, and USB keys' 
  'unzip: required to install Guild Wars, automatic installer extraction'  
) 
fi

url="http://www.codeweavers.com"
license=('custom')
source=("http://media.codeweavers.com/pub/crossover/cxgames/demo/crossover-games-demo_${pkgver}-1_i386.deb" cxgames.conf)
install=${pkgname}.install

build() {
	cd $srcdir/
	ar -p crossover-games-demo_${pkgver}-1_i386.deb data.tar.gz | tar zxf - -C "${pkgdir}" || return 1
	rm $pkgdir/opt/cxgames/doc # remove symbolic link
	mkdir $pkgdir/opt/cxgames/doc # create real directory
	mv $pkgdir/usr/share/doc/crossover-games-demo/* $pkgdir/opt/cxgames/doc
	gzip -d $pkgdir/opt/cxgames/doc/license.txt.gz
	install -m 644 -D $pkgdir/opt/cxgames/doc/license.txt $pkgdir/usr/share/licenses/crossover-games/license
	sed s/\;\;"\"MenuRoot\" = \"\""/"MenuRoot = Windows Games/" -i $pkgdir/opt/cxgames/share/crossover/bottle_data/cxbottle.conf
	sed s/\;\;"\"MenuStrip\" = \"\""/"MenuStrip = 1/" -i $pkgdir/opt/cxgames/share/crossover/bottle_data/cxbottle.conf
	rm $pkgdir/usr -r

	# Sed for Python2
	cd $pkgdir/opt/cxgames/bin
	sed -i -e "s|#![ ]*/usr/bin/python$|#!/usr/bin/python2|" *
	sed -i -e "s|#![ ]*/usr/bin/env python$|#!/usr/bin/env python2|" *

	cd $pkgdir/opt/cxgames/lib/python
	sed -i -e "s|#![ ]*/usr/bin/python$|#!/usr/bin/python2|" *.py
	sed -i -e "s|#![ ]*/usr/bin/env python$|#!/usr/bin/env python2|" *.py

	# Fix Auto update error
	install -m 644 -D "$srcdir/cxgames.conf" "$pkgdir/opt/cxgames/etc/cxgames.conf"
}



md5sums=('e8fc9b228857fd33df154bd3664058bc'
         '0c791f407ac58356d549775d69262b73')
