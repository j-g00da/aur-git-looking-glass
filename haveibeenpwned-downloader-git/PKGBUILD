# Maintainer: Iyán Méndez Veiga <me (at) iyanmv (dot) com>
_name=haveibeenpwned-downloader
pkgname=$_name-git
pkgver=r62.6b5eec3
pkgrel=1
pkgdesc="A tool to download all Pwned Passwords hash ranges and save them offline"
arch=(x86_64)
url=https://github.com/HaveIBeenPwned/PwnedPasswordsDownloader
license=(BSD-3-Clause)
_dotnet_version=8.0
depends=(
    dotnet-runtime-$_dotnet_version
    gcc-libs
    glibc
)
makedepends=(
    dotnet-sdk-$_dotnet_version
    git
)
source=($_name::git+https://github.com/HaveIBeenPwned/PwnedPasswordsDownloader.git)
sha256sums=('SKIP')

prepare() {
    cd $_name
    export NUGET_PACKAGES="$PWD/nuget"
    export DOTNET_NOLOGO=true
    export DOTNET_CLI_TELEMETRY_OPTOUT=true
    dotnet restore \
        --locked-mode \
        --runtime linux-x64 \
        src/HaveIBeenPwned.PwnedPasswords.Downloader
}

pkgver() {
    cd $_name
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

build() {
    cd $_name
    export NUGET_PACKAGES="$PWD/nuget"
    export DOTNET_NOLOGO=true
    export DOTNET_CLI_TELEMETRY_OPTOUT=true
    dotnet publish \
        --no-restore \
        --framework net$_dotnet_version \
        --runtime linux-x64 \
        --no-self-contained \
        --configuration release \
        --output lib \
        src/HaveIBeenPwned.PwnedPasswords.Downloader
}

package() {
    cd $_name

    install -dm755 "$pkgdir"/usr/lib/$_name
    cp --archive -t "$pkgdir"/usr/lib/$_name lib/*

    install -dm755 "$pkgdir"/usr/bin
    ln -s /usr/lib/$_name/$_name "$pkgdir"/usr/bin/$_name

    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
