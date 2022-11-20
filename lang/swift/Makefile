PORTNAME=	swift
DISTVERSION=	5.8
CATEGORIES=	lang

MAINTAINER=	mhjacobson@me.com
COMMENT=	Swift programming language compiler and standard library
WWW=		https://www.swift.org/

ONLY_FOR_ARCHS=	amd64

USES=		cmake ninja python
LIB_DEPENDS=	libuuid.so:misc/e2fsprogs-libuuid

CMAKE_SOURCE_PATH=${WRKSRC}/llvm-project/llvm
CMAKE_ARGS= \
	-DCMAKE_BUILD_TYPE=Release \
	-DCMAKE_INSTALL_PREFIX=/usr/local \
	-DLLVM_ENABLE_PROJECTS=clang \
	-DLLVM_TARGETS_TO_BUILD=X86 \
	-DLLVM_EXTERNAL_PROJECTS="cmark;swift" \
	-DLLVM_EXTERNAL_CMARK_SOURCE_DIR="${WRKSRC}/cmark" \
	-DLLVM_EXTERNAL_SWIFT_SOURCE_DIR="${WRKSRC}/swift" \
	-DSWIFT_PATH_TO_SWIFT_SYNTAX_SOURCE="${WRKSRC}/swift-syntax" \
	-DSWIFT_ENABLE_DISPATCH=OFF \
	-DSWIFT_IMPLICIT_CONCURRENCY_IMPORT=OFF \
	-DSWIFT_USE_LINKER=ld \
	-DSWIFT_BUILD_STATIC_STDLIB=ON \
	-DBOOTSTRAPPING_MODE=BOOTSTRAPPING \
	-DSWIFT_ENABLE_EXPERIMENTAL_STRING_PROCESSING=ON \
	-DEXPERIMENTAL_STRING_PROCESSING_SOURCE_DIR="${WRKSRC}/swift-experimental-string-processing"

INSTALL_TARGET=	install-compiler install-autolink-driver install-stdlib install-sdk-overlay

.include <bsd.port.pre.mk>

.if ${OSVERSION} < 1301000
IGNORE=will not build on older than FreeBSD 13.1
.endif

.include <bsd.port.mk>
