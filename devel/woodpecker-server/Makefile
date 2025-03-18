PORTNAME=	woodpecker-server
DISTVERSIONPREFIX=	v
DISTVERSION=	3.4.0
CATEGORIES=	devel
MASTER_SITES=	https://github.com/woodpecker-ci/woodpecker/releases/download/${DISTVERSIONFULL}/
DISTNAME=	woodpecker-src
DIST_SUBDIR=	woodpecker-ci-${DISTVERSION}

MAINTAINER=	orville@anislet.dev
COMMENT=	Woodpecker CI (Server)
WWW=		https://woodpecker-ci.org/

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		cpe go:modules,1.23
USE_RC_SUBR=	woodpecker-server

GO_TARGET=	go.woodpecker-ci.org/woodpecker/v3/cmd/server:woodpecker-server
GO_BUILDFLAGS+=	-ldflags=" \
		${STRIP} -w \
		-extldflags '-static' \
		-X go.woodpecker-ci.org/woodpecker/v3/version.Version=${DISTVERSION}"

EXTRACT_AFTER_ARGS=	-C ${WRKSRC}

USERS=		woodpecker
GROUPS=		woodpecker

pre-extract:
	@${MKDIR} ${WRKSRC}

post-install:
	${INSTALL} -m0600 ${FILESDIR}/${PORTNAME}-config.in \
		${STAGEDIR}${PREFIX}/etc/rc.conf.d/${PORTNAME}.sample

	@${MKDIR} ${STAGEDIR}/var/db/woodpecker
	@${MKDIR} ${STAGEDIR}/var/db/woodpecker/server

.include <bsd.port.mk>
