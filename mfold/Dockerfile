FROM	alpine:3.12

RUN	apk add --no-cache libstdc++ bash libgfortran \
## Version lite - comment out imagemagick will not output PDF result
imagemagick \
&&	apk add --no-cache --virtual .build-deps build-base gfortran \
&&	cd /tmp \
&&	wget http://unafold.rna.albany.edu/download/mfold-3.6.tar.gz \
&&	tar xf mfold-3.6.tar.gz \
&&	cd mfold-3.6 \
&&	./configure \
&&	make \
&&	make install \
# Cleanup
&&	cd / \
&&	rm -rf /tmp/* \
&&	apk --no-cache del .build-deps \
&&	rm -rf /var/cache/apk/*

LABEL	tool=mfold version=3.6

WORKDIR	/data