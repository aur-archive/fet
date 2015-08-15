# Maintainer: rtfreedman  (rob<d0t>til<d0t>freedman<aT>googlemail<d0t>com
# Contributor: speps <speps at aur dot archlinux dot org> 

pkgname=fet
pkgver=5.27.2
pkgrel=1
pkgdesc="Atomatically schedule the timetable of a school, high-school or university managing resources"
url="http://lalescu.ro/liviu/fet"
license=('AGPL3')

arch=('i686' 'x86_64')
depends=('qt5-base')
install="$pkgname.install"

source=("${url}/download/$pkgname-$pkgver.tar.bz2")
md5sums=('930272466db8e693acca29a96c7d7df2')

#_language=( ar ca da de el es fa fr gl he hu id it lt mk ms nl pl pt_BR ro ru si sk sq sr tr uk untranslated uz vi )
# Choose your language or leave it empty for all available languages
_language=( ) # do we really need 'untranslated' ? 

#_examples=( Algeria Argentina Belize Brazil Bulgaria Denmark Egypt Germany Greece Hong-Kong Hungary India Indonesia Iran Italy Malta Morocco Namibia Romania Saudi-Arabia South-Africa Spain Sudan United-Kingdom )
# Choose your examples based on country or leave it empty for all available examples
_examples=( )

prepare() {
  cd $pkgname-$pkgver
  # translations
  if [ ${#_language[@]} -ne 0 ]; then
	for _lang in ${_language[@]}; do
		_set_translations+="translations/fet_${_lang}.qm " 
	done
	sed "s@translations.files = translations/\*.qm@translations.files = $_set_translations@" -i fet.pro
  fi
  # examples
  if [ ${#_examples[@]} -ne 0 ]; then
	for _lang in ${_examples[@]}; do
		_set_examples+="examples/${_lang} " 
	done
	sed "s@examples.files = examples/@examples.files = $_set_examples@" -i fet.pro
  fi
}

build() {
  cd $pkgname-$pkgver
  # USE_SYSTEM_LOCALE : set your system language as default 
  qmake-qt5 "DEFINES+=USE_SYSTEM_LOCALE"
  make 
}

package() {
  cd $pkgname-$pkgver
  make install INSTALL_ROOT="$pkgdir"
}
