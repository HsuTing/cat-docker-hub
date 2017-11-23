FROM krlmlr/debian-ssh:latest as ssh

FROM node:latest

# upgrade system
RUN apt -y update

# watchman
RUN apt install -y python python-dev
RUN git clone https://github.com/facebook/watchman.git
WORKDIR watchman
RUN git checkout v4.9.0  # the latest stable release
RUN ./autogen.sh
RUN ./configure
RUN make
RUN make install

# cat-bin
RUN yarn global add https://github.com/HsuTing/cat-bin.git

# ssh
RUN apt -y install openssh-server
COPY --from=ssh /set_root_pw.sh /set_root_pw.sh
COPY --from=ssh /run.sh /run.sh
RUN mkdir -p /var/run/sshd && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
  && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
  && touch /root/.Xauthority \
  && true

RUN useradd docker \
  && passwd -d docker \
  && mkdir /home/docker \
  && chown docker:docker /home/docker \
  && addgroup docker staff \
  && addgroup docker sudo \
  && true

# expose
# use the port you need
EXPOSE 22
EXPOSE 8000
EXPOSE 8080
EXPOSE 9000

WORKDIR /root
CMD "/run.sh"
