FROM centos:centos7

# Install Python 3.7.9
RUN yum -y install wget make gcc openssl-devel bzip2-devel libffi-devel && \
    cd /tmp/ && \
    wget https://www.python.org/ftp/python/3.7.9/Python-3.7.9.tgz && \
    tar xzf Python-3.7.9.tgz && \
    cd Python-3.7.9 && \
    ./configure --enable-optimizations && \
    make altinstall && \
    ln -sfn /usr/local/bin/python3.7 /usr/bin/python3.7 && \
    ln -sfn /usr/local/bin/pip3.7 /usr/bin/pip3.7 && \
    ln -s /usr/local/bin/pip3.7 /usr/bin/pip

# Install pip requirements and upgrade pip
COPY requirements.txt /tmp/
RUN  pip install --upgrade pip && \
     pip install -r /tmp/requirements.txt

# Prepare and configure Python script
RUN     mkdir /python_api
COPY    python-api.py /python_api/

# Clean
RUN rm -rf /root/.cache/pip ; \
    rm -rf /var/cache/yum ; \
    rm -rf /tmp/Python-3.9.1.tgz ; \
    rm -rf /tmp/requirements.txt

# Run script
WORKDIR /python_api/
CMD  [ "/usr/bin/python3.7", "python-api.py" ]