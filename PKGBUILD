# $Id: PKGBUILD 38937 2011-02-03 15:23:52Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: Luiz Ribeiro <luizribeiro@gmail.com>

pkgname=qc-usb-messenger
pkgver=1.8
pkgrel=15
pkgdesc="QuickCam Messenger & Communicate driver for Linux"
arch=('i686' 'x86_64')
url="http://home.mag.cx/messenger/"
license=('GPL')
depends=("linux")
makedepends=('linux-headers')
conflicts=('qc-usb')
install=$pkgname.install
source=(http://home.mag.cx/messenger/source/$pkgname-$pkgver.tar.gz
	qc-usb-messenger-kernel-2.6.33.patch
	qc-usb-messenger-kernel-2.6.36.patch
	qc-usb-messenger-kernel-2.6.37.patch)
md5sums=('58dc5652a0c91e6cc2adc682ca848964'
         'aa4bb3f2262622d16c3827a4f23400d9'
         'ac2bec633194ac3f06aa683d6ff5668e'
         '56a9f78ad1448fa870fa9ca3521fd2a7')

build() {
  _kernver=`pacman -Q linux | cut -d . -f 2 | cut -f 1 -d -`
  depends=("linux>=3.${_kernver}" "linux<3.`expr ${_kernver} + 1`")

  cd $srcdir/$pkgname-$pkgver
  patch -p1 < $srcdir/qc-usb-messenger-kernel-2.6.33.patch
  patch -p1 < $srcdir/qc-usb-messenger-kernel-2.6.36.patch
  patch -p1 < $srcdir/qc-usb-messenger-kernel-2.6.37.patch
  make all
  _kernelver=`uname -r`
  make install PREFIX=$pkgdir/usr MODULE_DIR=$pkgdir/lib/modules/${_kernelver} LINUX_DIR=/lib/modules/${_kernelver}/build
}
