FROM openjdk:8-jre

RUN echo "deb http://www.ubnt.com/downloads/unifi/debian unifi-5.6 ubiquiti" > /etc/apt/sources.list.d/unifi.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C0A52C50
RUN apt-get update && apt-get upgrade -y && apt-get install unifi net-tools -y && apt clean all && rm -rf /var/cache/apt/*
RUN usermod -d /var/lib/unifi unifi
EXPOSE 3478/udp 6789/tcp 8080/tcp 8443/tcp 8843/tcp 8880/tcp 8881/tcp 8882/tcp
RUN mkdir -p /var/run/unifi /var/log/unifi /var/lib/unifi && \
	chmod 700 /var/lib/unifi /var/run/unifi /var/log/unifi && \
    chown unifi:root /var/log/unifi/ /var/run/unifi/ /var/run/unifi/ /var/lib/unifi/
RUN ln -s /var/log/unifi/ /logs ; ln -s /tmp/ /usr/lib/unifi/work ; \
	ln -s /var/log/unifi/ /usr/lib/unifi/logs ; ln -s /var/run/unifi/ /usr/lib/unifi/run ; \
	ln -s /var/lib/unifi/ /usr/lib/unifi/data
USER unifi:root

CMD [ "/usr/lib/jvm/java-8-openjdk-amd64/bin/java", \
      "-cp", "/usr/share/java/commons-daemon.jar:/usr/lib/unifi/lib/ace.jar", \
      "-Dunifi.datadir=/var/lib/unifi", \
      "-Dunifi.rundir=/var/run/unifi", \
      "-Xmx1024M", \
      "-Djava.awt.headless=true", \
      "-Dfile.encoding=UTF-8", \
      "com.ubnt.ace.Launcher", \
      "start" ]
