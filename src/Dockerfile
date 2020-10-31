FROM ruby:2.5-alpine3.7

# Run as root
USER root

# Create a custom user to run the container on
RUN addgroup mailcatcher \
 && adduser -u 1000 -D -S -G mailcatcher mailcatcher \
 && mkdir -p /home/mailcatcher \
 && touch /home/mailcatcher/.profile \
 && chown -R mailcatcher:mailcatcher /home/mailcatcher \
 && mkdir /data \
 && chown -R mailcatcher:mailcatcher /data

# Install mailcatcher
RUN set -xe \
 && apk add --no-cache libstdc++ sqlite-libs \
 && apk add --no-cache --virtual .build-deps build-base sqlite-dev \
 && gem install mailcatcher --no-ri --no-rdoc \
 && apk del .build-deps

# Run as node
USER mailcatcher

# Expose ports
EXPOSE 1025 1080

# The default command to execute
CMD ["mailcatcher", "--no-quit", "--foreground", "--ip=0.0.0.0"]
