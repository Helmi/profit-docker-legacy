FROM openjdk:jre-alpine

ENV JAVA_HOME=/usr/lib/jvm/default-jvm
ENV PATH /usr/local/bin:$PATH
ENV PT_VERSION=1.2.6.9

ENV FC_LANG en-US
ENV LC_CTYPE en_US.UTF-8

# install tools
RUN apk add --update nodejs wget bash python java-cacerts \
  ; npm install -g pm2 \
  ; ln -sf "${JAVA_HOME}/bin/"* "/usr/bin/"

# fix broken cacerts
RUN rm -f /usr/lib/jvm/default-jvm/jre/lib/security/cacerts \
  ; ln -s /etc/ssl/certs/java/cacerts /usr/lib/jvm/default-jvm/jre/lib/security/cacerts

RUN mkdir -p /var/opt/pt \
  ; wget https://github.com/taniman/profit-trailer/releases/download/v$PT_VERSION/ProfitTrailer.zip -P /var/opt/pt

# unzip the app
WORKDIR /var/opt/pt 
RUN unzip ProfitTrailer.zip \
  ; rm ProfitTrailer.zip \
  ; mv ProfitTrailer/* . \
  ; rm -rf ProfitTrailer/ \
  ; mkdir config \
  ; mv trading *.properties config \
  ; ln -s config/application.properties application.properties \
  ; ln -s config/configuration.properties configuration.properties \
  ; ln -s config/trading trading \
  ; chmod +x ProfitTrailer.jar

# add the application source to the image
COPY start /var/opt/pt

# tidy up
RUN rm -rf /tmp/* /var/cache/apk/*

# expose our default runtime port
EXPOSE 8081

# run it
ENTRYPOINT ["./start"]
