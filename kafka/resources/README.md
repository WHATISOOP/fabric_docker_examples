# create channel 
peer channel create -o orderer.example.com:7050 -c demochannel -f ./channel-artifacts/demochannel.tx --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/tlsca/tlsca.example.com-cert.pem
# join channel
peer channel join -b demochannel.block
# install chaincode
peer chaincode install -n chaincode_example02 -v 1.0 -p github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02
# init chaincode
peer chaincode instantiate -o orderer.example.com:7050 -C demochannel -n chaincode_example02 -v 1.0 -c '{"Args":["init","a","100","b","200"]}' --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/tlsca/tlsca.example.com-cert.pem
# invoke chaincode
peer chaincode invoke -C demochannel -n chaincode_example02 -v 1.0 -c '{"Args":["invoke","a","b","10"]}' --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/tlsca/tlsca.example.com-cert.pem
# query chaincode
peer chaincode query -C demochannel -n chaincode_example02 -v 1.0 -c '{"Args":["query","a"]}'
