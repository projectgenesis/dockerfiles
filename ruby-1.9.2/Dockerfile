FROM centos:6

ENV GEMS_VERSION "1.8.30"
ENV BUNDLER_VERSION "1.17.3"
ENV RAKE_VERSION "0.9.6"

# CentOS packages for ruby build
RUN yum install -y \
  git svn \
  tar vim wget \
  gcc \
  bzip2 \
  libyaml-devel \
  libffi-devel \
  readline-devel \
  gdbm-devel \
  ncurses-devel \
  make patch autoconf bison \
  hostname nmap-ncat \
  zlib-devel \
  openssl-devel \
  unzip \
  ssh \
  libxml2-devel libxslt-devel \
  postgresql-devel \
  sqlite-devel; \
  yum -y clean all && \
  rm -rf /var/cache/yum

# Download ruby and build from source, update system gems.
RUN cd ~ && \
    git clone https://github.com/rbenv/ruby-build.git && \
    ./ruby-build/install.sh && \
    curl -sSL https://gist.githubusercontent.com/fernandoaleman/e00009e72467d24e045a/raw/a535eb139f15197772d8a56adb96712b7dfd556a/rbenv-openssl.patch -o openssl.patch && \
    cat openssl.patch | ruby-build 1.9.2-p330 /usr/local --patch && \
    export PATH="/usr/local/bin:$PATH" && \
    gem update --system $GEMS_VERSION && \
    gem install bundler -v $BUNDLER_VERSION && \
    gem install rake -v $RAKE_VERSION && \
    gem cleanup
