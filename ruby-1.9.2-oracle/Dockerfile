# Starting point is ../ruby-1.9.2/Dockerfile
FROM ruby-1.9.2

# Install Action web service
# Required by a legacy application to accept web service calls
RUN cd ~ && \
    wget https://github.com/projectgenesis/actionwebservice/archive/master.zip && \
    unzip master.zip && \
    rm master.zip && \
    cd actionwebservice-master && \
    ruby setup.rb

# Install Oracle Instant Client
ENV ORACLE_CLIENT_VERSION "18.5"
RUN cd /etc/yum.repos.d && \
    wget http://yum.oracle.com/public-yum-ol6.repo && \
    wget http://yum.oracle.com/RPM-GPG-KEY-oracle-ol6 && \
    rpm --import RPM-GPG-KEY-oracle-ol6 && \
    yum install -y yum-utils && \
    yum-config-manager --enable ol6_oracle_instantclient && \
    yum install -y oracle-instantclient$ORACLE_CLIENT_VERSION-basic && \
    yum install -y oracle-instantclient$ORACLE_CLIENT_VERSION-devel && \
    yum install -y oracle-instantclient$ORACLE_CLIENT_VERSION-sqlplus && \
    yum -y clean all && \
    rm -rf /var/cache/yum && \
    echo /usr/lib/oracle/$ORACLE_CLIENT_VERSION/client64/lib > /etc/ld.so.conf.d/oracle-instantclient$ORACLE_CLIENT_VERSION.conf && \
    ldconfig
ADD tnsnames.ora /usr/lib/oracle/18.5/client64/lib/network/admin/tnsnames.ora
ENV PATH=$PATH:/usr/lib/oracle/$ORACLE_CLIENT_VERSION/client64/bin
