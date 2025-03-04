PORTNAME=	woodpecker-cli
DISTVERSIONPREFIX=	v
DISTVERSION=	3.2.0
CATEGORIES=	devel
MASTER_SITES=	https://github.com/woodpecker-ci/woodpecker/releases/download/${DISTVERSIONFULL}/
DISTNAME=	woodpecker-src
DIST_SUBDIR=	woodpecker-ci-${DISTVERSION}

MAINTAINER=	orville@anislet.dev
COMMENT=	Woodpecker CI (Cli)
WWW=		https://woodpecker-ci.org/

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		cpe go:modules,1.23

GO_TARGET=	go.woodpecker-ci.org/woodpecker/v3/cmd/cli:woodpecker-cli
GO_BUILDFLAGS+=	-ldflags=" \
		${STRIP} -w \
		-extldflags '-static' \
		-X go.woodpecker-ci.org/woodpecker/v3/version.Version=${DISTVERSION}"

EXTRACT_AFTER_ARGS=	-C ${WRKSRC}

pre-extract:
	@${MKDIR} ${WRKSRC}

.include <bsd.port.mk>
