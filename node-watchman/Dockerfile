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

# vim
RUN apt install -y vim

# cat-bin
RUN yarn global add cat-bin

WORKDIR /root
