以太坊地址

```jsx
pragma solidity ^0.4.26;

contract addresstest{
    
    address public account = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4; 
    //0x5B38Da6a701c568545dCfcB03FcB875f56beddC4    uint160
    //0xd9145CCE52D386f254917e481eB44e9943F39138   
    
    
    address account1 = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;
    address account2 = 0x358AA13c52544ECCEF6B0ADD0f801012ADAD5eE3;
    
    
    
    //转换地址
    function changeIt() view returns(uint160){
        return uint160(account); //520786028573371803640530888255888666801131675076
    }
    
		//反向转换
    function changeIt2() view returns(address){
        return address(520786028573371803640530888255888666801131675076); //0x5B38Da6a701c568545dCfcB03FcB875f56beddC4 
    }
    
    //可以进行地址大小判断
    function check1() view returns(bool){
        return account1 > account2;
    }
    
    function check2() view returns(bool){
        return account1 >= account2;
    }
    
    function check3() view returns(bool){
        return account1 < account2;
    }
    
    function check4() view returns(bool){
        return account1 <= account2;
    }
    
    
}
```

转移资金

```jsx
pragma solidity ^0.4.26;

//payable 关键字代表我们可以通过这个函数给我们的合约地址充值，转账，
contract payabletest{
    
		//转账
    function pay() payable{
        
    }
    
		//获取账户上的金额
    function getbalance() returns(uint){
        return this.balance; //this 代表当前合约地址，balance 代表合约地址的一个属性
    }

		//0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2   账户
    //0x8431717927C4a3343bCf1626e7B5B1D31E240406   合约地址
    //0x8431717927C4a3343bCf1626e7B5B1D31E240406
    function getthis() view returns(address){
        return this; // 获取这个账户的地址
    }
    
    //获取合约地址的余额
    function getrandombalance() view returns(uint){
        address account = 0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2;
        return account.balance;
    }
    
		//获取合约地址的余额
    function getrandombalance2(address account) view returns(uint){
        return account.balance;
    }
    

		//外部账户向外部账户转账
		function transfer() payable{
        address account = 0xdD870fA1b7C4700F2BD7f44238821C26f7392148;
        account.transfer(msg.value);  //msg.value 是一个全局变量
    }  
    
    
    //转账到合约地址    
    function transfer2() payable{
        this.transfer(msg.value);
    }
    
		//需要加上这个回滚函数，回滚函数需要加上 payable
    function () payable{
        
    }
		
}
```

部分全局变量

```jsx
pragma solidity ^0.4.26;

contract global{
    
		
    function getglobal() returns(address){
        return msg.sender;  //0x617F2E2fD72FD9D5503197092aC168c91465E7f2
    }
    

        
    function getglobal2() returns(uint){
        return block.difficulty;  
    }
    
    
    
        
    function getglobal3() view returns(uint){
        return block.number;  
    }
    
    
            
    function getglobal4() view returns(address){
        return block.coinbase;  
    }
    

		function sendmoney() payable returns(bool){
        address account = 0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2;
        return account.send(10 ether);
    }

    
}
```

mapping 映射

```jsx
pragma solidity ^0.4.26;

contract mappingtest{
		//定义 mapping     idmapping 代表地址与 id 映射到了一起，namemapping 代表与名字的字符串映射到了一起
    mapping(address => uint) idmapping;  //0x5B38Da6a701c568545dCfcB03FcB875f56beddC4 => 1
    mapping(uint => string) namemapping;  //1 => zheng
    
    //注册的总量
    uint public sum = 0;
    
    //
    function register(string name){
				//获取当前合约的调用者
        address account = msg.sender;
        sum++;

				//将合约的调用者的地址与注册总量 id 联系到了一起
        idmapping[account] = sum;

				//当前用户 id 与用户注册的名字绑定到了一起
        namemapping[sum] = name;
    }
    //通过关键字地址获取到和他绑定在一起的 id 值
    function getidbyaddress(address are) view returns(uint){
        return idmapping[are];
    }
    
    //通过 id 值获取到和他绑定在一起的名字
    function getnamebyid(uint id) view returns(string){
        return namemapping[id];
    }
    
    
    
}
```
