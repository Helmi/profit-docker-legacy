FROM microsoft/dotnet

ARG PTF_VERSION

# download package
RUN apt-get update \
  ; apt-get install -y unzip \
  ; apt-get clean \
  ; mkdir -p /var/opt \
  ; wget https://github.com/mehtadone/ptfeeder-beta/releases/download/pt-feeder-beta-v${PTF_VERSION}/pt-feeder-v${PTF_VERSION}.zip -P /var/opt

# unzip the app
WORKDIR /var/opt
RUN unzip pt-feeder-v${PTF_VERSION}.zip \
  ; rm pt-feeder-v${PTF_VERSION}.zip \
  ; mv pt-feeder ptf; cd ptf \
  ; rm -rf config database \
  ; chmod +x pt-feeder.dll

WORKDIR /var/opt/ptf

# run it
ENTRYPOINT ["dotnet", "pt-feeder.dll"]