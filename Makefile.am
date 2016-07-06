#
#  ZSTD compat library for OpenVPN - Makefile.am
#
#  BSD license
#
#  Redistribution and use in source and binary forms, with or without modification,
#  are permitted provided that the following conditions are met:
#
#  * Redistributions of source code must retain the above copyright notice, this
#    list of conditions and the following disclaimer.
#
#  * Redistributions in binary form must reproduce the above copyright notice, this
#    list of conditions and the following disclaimer in the documentation and/or
#    other materials provided with the distribution.
#
#  THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
#  ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
#  WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
#  DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR
#  ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
#  (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
#  LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
#  ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
#  (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
#  SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#

MAINTAINERCLEANFILES = \
	$(srcdir)/Makefile.in

AUTOMAKE_OPTIONS = subdir-objects

zstd_version_major = `sed -n '/define ZSTD_VERSION_MAJOR/s/.*[[:blank:]]\([0-9][0-9]*\).*/\1/p' < "$(srcdir)/common/zstd.h"`
zstd_version_minor = `sed -n '/define ZSTD_VERSION_MINOR/s/.*[[:blank:]]\([0-9][0-9]*\).*/\1/p' < "$(srcdir)/common/zstd.h"`
zstd_version_patch = `sed -n '/define ZSTD_VERSION_RELEASE/s/.*[[:blank:]]\([0-9][0-9]*\).*/\1/p' < "$(srcdir)/common/zstd.h"`
zstd_version = $(shell echo $(zstd_version_major).$(zstd_version_minor).$(zstd_version_patch))

noinst_LTLIBRARIES = libzstd.la

libzstd_la_CPPFLAGS = \
	-DXXH_NAMESPACE=ZSTD_ \
	-DZSTD_LEGACY_SUPPORT=0 \
	-DZSTD_VERSION=\"$(zstd_version)\" \
	-I$(srcdir)/common \
	-I$(srcdir)/compress \
	-I$(srcdir)/decompress

libzstd_la_CFLAGS = \
	-O3 \
	-std=c99 \
	-Wall -Wextra -Wcast-qual -Wcast-align -Wshadow -Wstrict-aliasing=1 \
	-Wswitch-enum -Wdeclaration-after-statement -Wstrict-prototypes -Wundef

libzstd_la_SOURCES = \
	common/entropy_common.c \
	common/xxhash.c \
	common/zstd_common.c \
	common/fse_decompress.c \
	compress/zstd_compress.c \
	compress/fse_compress.c \
	compress/huf_compress.c \
	decompress/zstd_decompress.c \
	decompress/huf_decompress.c
