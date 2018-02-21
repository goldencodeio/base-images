FROM ubuntu:latest
RUN apt-get update && apt-get install -y \
		make \
		openssh-client \
		curl
RUN SHPT=/usr/local/bin/shipit && curl -o $SHPT https://raw.githubusercontent.com/sapegin/shipit/master/bin/shipit && chmod +x $SHPT && unset SHPT
