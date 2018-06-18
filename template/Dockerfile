ARG TOOLS_TAG=x86_64-1.1.0
FROM hyperledger/fabric-tools:$TOOLS_TAG

ENV GOPATH=/opt/gopath
ENV CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
ENV CORE_LOGGING_LEVEL=DEBUG
ENV CORE_PEER_ID=cli
ENV CORE_PEER_ADDRESS=peer0.org1.example.com:7051
ENV CORE_PEER_LOCALMSPID=Org1MSP
ENV CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
ENV CORE_CHAINCODE_KEEPALIVE=10

VOLUME [ "/host/var/run/", "/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/", "/opt/gopath/src/github.com/hyperledger/fabric/peer/scripts/", "/opt/gopath/src/github.com/hyperledger/fabric/peer/scripts/env/", "/opt/gopath/src/github.com/hyperledger/fabric-samples/chaincode/marbles02/go"]

WORKDIR /opt/gopath/src/github.com/hyperledger/fabric/peer/scripts

RUN mkdir -p $GOPATH/bin && curl https://raw.githubusercontent.com/golang/dep/master/install.sh

CMD [ "/bin/bash", "-c", "--", "while true; do sleep 30; done;" ]
