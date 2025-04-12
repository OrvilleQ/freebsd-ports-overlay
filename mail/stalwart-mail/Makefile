PORTNAME=	stalwart-mail
DISTVERSIONPREFIX=	v
DISTVERSION=	0.11.7
CATEGORIES=	mail

MAINTAINER=	orville@anislet.dev
COMMENT=	Stalwart Mail Server
WWW=		https://stalw.art/

LICENSE=		AGPLv3 SELv1
LICENSE_COMB=		multi
LICENSE_NAME_SELv1=	Stalwart Enterprise License 1.0
LICENSE_FILE_AGPLv3=	${WRKSRC}/LICENSES/AGPL-3.0-only.txt
LICENSE_FILE_SELv1=	${WRKSRC}/LICENSES/LicenseRef-SEL.txt
LICENSE_PERMS_SELv1=	pkg-mirror auto-accept

LIB_DEPENDS=	libzstd.so:archivers/zstd

USES=		cpe cargo
USE_GITHUB=	yes
GH_ACCOUNT=	stalwartlabs
GH_PROJECT=	mail-server
GH_TAGNAME=	${DISTVERSIONFULL}

CARGO_FEATURES=	--no-default-features

CARGO_INSTALL_PATH=	crates/main crates/cli

OPTIONS_DEFINE=		ENTERPRISE
OPTIONS_DEFAULT=	SQLITE POSTGRES MYSQL ROCKS ELASTIC S3 REDIS AZURE
OPTIONS_MULTI=		BACKENDS
OPTIONS_MULTI_BACKENDS=	SQLITE FOUNDATIONDB POSTGRES MYSQL ROCKS ELASTIC S3 REDIS AZURE

AZURE_DESC=		Enable Azure storage backend
BACKEND_DESC=		Database and storage backends
ELASTIC_DESC=		Enable ElasticSearch backend
ENTERPRISE_DESC=	Enable Enterprise features (require license)
FOUNDATIONDB_DESC=	Enable FoundationDB backend (not supported yet)
MYSQL_DESC=		Enable MySQL backend
POSTGRES_DESC=		Enable PostgreSQL backend
REDIS_DESC=		Enable Redis backend
ROCKS_DESC=		Enable RocksDB backend
S3_DESC=		Enable S3 storage backend
SQLITE_DESC=		Enable SQLite backend

AZURE_VARS=		CARGO_FEATURES+=azure
ELASTIC_VARS=		CARGO_FEATURES+=elastic
ENTERPRISE_VARS=	CARGO_FEATURES+=enterprise
FOUNDATIONDB_VARS=	CARGO_FEATURES+=foundationdb
MYSQL_VARS=		CARGO_FEATURES+=mysql
POSTGRES_VARS=		CARGO_FEATURES+=postgres
REDIS_VARS=		CARGO_FEATURES+=redis
ROCKS_VARS=		CARGO_FEATURES+=rocks
S3_VARS=		CARGO_FEATURES+=s3
SQLITE_VARS=		CARGO_FEATURES+=sqlite

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MROCKS}
USES+=		llvm
LIB_DEPENDS+=	librocksdb.so:databases/rocksdb
.endif

.if ${PORT_OPTIONS:MFOUNDATIONDB}
IGNORE=	FoundationDB is not currently tested.
.endif

post-install:
	${INSTALL} -m0600 ${WRKSRC}/resources/config/config.toml \
		${STAGEDIR}${PREFIX}/etc/${PORTNAME}.toml.sample

	@${MKDIR} ${STAGEDIR}/var/db/stalwart-mail
	@${MKDIR} ${STAGEDIR}/var/db/stalwart-mail/data

.include <bsd.port.mk>

