PORTNAME=	e2fsprogs
CATEGORIES=	sysutils
PORTVERSION=	1.46.5
PORTREVISION=	5
BUILD_DEPENDS=	e2fsprogs-core>=${PORTVERSION}:sysutils/e2fsprogs-core
RUN_DEPENDS=	${BUILD_DEPENDS}
DISTFILES=	# empty
NO_BUILD=	yes
LICENSE=	GPLv2+
USES=		cpe
CPE_VENDOR=	e2fsprogs_project

MAINTAINER=	mandree@FreeBSD.org
COMMENT=	Wrapper to install e2fsprogs into /sbin

do-install:
		${MKDIR} 				${STAGEDIR}/sbin
		${CP} -p ${LOCALBASE}/sbin/fsck_ext2fs	${STAGEDIR}/sbin
		${CP} -p ${LOCALBASE}/sbin/e2fsck	${STAGEDIR}/sbin

.include <bsd.port.mk>
