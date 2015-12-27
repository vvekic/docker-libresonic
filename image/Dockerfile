FROM java:7-jdk

RUN { \
	export DEBIAN_FRONTEND=noninteractive; \
	apt-get update; \
	apt-get install -y maven tomcat8 libav-tools; \
	git clone https://github.com/EugeneKay/subsonic.git /tmp/subsonic; \
	cd /tmp/subsonic; \
	git checkout 67b003a3d15756552a0c59aa8b73a66de6854a6a; \
	mvn package; \
	mv /tmp/subsonic/subsonic-main/target/subsonic.war /usr/share/tomcat8/webapps/; \
	rm -r /tmp/*; \
	systemctl disable tomcat8; \
	mkdir -p \
		/usr/share/tomcat8/webapps \
		/usr/share/tomcat8/common/classes \
		/usr/share/tomcat8/shared/classes \
		/usr/share/tomcat8/server/classes \
		/usr/share/tomcat8/work \
		/usr/share/tomcat8/temp \
		/usr/share/tomcat8/logs; \
	chown tomcat8:tomcat8 -R \
		/usr/share/tomcat8/webapps \
		/usr/share/tomcat8/common/classes \
		/usr/share/tomcat8/shared/classes \
		/usr/share/tomcat8/server/classes \
		/usr/share/tomcat8/work \
		/usr/share/tomcat8/temp \
		/usr/share/tomcat8/logs; \
	apt-get remove --purge -y maven; \
	apt-get autoremove -y; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*; \
}

ADD tomcat-conf /usr/share/tomcat8/conf
RUN chown tomcat8:tomcat8 -R /usr/share/tomcat8/conf

ADD start_subsonic /usr/bin/
CMD ["start_subsonic"]
