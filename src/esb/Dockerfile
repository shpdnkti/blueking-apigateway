ARG IMAGE=tencentos/tencentos3-minimal
ARG TAG=latest
FROM ${IMAGE}:${TAG}

RUN dnf -y install \
        openssl-devel \
        libffi-devel \
        glibc-devel \
        vim \
        procps-ng \
        python36 \
        python36-devel

ADD build /app
WORKDIR /app

RUN mkdir ~/.pip && printf '[global]\nindex-url = https://mirrors.tencent.com/pypi/simple/' > ~/.pip/pip.conf && \
    pip3 install --upgrade pip && \
    pip3 install -r requirements.txt

CMD ["bash", "/app/bin/start.sh"]
