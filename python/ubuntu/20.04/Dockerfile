FROM ubuntu:20.04

# Time zone setting
RUN apt-get update && apt-get install -y tzdata
ARG TZ=UTC
ENV TZ ${TZ}

# Language setting
ARG LANG=POSIX
RUN if [[ ${LANG} =~ ^jp_JP ]]; then \
    apt-get update && apt-get install -y language-pack-ja-base language-pack-ja locales \
    && locale-gen ${LANG} \
;fi
ENV LANG ${LANG}

# build library
RUN apt update && apt install -y \
    curl \
    build-essential libbz2-dev libdb-dev \
    libreadline-dev libffi-dev libgdbm-dev liblzma-dev \
    libncursesw5-dev libsqlite3-dev libssl-dev \
    zlib1g-dev uuid-dev tk-dev

# Python build
ARG PYTHON_VERSION=3.11.0
RUN curl -OL https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tar.xz \
    && tar Jxfv Python-${PYTHON_VERSION}.tar.xz \
    && cd Python-${PYTHON_VERSION} \
    && ./configure \
    && make \
    && make install

# User setting
ARG USER_NAME=ubuntu
RUN useradd -m -s /bin/bash ${USER_NAME}
USER ${USER_NAME}
WORKDIR /home/${USER_NAME}

CMD ["/bin/bash"]
