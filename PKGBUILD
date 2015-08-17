# Contributor: Kevin Whitaker <eyecreate at gmail dot com>
# Contributor: Adria Arrufat <swiftscythe at gmail dot com>
# Contributor: Logan Allen (loganfynne) <loganfynne at gmail dot com>

pkgname=sumwars-latest
pkgver=0.5.5
pkgrel=3
pkgdesc="Summoning Wars is an open source role-playing game, featuring both a single-player and a multiplayer mode for about 2 to 8 players."
arch=('i686' 'x86_64')
url="http://sumwars.org/"
license=('GPL')
makedepends=('autoconf')
depends=('ogre' 'cegui-ogre' 'physfs' 'freealut' 'enet' 'openal' 'libvorbis' 'poco')
source=(resources.cfg sumwars.sh sumwars.desktop "http://downloads.sourceforge.net/project/sumwars/0.5.5/sumwars-0.5.5-src.tgz") 
md5sums=(
         '4d1a77ea55e6497b3128911252fc66e4'
         '78b8013c47e29526d75463e18002c995'
         '6d63a38f2120fc154700317914514278'
         '52dab84e0f4e9d99b9ef92c09b3b8bb4')

build() {
  cp -f resources.cfg sumwars-0.5.5-src/resources.cfg
  cd ${srcdir}/sumwars-0.5.5-src
#   rm CMakeCache.txt
  cmake -DCMAKE_INSTALL_PREFIX=/usr
  make ||return 1
#   make install is broken
#   make DESTDIR=$pkgdir install ||return 1
  mkdir -p $pkgdir/usr/share/games/
  mkdir -p $pkgdir/usr/share/games/sumwars
  mkdir -p $pkgdir/usr/share/games/sumwars/save
  chmod 777 $pkgdir/usr/share/games/sumwars/save
  mkdir -p $pkgdir/usr/{bin,share/{applications,pixmaps}}
  install -m755 sumwars $pkgdir/usr/share/games/sumwars/sumwars||return 1
  install -m644 plugins.cfg $pkgdir/usr/share/games/sumwars/plugins.cfg ||return 1
  install -m644 ogre.cfg $pkgdir/usr/share/games/sumwars/ogre.cfg||return 1
  install -m644 resources.cfg $pkgdir/usr/share/games/sumwars/resources.cfg||return 1
  install -m644 authors.txt $pkgdir/usr/share/games/sumwars/authors.txt||return 1
  install -m644 resources/itempictures/shield.png $pkgdir/usr/share/pixmaps/sumwars.png||return 1
  install -m644 $srcdir/../sumwars.desktop $pkgdir/usr/share/applications/sumwars.desktop||return 1
  install -m755 $srcdir/../sumwars.sh $pkgdir/usr/bin/sumwars||return 1
  cp -r data $pkgdir/usr/share/games/sumwars/
  cp -r resources $pkgdir/usr/share/games/sumwars
  touch $pkgdir/usr/share/games/sumwars/CEGUI.log
  touch $pkgdir/usr/share/games/sumwars/Ogre.log
  touch $pkgdir/usr/share/games/sumwars/sumwars.log
  chmod 777 $pkgdir/usr/share/games/sumwars/*.log
}
