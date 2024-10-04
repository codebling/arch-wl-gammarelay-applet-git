_pkgname=wl-gammarelay-applet
pkgname=${_pkgname}-git
pkgver=x.x.x
pkgrel=1
pkgdesc="Control wl-gammarelay-rs via applet"
arch=(any)
url=https://github.com/junelva/wl-gammarelay-applet
license=(MIT)
makedepends=(cargo sed git)
conflicts=(${_pkgname})
source=(
  "git+$url.git"
)
sha256sums=(
  'SKIP'
)

pkgver() {
  cd ${srcdir}/${_pkgname}
  git describe --long --abbrev=7 | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd ${srcdir}/${_pkgname}
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd ${srcdir}/${_pkgname}
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  cargo build --frozen --release --all-features
}

package() {
  cd ${srcdir}/${_pkgname}
  install -Dm0755 -t "$pkgdir/usr/bin/" target/release/{snx-rs,snxctl,snx-rs-gui}
}