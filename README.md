# quananon
Quantum_AnonCreds_Dew_Edge
# Initial setup for secure communication for Dynamic Identity, AnonCreds , Bell GHZ states , Chaincode, etc.
We employed Bionic 18.04.4, Pandas, Python 3.6, Jupyter Notebook, and Hyperledger AnonCreds 1.0 to create and confirm Dynamic Identities (DID), Wallet addresses, Healthcare CHoT participants. AnonCreds 1.0 operates with the Hyperledger Indy platform to generate an Indy System Pool, assigning verifier roles like Trust Anchor (role '101') or Trustee (role '0') using Nym Transactions in our main21.py program.

1. Start Docker with the following command
docker-compose up-d

to stop the docker after experiment
docker-compose down

2. Installation
AnonCreds 1.0 collaborates with the Hyperledger Indy platform, creating an Indy System Pool that assigns predefined verifiers, such as Trust Anchors (role '101') and Trustees (role '0'), through Nym Transactions in our main21.py program.

Please go inside path # cd fabric

./ install.sh

during Installation of Fabric, also please confirm that the following commands will run successfully
/network down

./network up

Add mychannel:

./network.sh createChannel -c mychannel

Add simple chaincode to channel:

./network.sh deployCC -ccn simple -ccp /home/suman/Downloads/caliper-benchmarks/src/fabric/samples/marbles/go -ccl go

Invoke chain code:

peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n simple --peerAddresses localhost:7051 --tlsRootCertFiles

${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses localhost:9051 --tlsRootCertFiles

${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt -c '{"function":"InitLedger","Args":[]}'

in test-networkfolder (onetime thing):

export FABRIC_CFG_PATH=$PWD/../config/

export CORE_PEER_TLS_ENABLED=true

export CORE_PEER_LOCALMSPID="Org1MSP"

export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt

export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp

export CORE_PEER_ADDRESS=localhost:7051

3. Installation of Ethereum platform
cd ethereum

sudo ./ install.sh

4. Installation of Hyperledger Indy platform for starting the system pool for AnonCreds and run the AnonCreds funcionality under Hyperledger platform
a.First clone Indy node repository for starting the repository using the commands-

git clone https://github.com/hyperledger/indy-node.git

Then go inside the directory using the command - cd indy-sdk

b. starting with a pre-configured docker image to build and run it for the pool:

docker build -f ci/indy-pool.dockerfile -t indy_pool.

docker run -itd -p 9701-9708: 9701-9708 ghoshbishakh/indy_pool

This creates an Indy container housing a pool of system-validated authenticators, each with a unique identity, pool number, and assigned port between 9701-9708.

c.Then run- docker ps , to get the container identity forexample in our case it is 351k39691g56. Then go inside the indy pool docker container using the command - docker exec -it 351k39691g56 bash

d. Now go inside the container 351k39691g56 and run the command - cat /var/lib/indy/sandbox/pool_transactions_genesis
to get the details information of each validator nodes.

e. Now open a terminal and copy the information of all the information of validators nodes in to an text editotor that is opened using the command -'code.'. and past all the information into the text editor and save it as 'pool1.txn' that is basically a type of JSON file for communication with the AnonCreds main code.

f. Import "main21.py" into the folder containing 'pool1.txn' to integrate Hyperledger AnonCreds for generating dynamic IDs, wallet addresses, and verifiable credentials for anonymous marketplace participant validation.

g. Now Import "main30.py" and "Registrationcontract.sol" into the editor's folder containing 'pool1.txn', then execute "main30.py" to validate dynamic identities and wallet addresses before registering marketplace participants.

All such coding related the aforesaid procedure is already uploaded under the path - ### smajumder/did_wallet_management/indy-sdk/
