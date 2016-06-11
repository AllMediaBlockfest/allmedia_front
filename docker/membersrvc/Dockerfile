#
# Hyperledger member service. Uses the latest hyperledger git.
#
FROM hyperledger/fabric-baseimage:x86_64-0.0.9
MAINTAINER A. Rutjes <arne.rutjesISC@nl.ibm.com>

ENV GOROOT /opt/go
ENV GOPATH /opt/go
ENV PATH $GOROOT/bin:$PATH
ENV FABRIC $GOROOT/src/github.com/hyperledger/fabric

RUN git clone https://github.com/hyperledger/fabric.git $FABRIC && cd $FABRIC && git checkout a713bd5ff065150db90d1e0dfaa8e1230933b3c4 .
RUN cd $FABRIC/membersrvc \
 && CGO_CFLAGS=" " CGO_LDFLAGS="-lrocksdb -lstdc++ -lm -lz -lbz2 -lsnappy" go install \
 && go build

COPY membersrvc.yaml $FABRIC/membersrvc
EXPOSE 50051

WORKDIR $FABRIC/membersrvc
CMD ["./membersrvc", "peer"]
