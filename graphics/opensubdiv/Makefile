PORTNAME=	opensubdiv
DISTVERSIONPREFIX=	v
DISTVERSION=	3_5_0
PORTREVISION=	2
CATEGORIES?=	graphics

MAINTAINER=	FreeBSD@Shaneware.biz
COMMENT=	High performance subdivision surface libraries
WWW=		https://graphics.pixar.com/opensubdiv

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

BUILD_DEPENDS=	glfw>3.0.0:graphics/glfw

USES=		cmake gl

USE_GITHUB=	yes
GH_ACCOUNT=	PixarAnimationStudios
GH_PROJECT=	OpenSubdiv

USE_GL=		egl gl glu glew
USE_LDCONFIG=	yes
CMAKE_ON=	NO_CLEW NO_CUDA NO_DX

OPTIONS_DEFINE=		DOCS EXAMPLES OPENCL OPENMP PTEX TBB TEST TUTORIALS
OPTIONS_DEFAULT=	TBB
#OPTIONS_EXCLUDE=	EXAMPLES
OPTIONS_SUB=		yes

DOCS_CMAKE_BOOL_OFF=	NO_DOC
DOCS_BUILD_DEPENDS=	rst2html.py:textproc/py-docutils \
			doxygen>=1.8.4:devel/doxygen
DOCS_USES=		python:build
DOCS_PORTDOCS=		*

#EXAMPLES_BROKEN=	ld: error: undefined symbol: glXGetCurrentContext
#Examples cannot utilize the latest opencl headers
EXAMPLES_CMAKE_BOOL_OFF=	NO_EXAMPLES
EXAMPLES_USES=		xorg
EXAMPLES_USE=		xorg=ice,sm,x11,xcursor,xext,xi,xinerama,xrandr,xxf86vm
EXAMPLES_LIB_DEPENDS=	libglfw.so:graphics/glfw

OPENCL_CMAKE_BOOL_OFF=	NO_OPENCL
OPENCL_CFLAGS=		-pthread
OPENCL_BUILD_DEPENDS=	${LOCALBASE}/include/CL/cl.h:devel/opencl
OPENCL_LIB_DEPENDS=	libOpenCL.so:devel/ocl-icd
OPENCL_PREVENTS=	EXAMPLES

OPENMP_CMAKE_BOOL_OFF=	NO_OMP

PTEX_DESC=		ptex support
PTEX_CMAKE_BOOL_OFF=	NO_PTEX
PTEX_CMAKE_ON=		-DPTEX_LOCATION:STRING=${LOCALBASE} \
			-DPTEX_INCLUDE_DIR:STRING=${LOCALBASE}/include/ptex
PTEX_LIB_DEPENDS=	libPtex.so:graphics/ptex

TBB_DESC=		Intel threading building blocks
TBB_CMAKE_BOOL_OFF=	NO_TBB
TBB_LIB_DEPENDS=	libtbb.so:devel/onetbb

TEST_CMAKE_BOOL_OFF=	NO_REGRESSION NO_TESTS NO_GL_TESTS
TEST_LIB_DEPENDS=	libglfw.so:graphics/glfw
TEST_USES=		xorg
TEST_USE=		xorg=ice,sm,x11,xcursor,xext,xi,xinerama,xrandr,xxf86vm

# the tutorials and tests include use of deprecated parts of the library
# using clang 10 on 32 bit fails to build all tutorials and tests
# currently 12.1 still works - 11.4 and current fail
# CMake files and pkg-plist are patched to prevent failing builds

TUTORIALS_DESC=		Install tutorial programs
TUTORIALS_CMAKE_BOOL_OFF=	NO_TUTORIALS

PLIST_SUB+=		LIBVERS=${PORTVERSION}

post-patch:
	${FIND} ${WRKSRC}/tutorials -name CMakeLists.txt -exec \
		${REINPLACE_CMD} -e 's|{CMAKE_BINDIR_BASE}/tutorials|{CMAKE_INSTALL_PREFIX}/${DATADIR_REL}/tutorials|g' {} +
	${FIND} ${WRKSRC}/examples -name CMakeLists.txt -exec \
		${REINPLACE_CMD} -e 's|{CMAKE_BINDIR_BASE}|{CMAKE_INSTALL_PREFIX}/${EXAMPLESDIR_REL}|g' {} +
	${FIND} ${WRKSRC}/regression -name CMakeLists.txt -exec \
		${REINPLACE_CMD} -e 's|{CMAKE_BINDIR_BASE}|{CMAKE_INSTALL_PREFIX}/tests/${PORTNAME}|g' {} +

.include <bsd.port.mk>
