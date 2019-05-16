FROM openjdk:8
COPY *.jar /backend.jar
RUN mkdir /config
WORKDIR /
RUN apt-get update && apt-get install htop net-tools telnet -y
ENV BUSER=bidopin
ENV BPASS=
ENV JWTSEC=XDQ-FYpq_PWMNVYCPS
ENTRYPOINT  java  -Dlog.logDirectory=/var/log/backend -Dspring.profiles.active=beta -Dspring.datasource.url=jdbc:postgresql://192.168.66.14:5432/bidopin -Dthread.pool.push.count=2 -Dserver.undertow.worker-threads=4 -Dspring.datasource.hikari.maximumPoolSize=4  -Djwt.secret=$JWTSEC -Dspring.datasource.username=$BIDBUSER -Dspring.datasource.password=$BIDBPASS  -jar /backend.jar
