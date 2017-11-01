FROM debian:stable-slim
ENV DEBIAN_FRONTEND=noninteractive
ENV DEBIAN_FRONTEND=teletype
RUN apt-get update && apt-get -y install \
																 kmod \
																 inetutils-inetd \
																 tftpd-hpa && \
		rm -rf /var/lib/apt/lists/*
COPY ./netboot /srv/tftp

RUN echo "tftp    dgram   udp4    wait    root    /usr/sbin/in.tftpd /usr/sbin/in.tftpd -s /srv/tftp" >> /etc/inetd.conf && \
		echo 'RUN_DAEMON="yes"' >> /etc/default/tftpd-hpa && \
		echo 'OPTIONS="-l -s /srv/tftp"' >> /etc/default/tftpd-hpa && \
		echo 'while [[ $(/etc/init.d/tftpd-hpa status | grep "is running") ]]; do sleep 10 ; done' > /loop.sh && chmod +x /loop.sh

EXPOSE 69/udp
VOLUME /srv/tftp
WORKDIR /srv/tftp

CMD /etc/init.d/tftpd-hpa start && /bin/bash -c /loop.sh