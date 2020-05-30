FROM ruby:2.7.1

# Allow apt to work with https-based sources
RUN apt-get update -yqq && apt-get install -yqq --no-install-recommends \
  apt-transport-https  build-essential libpq-dev

RUN mkdir /usr/src/app
WORKDIR /usr/src/app

RUN echo "gem: --no-rdoc --no-ri" > /etc/gemrc
COPY Gemfile* /usr/src/app/
RUN bundle config set path "/gems"
RUN bundle install --jobs "$(getconf _NPROCESSORS_ONLN)" --retry 5

COPY . /usr/src/app/

ENTRYPOINT ["./docker-entrypoint.sh"]

CMD ["bin/rails", "s", "-b", "0.0.0.0"]
