# FROM ubuntu:latest
FROM phusion/baseimage:latest

LABEL maintainer="edoardo.zanoni@gambabruno.it"

# Variabili della build
ENV	LANG=C.UTF-8 \
	OLD_JDK1_VER=1.3.1_20

# Aggiornamento ed installazione delle applicazioni di base
RUN sed 's/main$/main universe/' -i /etc/apt/sources.list && \
    apt-get update -qq && \
    echo 'Installing OS dependencies' && \
    apt-get install -qq -y --fix-missing sudo \
		software-properties-common \
		libxext-dev \
		libxrender-dev \
		libxslt1.1 \
		libxtst-dev \
		libgtk2.0-0 \
		libcanberra-gtk-module \
		libsecret-1-0 \
		lib32z1 \
		git \
		gnome-keyring \
		unzip \
		wget \
		openjdk-8-jdk && \
    echo 'Cleaning up' && \
    apt-get clean -qq -y && \
    apt-get autoclean -qq -y && \
    apt-get autoremove -qq -y &&  \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

# Creazione utente principale (developer)
RUN echo 'Creating user: developer' && \
    mkdir -p /home/developer && \
    echo "developer:x:1000:1000:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:1000:" >> /etc/group && \
    sudo echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    sudo chmod 0440 /etc/sudoers.d/developer && \
    sudo chown developer:developer -R /home/developer && \
    sudo chown root:root /usr/bin/sudo && \
    chmod 4755 /usr/bin/sudo

# Attivazione JDK 3
	wget https://github.com/Ryther/intellij-idea/raw/master/docker/jvm/jdk${OLD_JDK1_VER}.tar -O /tmp/jdk${OLD_JDK1_VER}.tar -q && \
	tar -xzvf /tmp/jdk${OLD_JDK1_VER}.tar -C /usr/lib/jvm/ && \
	rm -rf /tmp/* && \
	sudo update-alternatives --install "/usr/bin/java" "java" \
	"/usr/lib/jvm/jdk${OLD_JDK1_VER}/bin/java" 1 && \
	sudo update-alternatives --install "/usr/bin/javac" "javac" \
	"/usr/lib/jvm/jdk${OLD_JDK1_VER}/bin/javac" 1

# Impostazione dell'owner della cartella (developer)
RUN sudo chown developer:developer -R /home/developer

# Creazione dei mounting point
VOLUME [ "/home/developer" ]
VOLUME [ "/tmp/.X11-unix" ]

# Operazioni finali
USER developer
ENV HOME /home/developer
WORKDIR /home/developer
ENTRYPOINT [ "/bin/bash" ]
