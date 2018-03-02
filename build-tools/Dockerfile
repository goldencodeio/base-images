FROM gitlab/dind:latest

RUN apt-get update \
	&& apt-get install -y \
		make \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["bash"]
