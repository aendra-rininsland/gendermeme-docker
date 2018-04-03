# Based off https://hub.docker.com/r/konradstrack/corenlp/~/dockerfile/

FROM openjdk:alpine

ENV CORENLP_ARCHIVE_VERSION=2018-02-27
ENV CORENLP_ARCHIVE=stanford-corenlp-full-${CORENLP_ARCHIVE_VERSION}.zip \
  CORENLP_SHA1SUM=74518f1a5849be7edf0fe844dfb49bcaed6a8b12 \
  CORENLP_PATH=/corenlp
ENV PORT=9000

RUN apk update

RUN apk add curl

RUN curl -LO http://nlp.stanford.edu/software/$CORENLP_ARCHIVE \
  && echo "$CORENLP_SHA1SUM  $CORENLP_ARCHIVE" > corenlp.sha1 \
  && sha1sum -c corenlp.sha1 \
  && unzip $CORENLP_ARCHIVE \
  && mv $(basename ../$CORENLP_ARCHIVE .zip) $CORENLP_PATH \
  && rm $CORENLP_ARCHIVE \
  && rm corenlp.sha1

RUN apk --purge -v del curl

WORKDIR $CORENLP_PATH

CMD java -mx10g -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLPServer -port $PORT -timeout 150000 -parse.maxlen 100 -annotators "tokenize,ssplit,pos,lemma,ner,parse,depparse,quote,mention,natlog,dcoref,openie"
