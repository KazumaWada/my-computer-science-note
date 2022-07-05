- ? :を使えば、関数を使わずに、変数として保存できるから、for の i に使えた。

```javascript
function generateAlphabet(firstAlphabet, secondAlphabet) {
  // // 関数を完成させてください(乗車駅、降車駅)
  // let firstChar = firstAlphabet.toLowerCase().charCodeAt(0);
  // let secondChar = secondAlphabet.toLowerCase().charCodeAt(0);

  let charCloseToTheA = firstChar < secondChar ? firstChar : secondChar;
  let biggerChar = firstChar < secondChar ? secondChar : firstChar;

  let stations = [];

  if (firstAlphabet !== secondAlphabet) {
    for (let i = charCloseToTheA; i <= biggerChar; i++) {
      stations.push(String.fromCharCode(i));
    }
  } else if (firstAlphabet == secondAlphabet) {
    stations.push(firstAlphabet);
  }
  return stations;
}
```

- 次の配列の値が、前より小さかったら、false が true に変わって break によって出力され、処理がそこで終了する。

```javascript
function hasPenalty(records) {
  let found = false;
  for (let i = 1; i < records.length + 1; i++) {
    if (records[i - 1] > records[i]) {
      found = true;
      break;
    }
  }
  console.log(found);
  return found;
}
```

- ハッシュマップの値の取得方法

```javascript
// hashmapの値のみを取得するにはObject.value()を使います。
// スプレッド構文「...」を使って要素を展開し、最大値と最小値を取得します。
// 最大値と最小値が同じならtrueです。
return (
  Math.max(...Object.values(hashmap)) == Math.min(...Object.values(hashmap))
);
```

- let in statement

```javascript
// 値が 2 の時にキーを res へ push します。
for (let key in hashmap) {
  if (hashmap[key] == 2) res.push(parseInt(key));
}
```

- for(let hgoe of something)
  c,value は、なんでもいい。s が 3 だった場合、c は 0,1,2,3 に変化する。

```javascript
for (let c of s) {
  if (hashmap[c] == undefined) hashmap[c] = 1;
  else hashmap[c] += 1;
}
//または、
const iterable = [10, 20, 30];

for (const value of iterable) {
  console.log(value);
}
// 10
// 20
// 30
```
