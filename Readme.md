# Event Processing Based on the EventType
- Reference Material : the linux foundation lfd272

## Set Netowrk && Environment

### test-network 구동
- hyperledger fabric v2.2
- ./network.sh up createChannel -ca -s couchdb

### CouchDB URL
- http://localhost:5984/_utils 확인 가능
- COUCHDB_USER=admin
- COUCHDB_PASSWORD=adminpw

### Terminal 1 Environment variables for Org1MS 
- export PATH=${PWD}/../bin:$PATH
- export FABRIC_CFG_PATH=$PWD/../config/
- cd $HOME/go/src/github.com/pwhdgur/hyperledger/fabric-samples/test-network
- export CORE_PEER_TLS_ENABLED=true
- export CORE_PEER_LOCALMSPID="Org1MSP"
- export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
- export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
- export CORE_PEER_ADDRESS=localhost:7051

## Deploy SimpleContract Chaincode
- cd $HOME/go/src/github.com/pwhdgur/hyperledger/fabric-samples/test-network
- ./network.sh deployCC -ccn simple_chaincode -ccv 1.0 -ccp ~/go/src/github.com/pwhdgur/hyperledger/fabric-samples/lfd272/chaincodes/Lab13/simple_chaincode -ccl javascript

## Install the application and Create identities.
- Created wallet directory containing the identities od User1 and Admin from both Org1 and Org2
- npm install
- node addToWallet.js

## Run Application
- emit simple_event
- node submitTransaction.js 'Admin@org1.example.com' emitEvent simple_event 'Hello, World!'

- submit the put transaction
- node submitTransaction.js 'Admin@org1.example.com' put objType key value

## Docker Log
- docker logs dev-peer0.org1.example.com-reports_1.0-3e5c30afbe220a0c5d91e6c9fe58a8e40938bd1c59176dcf4e3e728f13ba3e27 -f

## Clear Up
- ./network.sh down