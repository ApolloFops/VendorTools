FROM ruby:3.4.7-alpine3.22

ENV SETUPDIR=/setup
WORKDIR ${SETUPDIR}
ARG GEMFILE_DIR=.
COPY $GEMFILE_DIR/Gemfile* .

# Install build dependencies
RUN set -eux; \
	apk add --no-cache --virtual build-deps \
		build-base \
		zlib-dev \
	;

# Install Bundler
RUN set -eux; gem install bundler

# Install gems from `Gemfile` via Bundler
RUN set -eux; bundler install

# Remove build dependencies
RUN set -eux; apk del --no-cache build-deps

# Clean up
WORKDIR /srv/jekyll
RUN set -eux; \
	rm -rf \
		${SETUPDIR} \
		/usr/gem/cache \
		/root/.bundle/cache \
	;

EXPOSE 4000
ENTRYPOINT ["bundler", "exec", "jekyll"]
CMD ["--version"]
