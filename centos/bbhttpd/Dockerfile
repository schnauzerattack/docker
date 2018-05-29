# Webserver container with CGI python script
# Using RHEL 7 base image and Apache Web server
# Version 1

# Pull the rhel image from the local repository
FROM centos:latest
USER root

MAINTAINER Maintainer_Name

# Fix per https://bugzilla.redhat.com/show_bug.cgi?id=1192200
RUN yum -y install deltarpm yum-utils --disablerepo=*-eus-* --disablerepo=*-htb-* \
    --disablerepo=*-ha-* --disablerepo=*-rt-* --disablerepo=*-lb-* --disablerepo=*-rs-* --disablerepo=*-sap-*

RUN yum-config-manager --disable *-eus-* *-htb-* *-ha-* *-rt-* *-lb-* *-rs-* *-sap-* > /dev/null


# Update image
RUN yum update -y
RUN yum install httpd mod_ssl php php-mysql -y

# Add configuration file
#ADD wp/wordpress/ /var/www/html/
COPY wp/latest.tar.gz /latest.tar.gz
RUN tar -xzvf latest.tar.gz --directory=/var/www/html --strip 1
RUN chown -R apache:apache /var/www/html/*
EXPOSE 80
EXPOSE 443

# Start the service
CMD ["-D", "FOREGROUND"]
ENTRYPOINT ["/usr/sbin/httpd"]

