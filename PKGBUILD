# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Lukas Fleischer
#     <lfleischer@archlinux.org>
#   Evangelos Foutras
#     <foutrelis@archlinux.org>
#   Allan McRae
#     <allan@archlinux.org>
#   Tom Newsom
#     <Jeepster@gmx.co.uk>

if [[ ! -v "_os" ]]; then
  _os="$(
    uname \
      -o)"
fi

_etc_get() {
  local \
    _etc \
    _os
  _os="$(
    uname \
      -o)"
  _etc="etc"
  if [[ "${_os}" == "Android" ]]; then
    _etc="usr/etc"
  fi
  echo \
    "${_etc}"
}

_arch="$(
  uname \
    -m)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _compiler="clang"
  _libcompiler="llvm-libs"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
fi
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
_pkg=sudo
if [[ ! -v "_android" ]]; then
  _android="false"
  if [[ "${_os}" == "Android" ]]; then
    _android="true"
  fi
fi
if [[ ! -v "_gnu" ]]; then
  _gnu="true"
  if [[ "${_android}" == "true" ]]; then
    _gnu="false"
  fi
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_git" ]]; then
  _git="false"
  if [[ "${_gnu}" == "true" ]]; then
    _git="false"
  fi
fi
if [[ ! -v "_release" ]]; then
  _release="false"
  if [[ "${_gnu}" == "true" ]]; then
    if [[ "${_git}" == "false" ]]; then
      _release="true"
    elif [[ "${_git}" == "true" ]]; then
      _release="false"
    fi
  fi
fi
if [[ ! -v "_ns" ]]; then
  if [[ "${_android}" == "true" ]]; then
    _ns="agnosticapollo"
    _ns="themartiancompany"
  fi
  if [[ "${_release}" == "true" ]]; then
    _ns="${_pkg}"
  elif [[ "${_release}" == "false" ]]; then
    _ns="themartiancompany"
  fi
