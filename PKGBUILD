pkgdesc="ROS - Standalone Python library for generating ROS message and service data structures for various languages."
url='http://www.ros.org/'

pkgname='ros-groovy-genmsg'
pkgver='0.4.17'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(
  ros-groovy-catkin
  )

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/genmsg ]; then
    cd ${srcdir}/genmsg
    git fetch origin --tags
    git reset --hard release/genmsg/${pkgver}
  else
    git clone -b release/genmsg/${pkgver} git://github.com/ros-gbp/genmsg-release.git ${srcdir}/genmsg
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/genmsg
  cmake ${srcdir}/genmsg -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
