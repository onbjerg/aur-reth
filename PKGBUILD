# Maintainer: Oliver Nordbjerg <hi@notbjerg.me>

pkgname=reth
pkgver=v1.9.2
_tag=v1.9.2
pkgrel=2
pkgdesc="A fast implementation of the Ethereum protocol in Rust"
arch=('x86_64')
url="https://github.com/paradigmxyz/reth"
license=('MIT' 'APACHE')
depends=()
makedepends=('git' 'cargo' 'clang')
provides=('reth')
source=("git+https://github.com/paradigmxyz/reth.git#tag=${_tag}")
sha512sums=('SKIP')

prepare() {
	cd ${pkgname}

	export RUSTUP_TOOLCHAIN=stable
	cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
	cd ${pkgname}

	export RUSTUP_TOOLCHAIN=stable
	export CARGO_TARGET_DIR=target
	export CFLAGS="${CFLAGS//-flto=auto/}"

	cargo build --bin reth --frozen --profile maxperf --features jemalloc,asm-keccak
}

package() {
	cd ${pkgname}

	install -Dm755 "target/maxperf/reth" "$pkgdir/usr/bin/reth"

	install -Dm644 "LICENSE-MIT" "$pkgdir/usr/share/licenses/${pkgname}/LICENSE-MIT"
	install -Dm644 "LICENSE-APACHE" "$pkgdir/usr/share/licenses/${pkgname}/LICENSE-APACHE"
}
