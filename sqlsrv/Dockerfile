FROM millerp/docker-ubuntu-phpfpm

RUN apt-get update && apt-get install apt-transport-https

RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

RUN apt-get update && ACCEPT_EULA=Y apt-get install -y msodbcsql unixodbc unixodbc-dev wget

RUN cd /tmp && wget https://pecl.php.net/get/sqlsrv-4.0.8.tgz && wget https://pecl.php.net/get/pdo_sqlsrv-4.0.8.tgz \
    && tar -xvf sqlsrv-4.0.8.tgz && tar -xvf pdo_sqlsrv-4.0.8.tgz

RUN cd /tmp/sqlsrv-4.0.8/ && phpize && ./configure && make && make install
RUN cd /tmp/pdo_sqlsrv-4.0.8/ && phpize && ./configure && make && make install

RUN touch /usr/local/etc/php/conf.d/sqlsrv.ini && echo "extension=sqlsrv.so" >> /usr/local/etc/php/conf.d/sqlsrv.ini \
    && echo "extension=pdo_sqlsrv.so" >> /usr/local/etc/php/conf.d/sqlsrv.ini