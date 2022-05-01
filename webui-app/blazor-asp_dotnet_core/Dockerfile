#// ------------------------------------------------------------------------------------------
#/// \file                  Dockerfile to distribute the simulation
#/// \author                Sreejith.Naarakathil@gmail.com
#/// \date                  27/3/2021
#// ------------------------------------------------------------------------------------------

FROM ubuntu:20.04
RUN apt-get update
RUN apt-get -qq -y install wget
RUN wget http://ftp.us.debian.org/debian/pool/main/i/icu/libicu57_57.1-6+deb9u4_amd64.deb
RUN dpkg -i libicu57_57.1-6+deb9u4_amd64.deb 
RUN rm -rf libicu57_57.1-6+deb9u4_amd64.deb

COPY bin/Release/netcoreapp3.1/linux-x64/publish /app
RUN ls -la /
RUN ls -la /app
RUN chmod u+x /app/blazor-asp_dotnet_core
WORKDIR /app

# Run the process with a non-root user
USER 1000
ENTRYPOINT ["./blazor-asp_dotnet_core"]
CMD ["--urls", "http://0.0.0.0:5000"]
