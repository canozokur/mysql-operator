# Copyright (c) 2021, Oracle and/or its affiliates.
#
# Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
#

FROM oraclelinux:8 AS pip-stage

# Most of this process is taken from:
# https://docs.oracle.com/en/database/oracle/machine-learning/oml4py/1/mlpug/build-and-install-python-linux-premises-databases.html
RUN dnf install -y gcc git tar perl-Env libffi-devel \
                   openssl openssl-devel tk-devel xz-devel \
                   zlib-devel bzip2-devel readline-devel \
                   libuuid-devel ncurses-devel make
ADD https://www.python.org/ftp/python/3.9.5/Python-3.9.5.tgz /Python-3.9.5.tgz
RUN mkdir -p /python && cd /python && tar xzf /Python-3.9.5.tgz --strip-components=1 -C /python \
    && ./configure --enable-shared --prefix=/python \
    && make clean && make && make altinstall

RUN ln -s /python/bin/python3.9 /python/bin/python3 && ln -s /python/bin/pip3.9 /python/bin/pip3

ENV PATH=/python/bin:$PATH
ENV LD_LIBRARY_PATH=/python/lib

COPY requirements.txt .

RUN pip3 install --target=/tmp/site-packages -r requirements.txt

FROM oraclelinux:8-slim

COPY --from=pip-stage /tmp/site-packages /usr/lib/mysqlsh/python-packages
