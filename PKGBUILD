pkgname=gns3-unofficial
pkgver=0.8.4RC4
pkgrel=1
pkgdesc="Graphical network simulator based on Dynamips with pemu included. (Release Candidate)"
arch=(i686 x86_64)
url="http://www.gns3.net/"
license=('GPLv2')
depends=('python2-pyqt' 'python2-sip' 'dynagen' 'inetutils' 'xdotool')
optdepends=('wireshark-gtk: to capture frames from your virtual networks'
'virtualbox-sdk>=4.1: to use virtualbox hosts'
'qemu: to run qemu hosts or emulate Cisco ASA5520 and IDS 4235/4215 Sensor'
'vde2: to emulate virtual switches')
conflicts=('pemu','gns3')
provides=('pemu')
install='gns3.install'
source=("http://downloads.sourceforge.net/gns-3/GNS3-0.8.4-RC4-src.tar.bz2"
"http://downloads.sourceforge.net/project/gns-3/Pemu/2008-03-03/pemu_2008-03-03_bin.tar.bz2")

md5sums=('0a057dc60c4c7006c4924b507369ab2e'
         '147ab04acdca5a79d6a4ab6307a1243d')

build() {
  cd ${srcdir}/GNS3-0.8.4-RC4-src
  python2 setup.py build
}

package() {
  cd ${srcdir}/GNS3-0.8.4-RC4-src
  sed -i "s#/usr/share#${pkgdir}/usr/lib#" setup.py
  sed -i "s#/usr/local/libexec#${pkgdir}/usr/local/libexec#" setup.py
  sed -i "s#/usr/local/share#${pkgdir}/usr/local/share#" setup.py
  sed -i '86s/QEMU/VBOX/' src/GNS3/Config/Defaults.py
  python2 setup.py install --prefix ${pkgdir}/usr
  gzip ./docs/man/gns3.1
  install -D -m 644 ./docs/man/gns3.1.gz ${pkgdir}/usr/share/man/man1/gns3.1.gz
  sed -i 's/#!\/usr\/bin\/env python/#!\/usr\/bin\/env python2/' \
${pkgdir}/usr/lib/gns3/qemuwrapper.py
  sed -i 's/#!\/usr\/bin\/env python/#!\/usr\/bin\/env python2/' \
${pkgdir}/usr/lib/gns3/vboxwrapper.py
  sed -i 's/#!\/usr\/bin\/env python/#!\/usr\/bin\/env python2/' \
${pkgdir}/usr/lib/gns3/vboxcontroller_4_1.py
  cd ${srcdir}/pemu_2008-03-03_bin
  mkdir -p ${pkgdir}/usr/share/GNS3/pemu
  install -D -m 755 ./pemu ${pkgdir}/usr/lib/gns3/pemu
  install -D -m 644 ./pemu.ini ${pkgdir}/usr/lib/gns3/pemu.ini
  install -D -m 755 ./ifup ${pkgdir}/usr/lib/gns3/ifup
  install -D -m 644 ./ifup.ini ${pkgdir}/usr/lib/gns3/ifup.ini
  install -D -m 644 ./README ${pkgdir}/usr/lib/gns3/README.pemu
}
