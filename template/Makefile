.PHONY: attach_cli destroy_cli setup_new_cc upgrade_existing_cc list_channels


include .env

export $(shell sed 's/=.*//' .env)


attach_cli:
	docker build -t mybc-cli --build-arg TOOLS_TAG=$(FABRIC_TOOLS_TAG) .
	docker run --name $(CHAIN_NETWORK)_cli --network=$(CHAIN_NETWORK) -d \
		-v /var/run/:/host/var/run/ \
		-v $(CRYPTO_CONFIG_DIR):/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ \
		-v $(CLI_SCRIPTS_DIR)/:/opt/gopath/src/github.com/hyperledger/fabric/peer/scripts/ \
		-v $(CC_DIR):/opt/gopath/src/github.com/hyperledger/fabric-samples/chaincode/marbles02/go/ \
    -v $(CC_ENV_DIR):/opt/gopath/src/github.com/hyperledger/fabric/peer/scripts/env/ \
		mybc-cli:latest

destroy_cli:
	docker container stop $(CHAIN_NETWORK)_cli
	docker container rm $(CHAIN_NETWORK)_cli

setup_new_cc:
	docker exec -t $(CHAIN_NETWORK)_cli bash  -c "make cc_install"
	docker exec -t $(CHAIN_NETWORK)_cli bash  -c -- "make cc_instantiate"

upgrade_existing_cc:
	docker exec -t $(CHAIN_NETWORK)_cli bash  -c -- "make cc_install"
	docker exec -t $(CHAIN_NETWORK)_cli bash  -c -- "make cc_upgrade"

list_channels:
	docker exec -t $(CHAIN_NETWORK)_cli bash  -c -- "make chn_list"
