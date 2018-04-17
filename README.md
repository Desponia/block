# block

> geth --networkid 4649 --nodiscover --maxpeers 0 --datadir data_testnet/ console 2>> data_testnet/geth.log

> geth --datadir data_testnet/ account new

> geth --datadir data_testnet/ account list

- EtherBase : 채굴 성공시 보상 받는 계정 기본적으로 0번 계정
> eth.coinbase
- 변경하려면
> eth.setEtherbase(eth.accounts[숫자])
- 계정의 잔고 확인
> eth.getBalance(eth.accounts[숫자])
- 블록체인의 블록 수 확인
> eth.blockNumber
- 계정 잠금 해제 (송금 등을 위해)
> personal.unlockAccount(eth.accounts[1], "pass1", 0)
- 송금
> eth.sendTransaction({from:eth.accounts[0], to:eth.accounts[1], value:web3.toWei(10, "ether")})
- 송금 확인
> eth.getTransaction("위에서 나온 해쉬 값")
- 송금이 0인 경우 송금 보류된 블락이 있는지 체크
> eth.pendingTransactions
- 펜딩된 게 있으면 다시 채굴하여 블락 생성 후 다시 펜딩 조회, 다시 송금 확인
- 몇 ether 송금되었는지 확인
> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")

nohup geth --networkid 4649 --nodiscover --maxpeers 0 --datadir blockTest/ --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" 2>> blockTest/geth.log &



curl -X POST --data '{"jsonrpc":"2.0","method":"personal_newAccount","params":["pass3"],"id":10}' localhost:8545


위에 두개는 프로세스는 살아있는데 잘 안됨

- solidity compiler 설치
 책에는 우분투 apt 기준으로 나와있어서 맥 기준 ( http://solidity.readthedocs.io/en/v0.4.21/installing-solidity.html 참고 )
> brew update
> brew upgrade
> brew tap ethereum/ethereum
> brew install solidity

내 솔리디티 경로는
/usr/local/Cellar/solidity/0.4.22
이걸 설치하는데 엄청난 디펜던시들을 설치하고 30분 걸렸다. 맞는건가..  sqllite, openssl 

인 줄 알았는데 which solc 날려보니 /usr/local/bin/solc


> nohup geth --networkid 4649 --nodiscover --maxpeers 0 --datadir blockTest/ --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --unlock 0,1 --password blockTest/passwd --verbosity 6 2>> blockTest/geth.log &

> geth attach rpc:http://localhost:8545


> Fatal: Failed to start the JavaScript console: api modules: Post http://localhost:8545: dial tcp [::1]:8545: connect: connection refused

T.T

