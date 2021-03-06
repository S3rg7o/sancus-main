# Clean Ubuntu 18.04 container
FROM ubuntu:18.04
RUN apt-get update -yqq
RUN apt-get -yqq install build-essential git lsb-release sloccount sudo vim

# Non-interactive 
RUN echo "Europe/Brussels" > /etc/timezone
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yqq tzdata

# Config parameters
ARG SANCUS_SECURITY=64
ARG SANCUS_KEY=deadbeefcafebabe
WORKDIR sancus

# Build and install latest Sancus toolchain
# Install Sergio's custom Sancus core - DMA support
RUN git clone https://github.com/S3rg7o/sancus-main.git .  
RUN make install clean \
	SANCUS_SECURITY=$SANCUS_SECURITY SANCUS_KEY=$SANCUS_KEY

# Display a welcome message for interactive sessions
RUN echo '[ ! -z "$TERM" -a -r /etc/motd ] && cat /etc/motd' \
	>> /etc/bash.bashrc ; echo "\
========================================================================\n\
= Sancus development Docker container                                  =\n\
========================================================================\n\
`lsb_release -d`\n\n\
To get started, see <https://distrinet.cs.kuleuven.be/software/sancus/>,\n\
or have a look at the example programs under </sancus/sancus-examples/>.\n\
\n"\
> /etc/motd

CMD /bin/bash
