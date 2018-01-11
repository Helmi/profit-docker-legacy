FROM microsoft/dotnet

ENV PTF_VERSION=1.3.3.208

# download package
RUN apt-get update \
  ; apt-get install -y unzip \
  ; apt-get clean \
  ; mkdir -p /var/opt/pt-feeder \
  ; wget https://github.com/mehtadone/PTFeeder/releases/download/pt-feeder-v$PTF_VERSION/pt-feeder-v$PTF_VERSION.zip -P /var/opt/pt-feeder

# unzip the app
WORKDIR /var/opt/pt-feeder
RUN unzip pt-feeder-v$PTF_VERSION.zip \
  ; rm pt-feeder-v$PTF_VERSION.zip \
  ; chmod +x pt-feeder.dll

# expose our default runtime port
EXPOSE 7071

# run it
ENTRYPOINT ["dotnet", "pt-feeder.dll"]
