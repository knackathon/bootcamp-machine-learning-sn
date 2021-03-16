FROM ubuntu:16.04

# To get rid of error messages like "debconf: unable to initialize frontend: Dialog":
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN apt-get -q update && apt-get install -qy unzip \
    supervisor \
    xmlstarlet \
    vim \
	dos2unix \
    wget \
    default-jre && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

COPY asset/* /opt/

RUN dos2unix /opt/init 
RUN dos2unix /opt/fill-config-parameter 

COPY mid.zip /tmp/mid.zip

RUN unzip -d /opt /tmp/mid.zip && \
    chmod 755 /opt/init && \
    chmod 755 /opt/fill-config-parameter && \
    rm -rf /tmp/*

RUN rm -f /opt/agent/config.xml

#Removed for now
#RUN ln -sf /dev/stdout /opt/agent/logs/agent0.log.0 \
#	&& ln -sf /dev/stderr /opt/agent/logs/wrapper.log

EXPOSE 80 443

VOLUME /opt/agent/scripts
VOLUME /opt/agent/work
VOLUME /opt/agent/keystore

ENTRYPOINT ["/opt/init"]

CMD ["mid:start"]