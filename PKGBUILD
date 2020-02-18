# Maintainer: Meishin  <lzjjht007 At gmail dot com> 

pkgname=caddy2-cloudflare
pkgver=beta.14
pkgrel=1
pkgdesc='Fast, cross-platform HTTP/2 web server with automatic HTTPS, with cloudflare plugin'
arch=('any')
license=('Apache')
url='https://github.com/caddyserver/caddy'
depends=()
provides=('caddy2')
conflicts=('caddy' 'caddy2')
makedepends=('go')
source=("main.go"
        "Caddyfile"
        "caddy.service")

sha256sums=('47192ea88eacafdf76569bf0715cc13f096d847a2d6c9e7e9495ca0794a78efe'
            'adf24a575a20ae9f503fac2348f7cfd26256f167992a1938f1a53a6d77b9b1f4'
            'c3eb327ba564b167e508b2bfa76ef459cacef09fb2e67a7f09944cb8f92e3207')

build() {
  export GOPATH="$srcdir/go"

  if [ -e $GOPATH ] then
    chmod -R a+w $GOPATH
    rm -r $GOPATH
  fi
  mkdir $GOPATH

  cd $srcdir
  go mod init caddy
  go get github.com/caddyserver/caddy/v2@v2.0.0-$pkgver
  go build
}

package() {
  mkdir -p "$pkgdir/var/lib/caddy2"
  install -D -m 0644 Caddyfile "$pkgdir/etc/caddy2/Caddyfile"
  install -D -m 0644 caddy.service "$pkgdir/usr/lib/systemd/system/caddy.service"
  install -D -m 0755 caddy "$pkgdir/usr/bin/caddy"
}
