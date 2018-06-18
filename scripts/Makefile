## This make file will be available within fabric-cli-tools docker container
## Thus allowing interaction with channel to install/instantiate/upgrade chaincode
.PHONY: cc_dep cc_install cc_upgrade cc_instantiate chn_list

include ./env/.env
export $(shell sed 's/=.*//' ./env/.env)


cc_dep:
	mkdir -p $(GOPATH)/bin	

cc_install: cc_dep
ifeq ($(CORE_PEER_TLS_ENABLED), true)
	peer chaincode install --tls $(CORE_PEER_TLS_ENABLED) -C $(CHANNEL_NAME) -n $(CC_NAME) -v $(CC_VERSION)-P $(ENDORSEMENT_POLICY_EXPR)
else
	peer chaincode install -n $(CC_NAME)  -v $(CC_VERSION) -p $(CC_SRC_PATH)	    	
endif

cc_instantiate:
ifeq ($(CORE_PEER_TLS_ENABLED), true)
	peer chaincode instantiate -o $(ORDERER) --tls $(CORE_PEER_TLS_ENABLED) --cafile $(ORDERER_CA) -C $(CHANNEL_NAME) -n $(CC_NAME)  -v $(CC_VERSION) -c '{"Args":[]}' -P $(ENDORSEMENT_POLICY_EXPR)
else
	peer chaincode instantiate -o $(ORDERER) -C $(CHANNEL_NAME) -n $(CC_NAME)  -v $(CC_VERSION) -c '{"Args":[]}' -P $(ENDORSEMENT_POLICY_EXPR)
endif

cc_upgrade:
ifeq ($(CORE_PEER_TLS_ENABLED), true)
	peer chaincode upgrade -o $(ORDERER) --tls $(CORE_PEER_TLS_ENABLED) --cafile $(ORDERER_CA) -C $(CHANNEL_NAME) -n $(CC_NAME)  -v $(CC_VERSION) -c '{"Args":[]}' -P $(ENDORSEMENT_POLICY_EXPR)
else
	peer chaincode upgrade -o $(ORDERER) -C $(CHANNEL_NAME) -n $(CC_NAME)  -v $(CC_VERSION) -c '{"Args":[]}' -P $(ENDORSEMENT_POLICY_EXPR)
endif

chn_list:
	peer channel list