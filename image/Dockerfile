FROM pikado/alpine-jetty

ENV SUBSONIC_VERSION 6.0.1

RUN { set -ex; \
	mkdir -p $JETTY_HOME/webapps/ROOT; \
	cd $JETTY_HOME/webapps/ROOT; \
	curl -fSL \
		"https://github.com/Libresonic/libresonic/releases/download/v$SUBSONIC_VERSION/libresonic-v$SUBSONIC_VERSION.war" \
		-o "libresonic.zip"; \
	unzip libresonic.zip; \
	rm libresonic.zip; \
	chown jetty:jetty -R .; \
	cd WEB-INF/lib; \
	rm jstl-1.1.2.jar standard-1.1.2.jar; \
}

ENV JAVA_OPTS="-Dsubsonic.defaultMusicFolder=/music/"
COPY etc $JETTY_HOME/etc/

COPY start_libresonic /usr/bin/
CMD ["start_libresonic"]
