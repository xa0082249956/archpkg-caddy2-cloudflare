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

sha256sums=('53f9475eb2a740c4441c028eb0b513296434d5941373fdbffd0cf0d11cbd2c9e'
            'adf24a575a20ae9f503fac2348f7cfd26256f167992a1938f1a53a6d77b9b1f4'
            'c3eb327ba564b167e508b2bfa76ef459cacef09fb2e67a7f09944cb8f92e3207')


build() {
  export GOPATH="$srcdir/go"
  pkgpath="$srcdir/$pkgname-$pkgver"

  if [ -e $GOPATH ] 
  then
    chmod -R a+w $GOPATH
    rm -r $GOPATH
  fi
  mkdir $GOPATH
  
  if [ -e $pkgpath ] 
  then
    rm -r $pkgpath
  fi
  mkdir $pkgpath

  ln -s $(pwd)/main.go $pkgpath/main.go
  cd $pkgpath

  go mod init caddy
  go get github.com/caddyserver/caddy/v2@v2.0.0-$pkgver
  go build
}

package() {
  pkgpath="$srcdir/$pkgname-$pkgver"
  mkdir -p "$pkgdir/var/lib/caddy2"
  install -D -m 0644 Caddyfile "$pkgdir/etc/caddy2/Caddyfile"
  install -D -m 0644 caddy.service "$pkgdir/usr/lib/systemd/system/caddy.service"
  cd $pkgpath
  install -D -m 0755 caddy "$pkgdir/usr/bin/caddy"
}
