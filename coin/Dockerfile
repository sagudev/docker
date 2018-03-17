FROM sagu/coin:build
ENV version=master
RUN git clone https://github.com/sagudev/freecoin.git -b ${version}
WORKDIR /freecoin
RUN ./autogen.sh
RUN ./configure
RUN make
RUN make install
#open service port
EXPOSE 9666 19666
CMD ["freecoind", "--printtoconsole"]