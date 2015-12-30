FROM jetty:9-jre8

RUN { set -ex; \
	export DEBIAN_FRONTEND=noninteractive; \
	apt-get update; \
	apt-get install -y libav-tools; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*; \
}

ENV SUBSONIC_VERSION 5.3
ENV JAVA_OPTS="-Dsubsonic.defaultMusicFolder=/music/"

RUN { set -ex; \
	cd $JETTY_BASE/webapps; \
	curl -fSL \
		"https://github.com/EugeneKay/subsonic/releases/download/v$SUBSONIC_VERSION-kang/subsonic-v$SUBSONIC_VERSION-kang.war" \
		-o "ROOT.war"; \
	unzip ROOT.war; \
	rm ROOT.war; \
}

COPY start_subsonic /usr/bin/
CMD ["start_subsonic"]
