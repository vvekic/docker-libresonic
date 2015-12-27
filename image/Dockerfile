FROM tomcat:8-jre8

ENV SUBSONIC_VERSION 5.3

RUN { set -ex; \
	export DEBIAN_FRONTEND=noninteractive; \
	apt-get update; \
	apt-get install -y libav-tools; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*; \
}

RUN curl -fSL \
	"https://github.com/EugeneKay/subsonic/releases/download/v$SUBSONIC_VERSION-kang/subsonic-v$SUBSONIC_VERSION-kang.war" \
	-o "webapps/subsonic.war"

COPY start_subsonic /usr/bin
CMD ["start_subsonic"]
