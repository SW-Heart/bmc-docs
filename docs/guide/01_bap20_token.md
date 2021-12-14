# BAP20 Token

A BAP20 token must implement the interface IBEP20 in IBAP20.sol. This is a template contract BAP20Token.template. Users just need to fill in _name, _symbol, _decimals and _totalSupply according to their own requirements:

```
  constructor() public {
    _name = {{TOKEN_NAME}};
    _symbol = {{TOKEN_SYMBOL}};
    _decimals = {{DECIMALS}};
    _totalSupply = {{TOTAL_SUPPLY}};
    _balances[msg.sender] = _totalSupply;

    emit Transfer(address(0), msg.sender, _totalSupply);
  }
```

Then users can use Remix IDE  to compile and deploy the BAP20 contract to BMC.


