pkgname=v4l2-relayd-intel-mipi
pkgver=0.2.0
pkgrel=1
pkgdesc="v4l2-relayd-intel-mipi daemon for Intel MIPI Cam"
arch=('x86_64')
url="https://gitlab.com/vicamo/v4l2-relayd"
license=('GPL')
depends=(
	'glib2'
	'gstreamer'
	'gst-plugins-base-libs'
	'gst-plugins-good'
	'v4l2loopback-dkms'

	'gst-plugin-libcamera'
	'icamerasrc-git'
)
conflicts=('v4l2-relayd')
makedepends=('git')
source=("https://gitlab.com/vicamo/v4l2-relayd/-/archive/upstream/${pkgver}/v4l2-relayd-upstream-${pkgver}.tar.gz")
sha256sums=('0c063edf18dcc6edcdef46e695128cfc2b2d60964ea8538c7e79a2454310c53d')

build() {
	cd "$srcdir/v4l2-relayd-upstream-${pkgver}"
	./autogen.sh
	./configure --prefix=/usr --sysconfdir=/etc
	make
}

check() {
	cd "$srcdir/v4l2-relayd-upstream-${pkgver}"
	make -k check
}

package() {
	cd "$srcdir/v4l2-relayd-upstream-${pkgver}"
	make DESTDIR="$pkgdir/" install

	cp "$pkgdir/etc/default/v4l2-relayd" "$pkgdir/etc/v4l2-relayd.d/virtual-camera.conf"
	sed -i 's/FORMAT=YUY2/FORMAT=NV12/g' "$pkgdir/etc/v4l2-relayd.d/virtual-camera.conf"
	sed -i 's/VIDEOSRC="videotestsrc"/VIDEOSRC="icamerasrc"/g' "$pkgdir/etc/v4l2-relayd.d/virtual-camera.conf"

	sed -i 's/DeviceAllow=char-video4linux//g' "$pkgdir/usr/lib/systemd/system/v4l2-relayd.service"
	sed -i 's/CapabilityBoundingSet=//g' "$pkgdir/usr/lib/systemd/system/v4l2-relayd.service"
}

