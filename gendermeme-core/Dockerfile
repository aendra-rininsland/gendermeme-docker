FROM python:2-alpine

RUN apk update

RUN apk add git build-base

RUN pip install --upgrade pip

RUN pip install --no-cache-dir pycorenlp numpy

WORKDIR /project

RUN git clone https://github.com/poorna-kumar/gendermeme-core.git /project/gendermeme

RUN apk --purge -v del git build-base

CMD ["python2"]
