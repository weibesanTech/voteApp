# voteApp

**项目背景**：
投票最担心的是暗箱操作，我们可以利用区块链的去中心化技术来实现一个DAPP，保证投票的公正、公平。

**需求描述**：
1. 每人只能投票一票
2. 记下一共又多少候选人
3. 记录每个候选人的得票数
==*在用户界面上，需要看到每个候选人的得票数以及选择候选人进行投票，需求设计效果如图所示：==*


**编写智能合约**:
Election.sol
`pragma solidity >=0.5.0 <0.7.0;`

`contract Election {`

`// Model a Candidate`

`struct Candidate {`

`uint id;`

//候选人
`string name;`

//得票数
`uint voteCount;`

`}`

`// Store accounts that have voted`

`mapping(address => bool) public voters;`

`// Store Candidates`

`// Fetch Candidate`

`mapping(uint => Candidate) public candidates;`

`// Store Candidates Count`

`uint public candidatesCount;`

`// voted event`

`event votedEvent (`

`uint indexed _candidateId`

`);`

`constructor() public {`

`addCandidate("Tiny 熊");`

`addCandidate("Big 熊");`

`}`

`function addCandidate (string memory _name) private {`

`candidatesCount ++;`

`candidates[candidatesCount] = Candidate(candidatesCount, _name, 0);`

`}`

`function vote (uint _candidateId) public {`

`// require that they haven't voted before`

`require(!voters[msg.sender]);`

`// require a valid candidate`

`require(_candidateId > 0 && _candidateId <= candidatesCount);`

`// record that voter has voted`

`voters[msg.sender] = true;`

`// update candidate vote Count`

`candidates[_candidateId].voteCount ++;`

`// trigger voted event`

`emit votedEvent(_candidateId);`

`}`

`}`

`
``
