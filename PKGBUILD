# Maintainer: Christoph Giesel <mail@cgiesel.de>

pkgname=wfrog-svn
_svnname=wfrog
pkgver=957
pkgrel=3
pkgdesc="Web-based customizable weather station software"
url="http://code.google.com/p/wfrog/"
license=('GPL3')
arch=('any')
options=('!strip')

depends=('python2-yaml' 'python2-cheetah' 'python-googlechart' 'python2-lxml' 'python2-pyusb' 'python2-pyserial')
makedepends=('subversion')
optdepends=(
  'pywws-git: wh1080 driver support'
)

source=("${_svnname}::svn+http://wfrog.googlecode.com/svn/trunk/"
        "wflogger.service"
        "wfrender.service")
md5sums=('SKIP'
         'fd3d069b54c5538afc9384a8989ea68c'
         '084358a4dec00954da9381ccba988642')

pkgver() {
  cd $_svnname
  svnversion | tr -d [A-z]
}

build() {
  cd $_svnname
  sed -i -e "s|#![ ]*/usr/bin/python$|#!/usr/bin/python2|" -e "s|#![ ]*/usr/bin/env python$|#!/usr/bin/env python2|" $(find . -type f)
}

package() {
  cd $_svnname
  mkdir -p $pkgdir/usr/lib/wfrog
  mkdir -p $pkgdir/usr/bin
  cp -r bin/ database/ wfcommon/ wfdriver/ wflogger/ wfrender/ $pkgdir/usr/lib/wfrog
  ln -s /usr/lib/wfrog/bin/wfrog $pkgdir/usr/bin/wfrog

  mkdir -p $pkgdir/usr/lib/systemd/system
  cp $srcdir/wflogger.service $srcdir/wfrender.service $pkgdir/usr/lib/systemd/system
}
