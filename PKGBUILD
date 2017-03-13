pkgname=nrf51-sdk
pkgver=12.2.0
pkgrel=1

pkgdesc="Software Development Kit for the nRF51 Series and nRF52 Series"
arch=('any')
url="https://www.nordicsemi.com/eng/Products/Bluetooth-low-energy/nRF5-SDK"
license=('custom:nordicsdk', 'custom:ant', 'LGPL')

_cksum='f012efa'
_path=nRF5_SDK_${pkgver}_${_cksum}
source=("https://developer.nordicsemi.com/nRF5_SDK/nRF5_SDK_v12.x.x/${_path}.zip")
md5sums=('f51f879777921f8b4630af3151995d62')
noextract=(${_path}.zip)

options=('!strip' 'staticlibs')

prepare() {
	bsdtar -xf "${srcdir}/${_path}.zip" \
		--exclude "arm4" --exclude "arm5*" --exclude "*.msi" --exclude "*keil*" --exclude "*iar*" --exclude "*KEIL*" --exclude "*IAR*" --exclude "*windows*"
}

package() {
	install -d "${pkgdir}/opt/${pkgname}"
	cp -a ${srcdir}/* "${pkgdir}/opt/${pkgname}"

	# Fix broken permissions
	chmod -R o=g "$pkgdir/opt/$pkgname"
	find "$pkgdir/opt/$pkgname" -perm 744 -exec chmod 755 {} +

	# generate correct makefile
	cat > $pkgdir/opt/$pkgname/components/toolchain/gcc/Makefile.posix << EOF
GNU_INSTALL_ROOT := $(dirname $(dirname $(which arm-none-eabi-gcc)))
GNU_PREFIX := arm-none-eabi
EOF
}
