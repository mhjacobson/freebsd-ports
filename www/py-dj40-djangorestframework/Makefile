PORTNAME=	djangorestframework
PORTVERSION=	3.14.0
CATEGORIES=	www python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}dj40-

MAINTAINER=	kai@FreeBSD.org
COMMENT=	Django REST framework
WWW=		https://www.django-rest-framework.org/

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE.md

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}django40>=3.0:www/py-django40@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pytz>=0:devel/py-pytz@${PY_FLAVOR}

USES=		python:3.6+
USE_PYTHON=	distutils autoplist

CONFLICTS_INSTALL=	${PYTHON_PKGNAMEPREFIX}*${PORTNAME}
NO_ARCH=		yes

.include <bsd.port.mk>
