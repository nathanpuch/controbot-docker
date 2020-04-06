FROM archlinux:latest

RUN pacman -Syuu --noconfirm
RUN pacman -S maven --noconfirm
RUN pacman -S jdk-openjdk --noconfirm
RUN pacman -S java-openjfx --noconfirm
RUN mkdir /home/code
WORKDIR /home/code
RUN curl -OL https://www.eei.cena.fr/products/ivy/download/packages/ivy-java-full-1.2.18.jar
RUN chmod +rwx /usr/sbin/mvn
RUN mvn install:install-file -Dfile=ivy-java-full-1.2.18.jar -DgroupId=fr.dgac -DartifactId=Ivy -Dversion=1.2.18 -Dpackaging=jar -DgeneratePom=true
RUN rm ivy-java-full-1.2.18.jar
RUN pacman -Scc --noconfirm
COPY pom.xml /home/code
RUN mvn compile
RUN mvn assembly:single
RUN mvn clean
RUN rm -rf *
RUN rm -rf /tmp/* /var/tmp/*
ENTRYPOINT ["./make.sh"]
