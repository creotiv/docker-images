From python:3.7.2-alpine3.9

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /usr/src/app/

RUN apk update \ 
    && apk add python3-dev gcc linux-headers libc-dev libffi-dev openssl-dev build-base \
    && pip install --no-cache-dir aiofiles==0.4.0 asn1crypto==0.24.0 certifi==2019.3.9 cffi==1.12.3 chardet==3.0.4 cryptography==2.6.1 greenlet==0.4.15 httptools==0.0.13 idna==2.8 multidict==4.5.2 pycparser==2.19 PyJWT==1.7.1 requests==2.21.0 sanic==19.3.1 six==1.12.0 ujson==1.35 urllib3==1.24.3 uvloop==0.12.2 websockets==6.0
    && apk del python3-dev gcc linux-headers libc-dev libffi-dev openssl-dev

