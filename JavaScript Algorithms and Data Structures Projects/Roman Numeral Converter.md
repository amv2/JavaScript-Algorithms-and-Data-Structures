# Roman Numeral Converter

### Problem Description
Convert the given number into a roman numeral.

All roman numerals answers should be provided in upper-case.

### Solution  


```javascript
const digitsa = ['','M', 'MM', 'MMM'];
const digitsb = ['','C', 'CC', 'CCC', 'CD', 'D', 'DC', 'DCC', 'DCCC', 'CM'];
const digitsc = ['','X', 'XX', 'XXX', 'XL', 'L', 'LX', 'LXX', 'LXXX', 'XC'];
const digitsd = ['','I', 'II', 'III', 'IV', 'V', 'VI', 'VII', 'VIII', 'IX'];

function digitConverter(digit, arr) {
  return arr[parseInt(digit)];
}

function convertToRoman(num) {
  num = num.toString().split('');
  let size = num.length;
  if(size == 4) return digitConverter(num[0], digitsa) +
    digitConverter(num[1], digitsb) +
    digitConverter(num[2], digitsc) +
    digitConverter(num[3], digitsd);
  if(size == 3) return digitConverter(num[0], digitsb) +
    digitConverter(num[1], digitsc) +
    digitConverter(num[2], digitsd);
  if(size == 2) return digitConverter(num[0], digitsc) +
    digitConverter(num[1], digitsd);
  if(size == 1) return digitConverter(num[0], digitsd);
}

convertToRoman(36);
```
