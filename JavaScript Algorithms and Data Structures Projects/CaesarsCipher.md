# Caesars Cipher

### Problem Description
One of the simplest and most widely known ciphers is a Caesar cipher, also known as a shift cipher. In a shift cipher the meanings of the letters are shifted by some set amount.

A common modern use is the ROT13 cipher, where the values of the letters are shifted by 13 places. Thus A ↔ N, B ↔ O and so on.

Write a function which takes a ROT13 encoded string as input and returns a decoded string.

All letters will be uppercase. Do not transform any non-alphabetic character (i.e. spaces, punctuation), but do pass them on.


### Solution
'''javascript
function rot13(str) {
  let alphabet = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'];
  str = str.split('');
  for (let i=0; i<str.length; i++) {
    if (alphabet.includes(str[i])) {
      let index = alphabet.indexOf(str[i]);
      if(index < 13) str[i] = alphabet[index+13];
      else str[i] = alphabet[index-13];
    }
  }
  return str.join('');
}

rot13("SERR PBQR PNZC");
'''
