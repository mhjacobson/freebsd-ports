PORTNAME=	aws-sdk-cpp
DISTVERSION=	1.9.364
CATEGORIES=	devel

MAINTAINER=	eduardo@FreeBSD.org
COMMENT=	C++ interface for Amazon Web Services (AWS)
WWW=		https://github.com/aws/aws-sdk-cpp

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

BROKEN_armv6=	fails to build: runaway process
BROKEN_armv7=	fails to build: runaway process
BROKEN_i386=	fails to build: compiler runs out of memory
BROKEN_powerpc=	fails to build: compiler runs out of memory

LIB_DEPENDS=	libaws-c-auth.so:security/aws-c-auth \
		libaws-c-cal.so:security/aws-c-cal \
		libaws-c-common.so:devel/aws-c-common \
		libaws-c-compression.so:devel/aws-c-compression \
		libaws-c-event-stream.so:devel/aws-c-event-stream \
		libaws-c-http.so:devel/aws-c-http \
		libaws-c-io.so:devel/aws-c-io \
		libaws-c-mqtt.so:devel/aws-c-mqtt \
		libaws-c-s3.so:devel/aws-c-s3 \
		libaws-c-sdkutils.so:devel/aws-c-sdkutils \
		libaws-checksums.so:devel/aws-checksums \
		libaws-crt-cpp.so:devel/aws-crt-cpp \
		libcurl.so:ftp/curl \
		libdbus-1.so:devel/dbus \
		libFLAC.so:audio/flac \
		libnghttp2.so:www/libnghttp2 \
		libogg.so:audio/libogg \
		libopus.so:audio/opus \
		libpulse.so:audio/pulseaudio \
		libs2n.so:security/s2n-tls \
		libsndfile.so:audio/libsndfile \
		libssh2.so:security/libssh2 \
		libvorbis.so:audio/libvorbis

USES=		cmake compiler:c++11-lib gettext-runtime localbase:ldflags \
		pkgconfig ssl xorg
USE_GITHUB=	yes
GH_ACCOUNT=	aws
USE_LDCONFIG=	yes
USE_XORG=	ice sm x11 xau xcb xdmcp xext xi xtst

CMAKE_ARGS+=	-DBUILD_ONLY="${BUILD_ONLY}" \
		-DCMAKE_INSTALL_LIBDIR=lib \
		-DCMAKE_PREFIX_PATH=${LOCALBASE}
CMAKE_ON=	BUILD_SHARED_LIBS
CMAKE_OFF=	BUILD_DEPS

CXXFLAGS+=	-Wno-error -Wno-c11-extensions

BUILD_ONLY?=

OPTIONS_DEFINE=	TEST
OPTIONS_SUB=	yes

TEST_CMAKE_BOOL_OFF=	ENABLE_TESTING

pre-everything::
	@${ECHO_MSG}
	@${ECHO_MSG} "You can build only the clients you need by defining the option BUILD_ONLY."
	@${ECHO_MSG}
	@${ECHO_MSG} "Example:"
	@${ECHO_MSG} "make BUILD_ONLY=\"s3;ec2;route53\""
	@${ECHO_MSG}
	@${ECHO_MSG} "For more information check the file ${WRKSRC}/Docs/CMake_Parameters.md"
	@${ECHO_MSG}
	@${ECHO_MSG} "If this option is not used, the package will be built with support for all the clients."
	@${ECHO_MSG}

post-patch:
	${REINPLACE_CMD} -e "s,/pkgconfig,/../libdata/pkgconfig,g" \
		${WRKSRC}/aws-cpp-sdk-core/CMakeLists.txt \
		${WRKSRC}/cmake/utilities.cmake
	${REINPLACE_CMD} -e 's,"-Werror",,g' \
		${WRKSRC}/cmake/compiler_settings.cmake

post-install:
	@cd ${STAGEDIR}/${LOCALBASE} && \
	${FIND} -s -d * -type f > ${TMPPLIST}

.include <bsd.port.mk>
