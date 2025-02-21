PORTNAME=	libpsl
PORTVERSION=	0.21.1
PORTREVISION=	6
CATEGORIES=	dns
MASTER_SITES=	https://github.com/rockdaboot/libpsl/releases/download/${PORTVERSION}/

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	C library to handle the Public Suffix List
WWW=		https://github.com/rockdaboot/libpsl

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	public_suffix_list>=0:dns/public_suffix_list

USES=		libtool localbase:ldflags pathfix pkgconfig python:build shebangfix tar:lz

CONFIGURE_ARGS=	--disable-man \
		--with-psl-file=${LOCALBASE}/share/public_suffix_list/public_suffix_list.dat \
		--with-psl-testfile=${LOCALBASE}/share/public_suffix_list/test_psl.txt
GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
USE_LDCONFIG=	yes
USE_LOCALE=	en_US.UTF-8

SHEBANG_FILES=	src/psl-make-dafsa

OPTIONS_DEFINE=	NLS
OPTIONS_SINGLE=	IDNA
OPTIONS_SINGLE_IDNA=	ICU IDN IDN2
OPTIONS_DEFAULT=IDN2
ICU_DESC=	Use devel/icu (IDNA2008 UTS\#46 library)
IDN_DESC=	Use dns/libidn (IDNA2003 library)
IDN2_DESC=	Use dns/libidn2 (IDNA2008 library)

ICU_CONFIGURE_ON=	--enable-builtin=libicu --enable-runtime=libicu
ICU_LIB_DEPENDS=	libicuuc.so:devel/icu
IDN_CONFIGURE_ON=	--enable-builtin=libidn --enable-runtime=libidn
IDN_LIB_DEPENDS=	libidn.so:dns/libidn \
			libunistring.so:devel/libunistring
IDN_USES=		iconv
IDN2_CONFIGURE_ON=	--enable-builtin=libidn2 --enable-runtime=libidn2
IDN2_LIB_DEPENDS=	libidn2.so:dns/libidn2 \
			libunistring.so:devel/libunistring
IDN2_USES=		iconv
NLS_CONFIGURE_ENABLE=	nls
NLS_USES=		gettext
NLS_USES_OFF=		gettext-tools

.include <bsd.port.mk>
