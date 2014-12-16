FROM jjhughes57/apacheds-docker
MAINTAINER Reinold Pasterkamp

# Use config with cds partition
COPY ./config.ldif /var/lib/apacheds-2.0.0-M19/default/conf/


#load default users and groups
ADD https://raw.githubusercontent.com/CDS-VRN/CDS-Assembly/assembly-docker/src/main/docker/cds-ldap/ldap-ontw.ldif /root/ldap-ontw.ldif
RUN /opt/apacheds-2.0.0-M19/bin/apacheds start default && \
    sleep 5 && \
	ldapadd -h localhost -p 10389 -w secret -f /root/ldap-ontw.ldif -D uid=admin,ou=system -c && \
	sleep 5 && \
	/opt/apacheds-2.0.0-M19/bin/apacheds stop default && \
	sleep 5 



ENTRYPOINT /opt/apacheds-2.0.0-M19/bin/apacheds console default