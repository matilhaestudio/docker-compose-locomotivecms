#FROM rails:onbuild
#MAINTAINER sebastien.beau@akretion.com
# Replace by your uid
#RUN groupadd -g 1000 loco && adduser --uid 1000 --gid 1000 loco
#RUN mkdir /usr/src/app/tmp &&\
#    chown loco -R /usr/src/app/log /usr/src/app/tmp &&\
#    chgrp loco -R /usr/src/app/log /usr/src/app/tmp
#USER loco

#Custom 
FROM ruby:2.2.0

RUN apt-get update -qq && apt-get install -y build-essential

# for postgres
#RUN apt-get install -y libpq-dev

# for nokogiri
#RUN apt-get install -y libxml2-dev libxslt1-dev

# for capybara-webkit
#RUN apt-get install -y libqt4-webkit libqt4-dev xvfb

# for a JS runtime
RUN apt-get install -y nodejs

ENV APP_HOME /myapp
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

ADD Gemfile* $APP_HOME/

# --- Add this to your Dockerfile ---
ENV BUNDLE_GEMFILE=$APP_HOME/Gemfile \
  BUNDLE_JOBS=2 \
  BUNDLE_PATH=/bundle

#RUN bundle install

ADD . $APP_HOME

RUN gem install locomotivecms_wagon

RUN wagon auth
RUN wagon init devenv -t bootstrap
RUN bundle install
RUN bundle exec wagon generate content_type projects name:string client:string description:text image:file
RUN bundle exec wagon serve 

