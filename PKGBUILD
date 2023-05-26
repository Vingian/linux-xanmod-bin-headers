_deb='https://github.com/xanmod/linux/releases/download/6.1.30-xanmod1/linux-headers-6.1.30-x64v3-xanmod1_6.1.30-x64v3-xanmod1-0.20230524.0edf0663_amd64.deb'
pkgname=linux-xanmod-bin-headers
pkgbase=linux-xanmod-bin
_kernel=$(echo "$_deb" | sed 's/^.*linux-headers-\([^_]*\).*$/\1/')
pkgver=$(echo "$_kernel" | sed 's/^\([0-9.]*\).*$/\1/')
pkgrel=$(echo "$_kernel" | sed 's/^.*xanmod\([0-9.]*\).*$/\1/')
pkgdesc='Linux Xanmod'
url='http://www.xanmod.org/'
arch=(x86_64)
license=(GPL2)
options=('!strip')
depends=(pahole)
source=("$_deb")
sha512sums=('SKIP')

package() {
  pkgdesc="Headers and scripts for building modules for the $pkgdesc kernel"

  mkdir -p "$srcdir/data"
  tar -xf "$srcdir/data.tar.xz" -C "$srcdir/data/"

  mkdir -p "$pkgdir/usr/lib/modules/$_kernel"
  mv "$srcdir/data/usr/src/linux-headers-$_kernel" "$pkgdir/usr/lib/modules/$_kernel/build"
  cp -f "$pkgdir/usr/lib/modules/$_kernel/build/include/config/kernel.release" "$pkgdir/usr/lib/modules/$_kernel/build/version"

  mkdir -p "$pkgdir/usr/src"
  ln -sf "../lib/modules/$_kernel/build" "$pkgdir/usr/src/${pkgbase%-*}"
  ln -sf "../lib/modules/$_kernel/build" "$pkgdir/usr/src/linux"
}
