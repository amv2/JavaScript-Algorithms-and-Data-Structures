# Cash Register

### Problem Description
Design a cash register drawer function checkCashRegister() that accepts purchase price as the first argument (price), payment as the second argument (cash), and cash-in-drawer (cid) as the third argument.

cid is a 2D array listing available currency.

The checkCashRegister() function should always return an object with a status key and a change key.

Return {status: "INSUFFICIENT_FUNDS", change: []} if cash-in-drawer is less than the change due, or if you cannot return the exact change.

Return {status: "CLOSED", change: [...]} with cash-in-drawer as the value for the key change if it is equal to the change due.

Otherwise, return {status: "OPEN", change: [...]}, with the change due in coins and bills, sorted in highest to lowest order, as the value of the change key.

          Currency Unit  | Amount
          -------------  | -------------
            Penny        | $0.01 (PENNY)
            Nickel       | $0.05 (NICKEL)
            Dime         | $0.10 (DIME)
            Quarter      | $0.25 (QUARTER)
            Dollar       | $1.00 (ONE)
          Five Dollars   | $5.00 (FIVE)
           Ten Dollars   | $10.00 (TEN)
          Twenty Dollars | $20.00 (TWENTY)
     One-hundred Dollars | $100.00 (ONE HUNDRED)


See below for an example of a cash-in-drawer array:

```javascript
[
  ["PENNY", 1.01],
  ["NICKEL", 2.05],
  ["DIME", 3.1],
  ["QUARTER", 4.25],
  ["ONE", 90],
  ["FIVE", 55],
  ["TEN", 20],
  ["TWENTY", 60],
  ["ONE HUNDRED", 100]
]
```

### Solution
```js
function checkCashRegister(price, cash, cid) {
  let change = cash - price;
  let sum = 0, remainder = [];
  for (let key in cid) sum += cid[key][1];
  if (sum == change) return {status: "CLOSED", change: cid};
  if (sum < cash) return {status: "INSUFFICIENT_FUNDS", change: []};

  let bills = [100, 20, 10, 5, 1, 0.25, 0.10, 0.05, 0.01];
  cid = cid.reverse();
  remainder = [['ONE HUNDRED', 0 ], ['TWENTY', 0 ], ['TEN', 0 ], ['FIVE', 0 ], ['ONE', 0], ['QUARTER', 0 ], ['DIME', 0 ], ['NICKEL', 0 ], ['PENNY', 0 ]];
  for (let i=0; i<bills.length; i++) {
    while(change - bills[i] >= -0.001 && cid[i][1] >= bills[i]) {
      change -= bills[i];
      cid[i][1] -= bills[i];
      remainder[i][1] += bills[i];
    }
  }
  remainder = remainder.filter(value => value[1] != 0);
  return {status: "OPEN", change: remainder};
}

checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]);
checkCashRegister(19.5, 20, [["PENNY", 0.01], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]);
checkCashRegister(19.5, 20, [["PENNY", 0.5], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]);
```
