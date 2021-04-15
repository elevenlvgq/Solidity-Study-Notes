## 1，实现自己第一个智能合约

函数有四种可见性的类型

public 权限最大，所有人都可以使用

view 不能修改状态变量，能够读取到状态变量

pure 和 view 可节约 gas (不消耗gas)

```jsx
pragma solidity ^0.4.26;

contract helloworld{
    string Myname = "eleven";
    
		//获取自己的名字
		//view 可以节省gas费
		//public 代表最大的权限
    function getName() public view returns(string){
        return Myname;
    }
    //修改名字，
    function changeName(string _newName) public{
        Myname = _newName;
    }
}
```

## 2，节约 gas 的利器 pure 和 view

```jsx

//pure 不消耗 gas  
//（此处代码接 1 部分）
function puretest(string _name) pure public returns(string){
        return _name;
    }
```

## 3，真假 bool 值

```jsx
pragma solidity ^0.4.26;

contract Helloworld{
    bool _a;
    int num1 = 100;
    int num2 = 200;
    
    function getBool() returns(bool){
        return _a;
    }
    
    function getBool2() returns(bool){
        return !_a;
    }
    
    function panduan() returns(bool){
        return num1 == num2;
    }
    
    function panduan2() returns(bool){
        return num1 != num2;
    }
    
    
    // && ||
    
    // true && false = false;
    // false && true = false;
    // true && true = true;
    //true || false = true;

    function  yu() returns(bool){
        return (num1 == num2) && true;
    }
    
    function  yu2() returns(bool){
        return (num1 != num2) && true;
    }
    
    function  huo() returns(bool){
        return (num1 == num2) && true;
    }
    
    function  huo2() returns(bool){
        return (num1 != num2) && true;
    }
    
    function huo3() returns(bool){
        return (num1 == num2) && false;
    }
}
```

## 4，整形特性与运算

定义整型，有两种，int、uint

 int 可正可负

uint 非负

```jsx
pragma solidity ^0.4.26;

contract math{
    
    // int  uint
    
    uint numa = 4;  // int256==int
    uint numb = 2;  // uint256==int
    // uint8 numc = 2;
    
		//加
	  function add(uint a, uint b) pure public returns(uint){
        return a+b;
    }
    //减
    function jian(uint a, uint b) pure public returns(uint){
        return a-b;
    }
    //乘
    function cheng(uint a, uint b) pure public returns(uint){
        return a*b;
    }
    //除
    function achu(uint a, uint b) pure public returns(uint){
        return a/b;
    }
    //余数
    function yu(uint a, uint b) pure public returns(uint){
        return a%b;
    }
    //平方
    function pingfang(uint a, uint b) pure public returns(uint){
        return a**b;
    }
    
}
```

## 5，底层位运算

需要了解二进制的原理

```jsx
pragma solidity ^0.4.26;

contract math{
 
    uint8 a = 3;
    uint8 b = 4;
    
    function weiyu() view public returns(uint){
        return a & b;
    }
    
     function weihuo() view public returns(uint){
        return a | b;
    }
    
     function weifan() view public returns(uint){
        return ~ a;
    }
    
     function weiyihuo() view public returns(uint){
        return a ^ b;
    }
    
     function zuoyi() view public returns(uint){
        return a << 1;
    }
    
     function youyi() view public returns(uint){
        return a >> 1;
    }
    
}
```

## 6，危险的整数溢出以及异常处理

```jsx
pragma solidity ^0.4.26;

contract math{
    
    // int  uint
    
    uint numa = 4;  // int256==int
    uint numb = 2;  // uint256==int
    // uint8 numc = 2;
    
    
    function add(uint a, uint b) pure public returns(uint){
        return a+b;
    }
    
     function jian(uint a, uint b) pure public returns(uint){
        return a-b;
    }
    
     function cheng(uint a, uint b) pure public returns(uint){
        return a*b;
    }
    
     function achu(uint a, uint b) pure public returns(uint){
        return a/b;
    }
    
     function yu(uint a, uint b) pure public returns(uint){
        return a%b;
    }
    
     function pingfang(uint a, uint b) pure public returns(uint){
        return a**b;
    }
    
    
    uint8 a = 3;
    uint8 b = 4;
    
    function weiyu() view public returns(uint){
        return a & b;
    }
    
     function weihuo() view public returns(uint){
        return a | b;
    }
    
     function weifan() view public returns(uint){
        return ~ a;
    }
    
     function weiyihuo() view public returns(uint){
        return a ^ b;
    }
    
     function zuoyi() view public returns(uint){
        return a << 1;
    }
    
     function youyi() view public returns(uint){
        return a >> 1;
    }
    
    
    
    
    
    function flow() view public returns(uint){
        uint8 mm = 255;
        mm++; // mm=mm+1
        return mm;
    }
    
    function flow2() view public returns(uint){
        uint8 mm = 0;
        mm--;// mm=mm-1;
        return mm;
    }
    //
    function errorTest() returns(int){
        int a = 2;
        // int b = 0; 不能执行除0;
        // return a/b; 
    }
    
    function errorTest2() returns(int){
        int a = 2;
        // int b = 0; 不能执行除0;
        // return a/b; 
        int b = -1;
        a<<b;
    }
    
		//整形字面量
    function intergerTest() returns(uint){
        uint num = (2**800+1)-2**800;
        return num;
    }
    
    function intergerTest2() returns(uint){
        uint num = 2/4*1000;
        return num;
    }
    
    function intergerTest3() returns(uint){
        uint num = 111111111111111111111111111111111111111111111111111111111111112 - 111111111111111111111111111111111111111111111111111111111111111;
        return num;
    }
    
}
```

