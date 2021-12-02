# The Anatomy of ERC-20

[Article URL](https://medium.com/blockchannel/the-anatomy-of-erc20-c9e5c5ff1d02)

Ethereum Request for Comments 20, or ERC20, is an **Ethereum Improvement Proposal** introduced by Fabian Vogelstellar in late 2015. It's a standard by which many popular Ethereum smart contracts abide.

ERC20 allows smart contracts to act very similarly to a conventional cryptocurrency like Bitcoin or Ethereum itself. A token hosted on the Ethereum blockchain can be sent, received, checked of its total supply, and checked for the amount that is available on an individual address. This is analogous to sending and receiving Ether or Bitcoin from a wallet, knowing the total amount of coins in circulation, and knowing a particular wallet’s balance of a coin.

## ERC-20 Functions

### From a high level

```js
// Grabbed from: https://github.com/ethereum/EIPs/issues/20
contract ERC20 {
   function totalSupply() constant returns (uint theTotalSupply);
   function balanceOf(address _owner) constant returns (uint balance);
   function transfer(address _to, uint _value) returns (bool success);
   function transferFrom(address _from, address _to, uint _value) returns (bool success);
   function approve(address _spender, uint _value) returns (bool success);
   function allowance(address _owner, address _spender) constant returns (uint remaining);
   event Transfer(address indexed _from, address indexed _to, uint _value);
   event Approval(address indexed _owner, address indexed _spender, uint _value);
}
```

### totalSupply()

This function allows an instance of the contract to calculate and return the total amount of the token that exists in circulation.

```js
contract MyERCToken {
  // In this case, the total supply
  // of MyERCToken is fixed, but
  // it can very much be changed
  uint256 _totalSupply = 1000000;
  
  function totalSupply() constant returns (uint256 theTotalSupply) {
    // Because our function signature
    // states that the returning variable
    // is "theTotalSupply", we'll just set that variable
    // to the value of the instance variable "_totalSupply"
    // and return it
    theTotalSupply = _totalSupply;
    return theTotalSupply;
  }
}
```

### balanceOf()

This function allows a smart contract to store and return the balance of the provided address. The function accepts an address as a parameter, so it should be known that the balance of any address is public.

```js
contract MyERCToken {
  // Create a table so that we can map addresses
  // to the balances associated with them
  mapping(address => uint256) balances;
  // Owner of this contract
  address public owner;
  
  function balanceOf(address _owner) constant returns (uint256 balance) {
    // Return the balance for the specific address
    return balances[_owner];
  }
}
```

### approve()

By calling this function, the owner of the contract authorizes, or *approves* the given address to withdraw instances of the token from the owner's address.

**NOTE** Here and in later snippets, you will see a variable **msg**. This is an implicit field provided by external applications like wallets so that they can better interact with the contract. The EVM lets us use this field to hold and process data given by the external application.

Here, `msg.sender` is the address of the contract owner.

```js

contract MyERCToken {
  // Create a table so that we can map
  // the addresses of contract owners to
  // those who are allowed to utilize the owner's contract
  mapping(address => mapping (address => uint256)) allowed;
  
  function approve(address _spender, uint256 _amount) returns (bool success) {
    allowed[msg.sender][_spender] = _amount;
    // Fire the event "Approval" to execute any logic
    // that was listening to it
    Approval(msg.sender, _spender, _amount);
    return true;
  }
}
```

### transfer()

This function lets a contract owner send a specified amount of the token to another address just like a conventional crypto transaction.

```js
contract MyERCToken {
  mapping(address => uint256) balances;
  
  // Note: This function returns a boolean value
  //       indicating whether the transfer was successful
  function transfer(address _to, uint256 _amount) returns (bool success) {
    // If the sender has sufficient funds to send
    // and the amount is not zero, then send to
    // the given address
    if (balances[msg.sender] >= _amount 
      && _amount > 0
      && balances[_to] + _amount > balances[_to]) {
      balances[msg.sender] -= _amount;
      balances[_to] += _amount;
      // Fire a transfer event for any
      // logic that's listening
      Transfer(msg.sender, _to, _amount);
        return true;
      } else {
        return false;
      }
   }
}
```

### transferFrom()

This function lets a smart contract owner to automate the transfer process and send a given amount of a token on behalf of the owner.

Question: **Why do we need both `transfer()` and `transferFrom()` functions?**

Using `transfer()` is like manually sending money. You're doing the money transfer process yourself, without the help of another party.

Using `transferFrom()` is like setting up an automatic bill pay with your bank. With this function, a contract can send a certain amount of the token to another address on your behalf without your intervention.

```js
contract MyERCToken {
  mapping(address => uint256) balances;
  
  function transferFrom(address _from, address _to, uint256 _amount) returns (bool success) {
    if (balances[_from] >= _amount
      && allowed[_from][msg.sender] >= _amount
      && _amount > 0
      && balances[_to] + _amount > balances[_to]) {
    balances[_from] -= _amount;
    balances[_to] += _amount;
    Transfer(_from, _to, _amount);
      return true;
    } else {
      return false;
    }
  }
}
```

## Optional ERC20 fields

### Token Name

Used by many popular wallets to identify the token

```js
contract MyERCToken {
  string public constant name = "My Custom ERC20 Token";
}
```

### Token Symbol

Another identifying field. 3 or 4 letter symbol abbreviation.

```js
contract MyERCToken {
  string public constant symbol = "MET";
}
```

### Number of Decimals

Used to determine to what decimal place the amount of the token will be calculated. Most common is 18.

```js
contract MyERCToken {
  uint8 public constant decimals = 18;
}
```

[Total source code of ERC20 token](https://gist.github.com/aunyks/aa97affc1dc47ba6ca881f9bf7897637)

