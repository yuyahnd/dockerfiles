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

# User setting
ARG USER_NAME=ubuntu
RUN useradd -m -s /bin/bash ${USER_NAME}
USER ${USER_NAME}
WORKDIR /home/${USER_NAME}

CMD ["/bin/bash"]
