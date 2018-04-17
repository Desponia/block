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
