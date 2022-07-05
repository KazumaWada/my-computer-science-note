# tree

- グラフ、頂点(または Node), 辺(2 つの要素間の関係. [頂点 1,頂点 2]と表される。)
- parents と child の関係にある階層を表現するのに便利

![](/上級/img01.png)

## Graph

- 頂点と辺を持つ構造体
- directed graph(向きを持つ辺)と undirected graph(ただ繋がっている)がある。
- x∈S

# tree and forest

## tree

- 非環状無向グラフ(全て繋がっている(閉路を持つ) + 全てを一度だけ連結される。)

## forest

- 閉路を持たない(繋がっていない)木.(木が複数あるが、繋がってはいない。) == 連結な森は木となる。

- 二つの node に上下関係がある場合、親に当たる node を根ノード(root)という。そして、root がある tree を根付き木(binary tree?多分。)と呼ぶ(先祖、子孫関係が成り立つ)
- root があるという事は、木構造の始まりを意味する。
- 共通の親を持つ全ての node は兄弟と呼ばれる。
- その node に子がない(一番下の node)は、leaf node(葉ノード)と呼ばれる。

## 木の高さ heigh

- ある node から、根 node への辺の最大個数

## 木の深さ depth

- 高さとは逆で、ある node から、葉 node までの辺の数。根 node はいつも深さ 0. 深さ == level

## binary tree(二分木)

- sort,search が実装できる。
- node が持つ子が最大で 2 つであるものを指す。

```javascript
class BinaryTree {
  constructor(data) {
    this.data = data;
    // 左二分木
    this.left = null;
    // 右二分木
    this.right = null;
  }
}

class BinaryTree {
  constroctor(data) {
    this.data = data;
    this.left = null;
    this.right = null;
  }
}

let binaryTree = new BinaryTree(1);
let node2 = new BinaryTree(2);
let node3 = new BinaryTree(3);

binaryTree.left = node2;
binaryTree.right = node3;

console.log("Root: " + binaryTree.data);
console.log("Left: " + binaryTree.left.data);
console.log("Right: " + binaryTree.right.data);
// Root: 1
// Left: 2
// Right: 3
```

- full binary tree: 全ての tree が 2 つの子を持っている木。
- perfect binary tree: full binary tree かつ宇部手の葉ノードが同じ深さを持つ木。
- complete binary tree: 最下層を除いた、全ての深さが、Node で満たされ(2 つ持ってるてことかな)、最下層の葉 Node が可能な限り左に寄せられているような木。bainary tree が最大容量であることを示している。

## complete binary tree

- 葉の数 = 葉以外の node の数 - 1;
