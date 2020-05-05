FROM archlinux:latest

RUN pacman -Syuu --noconfirm
RUN pacman -S maven --noconfirm
RUN pacman -S jdk-openjdk --noconfirm
RUN pacman -S java-openjfx --noconfirm
RUN mkdir /home/code
WORKDIR /home/code
RUN curl -OL https://www.eei.cena.fr/products/ivy/download/packages/ivy-java-full-1.2.18.jar
#RUN ls -l /opt/maven/bin
#RUN chmod +rwx /usr/sbin/mvn
RUN /opt/maven/bin/mvn install:install-file -Dfile=ivy-java-full-1.2.18.jar -DgroupId=fr.dgac -DartifactId=Ivy -Dversion=1.2.18 -Dpackaging=jar -DgeneratePom=true
RUN rm ivy-java-full-1.2.18.jar

RUN curl -OL https://artifactory.cronapp.io/public-release/com/google/code/gson/gson-extras/2.8.5/gson-extras-2.8.5.jar
RUN /opt/maven/bin/mvn install:install-file -Dfile=gson-extras-2.8.5.jar -DgroupId=com.google.code.gson -DartifactId=gson-extras -Dversion=2.8.5 -Dpackaging=jar -DgeneratePom=true
RUN rm gson-extras-2.8.5.jar

RUN pacman -Scc --noconfirm
COPY pom.xml /home/code
RUN /opt/maven/bin/mvn compile
RUN /opt/maven/bin/mvn assembly:single
RUN /opt/maven/bin/mvn clean
RUN rm -rf *
RUN rm -rf /tmp/* /var/tmp/*
ENTRYPOINT ["./make.sh"]
