# 14.04はパッチ当てないとダメでちょっとめんどい
FROM ubuntu:saucy
MAINTAINER Seiei Higa <hanachin@gmail.com>

# gen locale
RUN locale-gen ja_JP.UTF-8

# Install basic dev tools
RUN apt-get update && apt-get install -y \
    build-essential \
    wget \
    curl \
    git

# Install package for ruby
RUN apt-get install -y \
    zlib1g-dev \
    libssl-dev \
    libreadline-dev \
    libyaml-dev \
    libxml2-dev \
    libxslt-dev

# Install package for sqlite3
RUN apt-get install -y \
    sqlite3 \
    libsqlite3-dev

# Install package for postgresql
RUN apt-get install -y libpq-dev

# Install rbenv and ruby-build
RUN git clone https://github.com/sstephenson/rbenv.git /root/.rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /root/.rbenv/plugins/ruby-build
RUN ./root/.rbenv/plugins/ruby-build/install.sh
ENV PATH /root/.rbenv/bin:$PATH
RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh # or /etc/profile
RUN echo 'eval "$(rbenv init -)"' >> .bashrc

# Install multiple versions of ruby
ENV CONFIGURE_OPTS --disable-install-doc
RUN rbenv install 2.0.0-p451 /usr/local

# Install Bundler for each version of ruby
RUN echo 'gem: --no-rdoc --no-ri' >> /.gemrc
RUN bash -l -c 'rbenv global 2.0.0-p451; gem update; gem install bundler'

# Install hiki
WORKDIR /
RUN git clone https://github.com/hiki/hiki.git
WORKDIR /hiki
VOLUME ["/hiki/data"]
RUN sed -i -e "s/gem 'mysql2'//" Gemfile
RUN rbenv exec bundle install --without development test
RUN cat hikiconf.rb.sample | sed -e "s/path to data/data/" hikiconf.rb.sample > hikiconf.rb
RUN sed -i -e "s/attach'/attach.cgi'/" hiki.ru

EXPOSE 9292
CMD ["./hiki.ru"]
