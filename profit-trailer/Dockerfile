FROM openjdk:8-jre-alpine

ARG PT_VERSION

ENV PT_FILENAME=ProfitTrailer-${PT_VERSION}.zip

ENV JAVA_HOME=/usr/lib/jvm/default-jvm
ENV PATH /usr/local/bin:$PATH
ENV FC_LANG en-US
ENV LC_CTYPE en_US.UTF-8

# install tools
RUN apk add --update wget bash java-cacerts \
  ; ln -sf "${JAVA_HOME}/bin/"* "/usr/bin/"

# fix broken cacerts
RUN rm -f /usr/lib/jvm/default-jvm/jre/lib/security/cacerts \
  ; ln -s /etc/ssl/certs/java/cacerts /usr/lib/jvm/default-jvm/jre/lib/security/cacerts

RUN mkdir -p /var/opt/pt 

WORKDIR /var/opt/pt 

RUN wget https://github.com/taniman/profit-trailer/releases/download/${PT_VERSION}/${PT_FILENAME}

# unzip the app
RUN unzip ${PT_FILENAME} -j \
  ; rm ${PT_FILENAME} \
  ; rm application.properties \
#  ; mkdir config \
#  ; ls -la config/ \
  ; ln -s ./config/application.properties . \
  ; chmod +x ProfitTrailer.jar

# add the application source to the image
COPY start /var/opt/pt
RUN chmod +x /var/opt/pt/start

# tidy up
RUN rm -rf /tmp/* /var/cache/apk/*

# expose our default runtime port
EXPOSE 8081

# run it
ENTRYPOINT ["/var/opt/pt/start"]