## 7，整形字面量

接上一部分代码

```jsx
		//整形字面量
    function intergerTest() returns(uint){
        uint num = (2**800+1)-2**800;
        return num;
    }
    
    function intergerTest2() returns(uint){
        uint num = 2/4*1000;
        return num;
    }
    
    function intergerTest3() returns(uint){
        uint num = 111111111111111111111111111111111111111111111111111111111111112 - 111111111111111111111111111111111111111111111111111111111111111;
        return num;
    }
    
```

## 8，固定长度字节数组

关键字有：bytes1，bytes2，bytes3，......，bytes32。（步长以 1 递增）。byte 代表 bytes1。

[在线进制转换工具](https://tool.lu/hexconvert/)

加入 public 会自动生成一个函数，不会消耗燃料

```jsx
pragma solidity ^0.4.26;

contract ByteArray {
    // 0x7a68656e676a69616e78756e ---->zhengjianxun
    bytes1 public num1 = 0x7a; // 0111 1010
    bytes2 public num2 = 0x7a68; // 0111 1010 0110 1000
    
    bytes12 public num3 = 0x7a68656e676a69616e78756e; // 011110100110100001100101011011100110011101101010011010010110000101101110011110000111010101101110
		//可以获取长度
		function getLength() returns(uint){
				return num1.length;
		}
		//可以获取长度
		function getLength2() returns(uint){
				return num2.length;
		}
		//可以获取长度
		function getLength3() returns(uint){
				return num3.length;
		}
    //长度不能被修改
		function setLength(){
				// num1.length = 18;
		}
}
```

## 9，固定字节数组深入研究

```jsx
pragma solidity ^0.4.26;

contract ByteArray {
    // 0x7a68656e676a69616e78756e ---->zhengjianxun
    bytes1 public num1 = 0x7a; // 0111 1010
    bytes2 public num2 = 0x7a68; // 0111 1010 0110 1000
    
    bytes12 public num3 = 0x7a68656e676a69616e78756e; // 011110100110100001100101011011100110011101101010011010010110000101101110011110000111010101101110
    
    bytes1 public a = 0x7a;//0111    1010  7*16+10=122
    bytes2 public b = 0x68; //0110    1000  6*16+8=104
    
    function getLength1() returns(uint){
        return num1.length;
    }
    
    function getLength2() returns(uint){
        return num2.length;
    }
    
    function getLength3() returns(uint){
        return num3.length;
    }
    
    function setLength(){
        // num1.length = 18;
    }
    
    
    // bool 比较
    function bijiao1() returns(bool){
        return a > b;
    }
    
    function bijiao2() returns(bool){
        return a >= b;
    }
    
    function bijiao3() returns(bool){
        return a < b;
    }
    
    function bijiao4() returns(bool){
        return a <= b;
    }
    
    function bijiao5() returns(bool){
        return a != b;
    }
    
    
    // 可以进行位运算，但是这块代码有错误，需要校对下
    function weiyu() view public returns(bytes2){
        return a & b;
    }
    
    function weihuo() view public returns(bytes2){
        return a | b;
    }
    
    function weifan() view public returns(bytes2){
        return ~ a;
    }
    
    function weiyihuo() view public returns(bytes2){
        return a ^ b;
    }
    
    function zuoyi() view public returns(bytes2){
        return a << 1;
    }
    
    function youyi() view public returns(bytes2){
        return a >> 1;
    }
    
    
    //内部的数据不能被修改
    function changeContent() public{
        num3[0] = 2;
    }
    
}
```

## 10，动态字节数组

动态字节数组 获取、修改、push 字节，数据都是加在后面。

```jsx
pragma solidity ^0.4.26;

contract DynamicByte{
    
    bytes public name = new bytes(2);  //表示新建了一个初始化的动态字节数组，并给了两个空间
    
    function InitName() public {
        name[0] = 0x7a;
        name[1] = 0x68;
    }
    
		// 获取长度
    function getLength() public view returns(uint){
        return name.length;
    }
    
    // 修改
    function changeName() public {
        name[0] = 0x88;
    }
    
    // 改变长度
    function changeLength() public {
        name.length = 5;
    }
 
		// push 
    function pushTest() public {
        name.push(0x99);
    } 
}
```
