FROM	alpine:3.12 AS builder

RUN	cd /tmp \
&&	wget -qO ViennaRNA-2.4.14.tar.gz "https://www.tbi.univie.ac.at/RNA/download/sourcecode/2_4_x/ViennaRNA-2.4.14.tar.gz" \
&&	tar -xzvf ViennaRNA-2.4.14.tar.gz \
&&	cd ViennaRNA-2.4.14 \
&&	mv configure configure.ori.bak

## Compile failed at line 19258 in original configure file
## osx_arch_array=( ${enable_universal_binary} ) ==> osx_arch_array= ${enable_universal_binary}
COPY	config/configure /tmp/ViennaRNA-2.4.14

RUN	apk add --no-cache libstdc++ --update perl \
&&	apk add --no-cache --virtual .build-deps perl-dev build-base bash \
&&	cd /tmp/ViennaRNA-2.4.14 \
&&	./configure \
&&	make \
&&	make install \
## Clean up
&&	cd / \
&&	rm -rf /tmp/* \
&&	apk --no-cache del .build-deps \
&&	rm -rf /var/cache/apk/*

FROM alpine:3.12
COPY --from=builder /usr/local/bin /usr/local/bin
## RNAfold runtime dependency
RUN	apk --no-cache add libgomp \
&&	rm -rf /var/cache/apk/* 

LABEL	tool=rnafold version=2.4.14

WORKDIR	/data
