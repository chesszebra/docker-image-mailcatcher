FROM ruby:2.2

LABEL maintainer="developers@chesszebra.com"

RUN apt-get update && apt-get install -y build-essential sqlite3 libsqlite3-dev \
 && gem install mailcatcher -v 0.6.5 --no-ri --no-rdoc \
 && apt-get remove --purge -y build-essential libsqlite3-dev && apt-get autoclean && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Expose SMTP and the webserver port:
EXPOSE 1025
EXPOSE 1080

# The command to run
CMD ["mailcatcher", "-f", "--ip=0.0.0.0"]