fi
if [[ ! -v "_http" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _http="https://${_git_service}.com"
  elif [[ "${_git}" == "false" ]]; then
    _http="https://${_git_service}.com"
    if [[ "${_release}" == "true" ]]; then
      _http="https://www.${_pkg}.ws"
    fi
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_release}" == "false" ]]; then
      _archive_format="tar.gz"
      if [[ "${_git_service}" == "github" ]]; then
        _archive_format="zip"
      elif [[ "${_git_service}" == "gitlab" ]]; then
        _archive_format="tar.gz"
      fi
    elif [[ "${_release}" == "true" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
pkgbase="${_pkg}"
pkgname=(
)
if [[ "${_android}" == "true" ]]; then
  pkgname+=(
    "${_pkg}-android"
  )
fi
if [[ "${_gnu}" == "true" ]]; then
  pkgname+=(
    "${_pkg}"
  )
fi
_sudover=1.9.17p2
_gnu_ver=1.9.17
_gnu_commit="8019c5760f7fcdeb3618e48860f5a0be87f49e2c"
_android_ver=1.2.0
_android_commit="50b2ec4455b63e3a117d8a1ca7025c3cc8923322"
pkgver="1000000.g${_gnu_ver}.a${_android_ver}"
pkgrel=17
_pkgdesc=(
  "Give certain users the"
  "ability to run some commands as root."
)
pkgdesc="${_pkgdesc[*]}"
arch=()
if [[ "${_gnu}" == "true" ]]; then
  arch+=(
    "aarch64"
    "arm"
    "armv6l"
    "armv7l"
    "armv8l"
    "i686"
    "mips"
    "pentium4"
    "powerpc"
    "x86_64"
  )
fi
if [[ "${_android}" == "true" ]]; then
  arch+=(
    "any"
  )
fi
_gnu_url="https://www.${_pkg}.ws/${_pkg}"
url="https://www.${_git_service}.com/${_ns}/${_pkg}"
license=(
  'custom'
)
depends=(
  "${_libc}"
  'openssl'
  'pam'
  'libldap'
  'zlib'
)
makedepends=(
  "${_compiler}"
  "tree"
)
_etc="$(
  _etc_get)"
backup=(
  "${_etc}/pam.d/${_pkg}"
  "${_etc}/${_pkg}.conf"
  "${_etc}/${_pkg}_logsrvd.conf"
  "${_etc}/${_pkg}ers"
)
if [[ ! -v "_tag_name" ]]; then
  if [[ "${_release}" == "true" ]]; then
    _tag_name="tag"
  elif [[ "${_release}" == "false" ]]; then
    _tag_name="commit"
  fi
fi
if [[ ! -v "_tag" ]]; then
  if [[ "${_release}" == "true" ]]; then
    _tag="${_sudover}"
  elif [[ "${_release}" == "false" ]]; then
    if [[ "${_gnu}" == "true" ]]; then
      _tag="${_gnu_commit}"
    fi
    if [[ "${_android}" == "true" ]]; then
      _tag="${_android_commit}"
    fi
  fi
fi
_tarname="${_pkg}-${_tag}"
if [[ "${_release}" == "true" ]]; then
  _tarname="${_pkg}-${_sudover}"
fi
_tarname_android="${_pkg}-android-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
_tarfile_android="${_tarname_android}.${_archive_format}"
_github_sum="SKIP"
source=(
)
sha256sums=(
)
if [[ "${_gnu}" == "true" ]]; then
  if [[ "${_release}" == "true" ]]; then
    _uri="${_gnu_url}/${_pkg}/dist/${_tarname}.tar.gz"
    _src="${_tarfile}::${_uri}"
    _sig_src="${_tarfile}.sig::${_uri}.sig"
    _sum='4a38a1ab3adb1199257edc2a7c4a2bd714665eb605b04368843b06dada2cfcfb'
  elif [[ "${_release}" == "false" ]]; then
    _url="${url}"
    if [[ "${_evmfs}" == "false" ]]; then
      if [[ "${_git}" == true ]]; then
        _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
        _sum="SKIP"
      elif [[ "${_git}" == false ]]; then
        _uri=""
        if [[ "${_git_service}" == "github" ]]; then
          if [[ "${_tag_name}" == "commit" ]]; then
            _uri="${_url}-gnu/archive/${_tag}.${_archive_format}"
            _sum="${_github_sum}"
          fi
        elif [[ "${_git_service}" == "gitlab" ]]; then
          if [[ "${_tag_name}" == "commit" ]]; then
            _uri="${_url}-gnu/-/archive/${_tag}/${_tag}.${_archive_format}"
          fi
        fi
        _src="${_tarfile}::${_uri}"
      fi
    fi
  fi
  source+=(
    "${_src}"
    "${_pkg}_logsrvd.service"
    "${_pkg}.pam"
  )
  sha256sums+=(
    "${_sum}"
    'bd4bc2f5d85cbe14d7e7acc5008cb4fe62c38de7d42dc6876c87bfaa273c0a6e'
    '7ec1c668c10e0f83d00e25f336872212fe04ce2c2563e1d661d34d28852f4649'
  )
  if [[ "${_release}" == "true" ]]; then
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      'SKIP'
    )
    if [[ "${_gnu}" == "true" ]]; then
      validpgpkeys=(
        # Todd C. Miller
        #   <Todd.Miller@sudo.ws
        '59D1E9CCBA2B376704FDD35BA9F4C021CEA470FB'
      )
    fi
  fi
fi
if [[ "${_android}" == "true" ]]; then
  _tarname="${_tarname_android}"
  _tarfile="${_tarfile_android}"
  _url="${url}"
  if [[ "${_evmfs}" == "false" ]]; then
    if [[ "${_git}" == true ]]; then
      _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
      _sum="SKIP"
    elif [[ "${_git}" == false ]]; then
      _uri=""
      if [[ "${_git_service}" == "github" ]]; then
        if [[ "${_tag_name}" == "commit" ]]; then
          _uri="${_url}-android/archive/${_tag}.${_archive_format}"
          _sum="${_github_sum}"
        fi
      elif [[ "${_git_service}" == "gitlab" ]]; then
        if [[ "${_tag_name}" == "commit" ]]; then
          _uri="${_url}-android/-/archive/${_tag}/${_tag}.${_archive_format}"
        fi
      fi
      _src="${_tarfile}::${_uri}"
    fi
  fi
  source+=(
    "${_src}"
  )
  sha256sums+=(
    "${_sum}"
  )
fi
if [[ "${_release}" == "true" ]]; then
  # Error 'too many levels of
  # symbolic links when extracting
  # with bsdtar, deferring
  # extraction to prepare function
  noextract=(
    "${_tarfile}"
  )
fi

prepare() {
  if [[ "${_release}" == "true" ]]; then
    tar \
      vxf \
      "${_tarfile}"
  fi
}

build() {
  local \
    _cflags=() \
    _configure_opts=()
  _cflags+=(
    # ${CFLAGS}
  )
  if [[ "${_gnu}" == "true" ]]; then
    _configure_opts+=(
      --prefix="/usr"
      --sbindir="/usr/bin"
      --libexecdir="/usr/lib"
      --with-rundir="/run/${_pkg}"
      --with-vardir="/var/db/${_pkg}"
      --with-logfac="auth"
      --enable-tmpfiles.d
      --with-pam
      --with-sssd
      --with-ldap
      --with-ldap-conf-file="/etc/openldap/ldap.conf"
      --with-env-editor
      --with-passprompt="[${_pkg}] password for %p: "
      --with-secure-path-value="/usr/local/sbin:/usr/local/bin:/usr/bin"
      --with-all-insults
    )
    if [[ "${_compiler}" == "gcc" ]]; then
      _cflags+=(
        -Wno-old-style-definition
      )
      export \
        CFLAGS="${_cflags[*]}"
    fi
    cd \
      "${_tarname}"
    ./configure \
      "${_configure_opts[@]}"
    # Prevent excessive overlinking due
    # to libtool; for details, please refer to
    # https://gitlab.archlinux.org/archlinux/packaging/packages/sudo/-/merge_requests/3.
    sed \
      -i \
      -e \
        's/ -shared / -Wl,-O1,--as-needed\0/g' \
      "libtool"
    make
  fi
  if [[ "${_android}" == "true" ]]; then
    ls
    cd \
      "${_tarname}"
    make \
      all
  fi
}

check() {
  if [[ "${_gnu}" == "true" ]]; then
    make \
      -C \
        "${_tarname}" \
      check
  fi
}

package_sudo() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
  provides=(
    "${_pkg}=${_gnu_ver}"
    "${_pkg}-android=${_android_ver}"
  )
  depends+=(
    'libcrypto.so'
    'libssl.so'
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install
  # sudo_logsrvd service file
  # (taken from sudo-logsrvd-1.9.0-1.el8.x86_64.rpm)
  install \
    -vDm644 \
    -t \
    "${pkgdir}/usr/lib/systemd/system" \
    "../${_pkg}_logsrvd.service"
  # Remove sudoers.dist; not needed since
  # pacman manages updates to sudoers
  rm \
    "${pkgdir}/etc/${_pkg}ers.dist"
  # Remove /run/sudo directory; we create it using systemd-tmpfiles
  rmdir \
    "${pkgdir}/run/${_pkg}"
  rmdir \
    "${pkgdir}/run"
  install \
    -vDm644 \
    "${srcdir}/${_pkg}.pam" \
    "${pkgdir}/etc/pam.d/${_pkg}"
  install \
    -Dm644 \
    "LICENSE.md" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_sudo-android() {
  local \
    _make_opts=()
  _make_opts+=(
  #   "SUDO_PKG__VERSION=${TERMUX_PKG_VERSION}"
  #   "SUDO_PKG__ARCH=${TERMUX_ARCH}"
  #   "TERMUX__NAME=${TERMUX__NAME}"
  #   "TERMUX__LNAME=${TERMUX__LNAME}"
  #   "TERMUX_APP__NAME=${TERMUX_APP__NAME}"
  #   "TERMUX_APP__PACKAGE_NAME=${TERMUX_APP__PACKAGE_NAME}"
  #   "TERMUX_APP__DATA_DIR=${TERMUX_APP__DATA_DIR}"
  #   "TERMUX__ROOTFS=${TERMUX__ROOTFS}"
  #   "TERMUX__HOME=${TERMUX__HOME}"
  #   "TERMUX__PREFIX=${TERMUX__PREFIX}"
  #   "TERMUX_ENV__S_ROOT=${TERMUX_ENV__S_ROOT}"
  #   "TERMUX_ENV__SS_TERMUX=${TERMUX_ENV__SS_TERMUX}"
  #   "TERMUX_ENV__S_TERMUX=${TERMUX_ENV__S_TERMUX}"
  #   "TERMUX_ENV__SS_TERMUX_APP=${TERMUX_ENV__SS_TERMUX_APP}"
  #   "TERMUX_ENV__S_TERMUX_APP=${TERMUX_ENV__S_TERMUX_APP}"
    DESTDIR="${pkgdir}"
    PREFIX="/usr"
  )
  cd \
    "${_tarname}"
  make \
    all
  tree \
    .
  make \
    "${_make_opts[@]}" \
    install
  if [[ -e "build/${_pkg}" ]]; then
    install \
      -vDm755 \
      "bin/${_pkg}" \
      "${pkgdir}/usr/bin/${_pkg}"
  fi
	install \
    -vdm755 \
    "${pkgdir}/usr/share/licenses/${pkgname}/licenses"
  install \
    -vDm644 \
    "LICENSE" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  cp \
    -rv \
    "licenses/"* \
    "${pkgdir}/usr/share/licenses/${pkgname}/licenses"
}

# vim:set ts=2 sw=2 et:
