# Maintainer: Samuel Čavoj <sammko@sammserver.com>

pkgname=funky-git
pkgver=r352.8bc821c
pkgrel=1
pkgdesc='the best functional language ever'
arch=('x86_64')
url='https://github.com/faiface/funky'
license=('MIT')
makedepends=('git' 'go')
provides=('funky')
conflicts=('funky')
source=("${pkgname}::git+${url}.git" 'funkygame' 'funkycmd')
sha512sums=('SKIP'
            '8cd3fe84846803a0616eb4b25a4d45ccc4310a12df1390a206b97347063d2379c9fa956858faa4754c94e14c33a92758e59eeb215920aa0ba8bece425a13010e'
            '83446eb760c42f7309bd8163be8c086b8449a69f4e796a6aac8912c32803168d18f11bdb49069a03c161b408571115c0d2f3f81cdc26567146b50cd612a3b9c0')

pkgver() {
    cd "${pkgname}"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    export GOPATH="${srcdir}"
    mkdir -p src/github.com/faiface
    ln -rTsf "${pkgname}" src/github.com/faiface/funky
    cd src/github.com/faiface/funky
    go get -v -d ./...
}

build() {
    export GOPATH="${srcdir}"
    cd src/github.com/faiface/funky
    go install -v -gcflags "all=-trimpath=${GOPATH}/src" -asmflags "all=-trimpath=${GOPATH}/src" ./...
}

# check() {
#     export GOPATH="${srcdir}"
#     cd src/github.com/faiface/funky
#     go test ./...
# }

package() {
    install -d "${pkgdir}/usr/lib/funky"

    # binaries
    install -Dm755 bin/funkycmd "${pkgdir}/usr/lib/funky/funkycmd"
    install -Dm755 bin/funkygame "${pkgdir}/usr/lib/funky/funkygame"

    # stdlib
    cp -r "${pkgname}/stdlib" "${pkgdir}/usr/lib/funky/"

    # launcher scripts
    install -Dm755 funkycmd "${pkgdir}/usr/bin/funkycmd"
    install -Dm755 funkygame "${pkgdir}/usr/bin/funkygame"
}
