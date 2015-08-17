# Maintainer: Mike Krueger <info@memoryleakx.dudmail.com>
pkgname=pnmixer-xfce4-fixed
pkgver=1
pkgrel=4
pkgdesc="PNMixer is a GTK volume mixer applet. Fixed: Child Process pavucontrol becomes to a zombie process after close. Fixed: improve mouse wheel speed."
arch=('i686' 'x86_64')
license=('GPL-3')
url="https://code.google.com/p/pnmixer-xfce4/"
groups=('pnmixer')
depends=('gtk2' 'alsa-lib' 'subversion' 'pavucontrol')
makedepends=('git')
provides=('pnmixer')
conflicts=('pnmixer')

_svntrunk="http://pnmixer-xfce4.googlecode.com/svn/trunk/"
_svnmod="pnmixer"

build() {
  cd "${srcdir}/"
  msg "Connecting to $_svntrunk..."

 if [ -d ${_svnmod}/.svn ]; then
    (cd ${_svnmod} && svn up -r ${pkgver})
  else
    svn co ${_svntrunk} --config-dir ./ ${_svnmod}
  fi
  
  msg "SVN checkout done"
  msg "Starting make..."
  
  cp -r ${_svnmod} {$_svnmod-build}
  cd ${_svnmod-build}

  sh ./autogen.sh || return 1
  make || return 1
}

package(){
  cd ${srcdir}/${_svnmod-build}
  make DESTDIR=${pkgdir} install
}
