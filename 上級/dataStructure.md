# Data Structure

data structure

- list[]
- linked list

## 連結リスト(メモリアドレスが等しく連続していないリスト。pointer で繋がっている。)

- メモリ上のリストを表現することができる.
- list で言う array[0]は、連結リストでは node と呼ぶ。
- node と辺で出来ている。
- node の pointer を辿っていけば、欲しい情報がある node にたどり着く。

リストとは違い、データが連続したメモリに保存されないデータ構造。つまり、for,index でとってくることができないって事かな？

![](/上級//FireShot Capture 269 - Recursion - コンピュータサイエンスを基礎から学べるプラットフォーム - recursionist.io.png)

> 連結リストはポインタによってデータどうしがリンクされているシーケンスを持つデータ構造です。したがって、配列のときのようにデータは連続したメモリには格納されません。

list: adress が連続している配列
連結 list:pointar で data 同士がリンクされているので、連続してメモリに保存されているわけではない。メモリ上のリストを表現できる。

- 連結リストの各要素は node と呼ばれる。node は object である。
- グラフ理論と一緒に使われることがある。枝のように node と次の node が繋がっている。つまり、node が次の node と繋がっている。従って、リンクを辿るだけで、nodeX から nodeY へと移動づることができる。

### 連結リストの中の singly linked list という種類のリスト

- 最も単純な連結リスト. node = そのメモリに入る data + 次の node がどこなのかを示す Next(= pointer))の 2 つが object によって表現されている。node は object なので、次の node を示すコードは、メモリアドレスである事に注意。
  ↓
  pointer は、node 内の関数に書かれているため、メモリアドレスを参照している。
- 先頭は、インデックスの 0 ではない可能性もある。
- 末尾は pointer に null を当てる。

```java
class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
    }
}

class SinglyLinkedList{
    public Node head;
    public SinglyLinkedList(Node head){
        this.head = head;
    }
}

class Main{
    public static void main(String[] args){
    Node node1 = new Node(4);
    Node node2 = new Node(65);
    Node node3 = new Node(24);

    SinglyLinkedList numList = new SinglyLinkedList(node1);
    }

}
```

```java
class Node {
    public int data;
    public Node next;

    public Node(int data) {
        this.data = data;
        // nextを割り当てないでください。オブジェクト変数はヒープアドレスへの参照を保持するだけで、アクセス演算子「.」を使ってデータにアクセスします。オブジェクトが何も代入されていない場合は、何も指していないのでnullを保持します。
    }
}

// 先頭のノードを保持するコンテナで、リスト自体を表します。
class SinglyLinkedList{
    public Node head;

    public SinglyLinkedList(Node head){
        this.head = head;
    }
}

class Main{
    public static void main(String[] args){
        // 3つのノードを作成します。
        Node node1 = new Node(4);
        Node node2 = new Node(65);
        Node node3 = new Node(24);

        SinglyLinkedList numList = new SinglyLinkedList(node1);

        // リストに他のリストを追加します。
        // nodeはオブジェクトなので、=は値ではなく、メモリアドレスを指している点に注意してください。
        numList.head.next = node2;
        numList.head.next.next = node3;

        // 連結リストを反復します。
        // 反復によって、現在のノードは次のノードになります。この処理を最後のノードまで繰り返します。
        Node currentNode = numList.head;
        while(currentNode != null){
            // 現在のノードを出力します。
            System.out.println(currentNode.data);
            currentNode = currentNode.next;
        }
    }
}
```

```java
class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
    }
}

class SinglyLinkedList{
    public Node head;

    public SinglyLinkedList(Node head){
        this.head = head;
    }
}

class Main{
    public static void main(String[] args){

        int[] arr = new int[]{35,23,546,67,86,234,56,767,34,1,98,78,555};

        SinglyLinkedList numlist = new SinglyLinkedList(new Node(arr[0]));

        Node currentNode = numlist.head;
        for(int i = 1; i < arr.length; i++) {
            currentNode.next = new Node(arr[i]);
            currentNode = currentNode.next;
        }

        currentNode = numlist.head;
        while(currentNode != null){
            System.out.println(currentNode.data);
            currentNode = currentNode.next;
        }

    }
}
```

## 片方向リスト

- 行える操作(index, 挿入, 削除)

### index

配列は、O(1)でアクセスできるが、片方向リストは、O(n)かかってしまう。取得したい要素まで、pointer を辿る必要がある。

連結リストから index を探すコード。
このコードを見ていて思ったけど、リストは全て繋がって一つだけど、連結リストは全て散らばっていて pointer で繋がっているってことかな??

```java
class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
    }
}

class SinglyLinkedList{
    // 配列が渡されるようにします。片方向リストの初期化を行います。
    public Node head;

    public SinglyLinkedList(int[] arr){
        // 連結リストは先頭が必要です。もし配列に要素が存在しなれば、nullを初期値とします。
        this.head = arr.length > 0 ? new Node(arr[0]) : null;

        Node currentNode = this.head;
        System.out.print("[ ");
        System.out.print(currentNode.data + " ");
        for(int i = 1; i < arr.length; i++){
            currentNode.next = new Node(arr[i]);
            currentNode = currentNode.next;
            System.out.print(currentNode.data + " ");
        }
        System.out.println("]");
    }

    public Node at(int index){
        Node iterator = this.head;
        // 与えられたインデックスまでリストの中を反復します。
        // nullになったところは反復の範囲外になります。
        for(int i = 0; i < index; i++){
            // もしnextがnullの場合、nullを返します。これはインデックスが範囲外にあることを示します。
            iterator = iterator.next;
            if(iterator == null) return null;
        }
        return iterator;
    }
}

class Main{
    public static void main(String[] args){
        int[] arr = new int[]{35,23,546,67,86,234,56,767,34,1,98,78,555};
        SinglyLinkedList numList = new SinglyLinkedList(arr);
        // 連結リストを反復します。
        System.out.println(numList.at(2).data);
        System.out.println(numList.at(12).data);

        // System.out.println(numList.at(13).data); // a(13)はnullを返すので、エラーになります。
    }
}
```

### insert

- 配列は、サイズが固定されているため、新しく増やそうとしたら、また新たに配列を作成することが必要。o(n)
- 連結リストは、前後の pointer の先を変更するだけで insert することができる。o(1)

```java
class SinglyLinkedListNode<E>{
    public E data;
    public SinglyLinkedListNode<E> next;

    public SinglyLinkedListNode(E data){
        this.data = data;
        this.next = null;
    }
}

class Solution{
    public static SinglyLinkedListNode<Integer> insertAtPosition(SinglyLinkedListNode<Integer> head, int position, int data){
        // 関数を完成させてください
        SinglyLinkedListNode<Integer> currentNode = head;
        for(int i = 0; i < position; i++){
          if(currentNode.next == null) return head;
          currentNode = currentNode.next;
        }
        SinglyLinkedListNode<Integer> newData = new SinglyLinkedListNode(data);
        newData.next = currentNode.next;//アドレス指定
        currentNode.next = newData;
        return head;
    }
}

```

```java
class SinglyLinkedListNode<E>{
    public E data;
    public SinglyLinkedListNode<E> next;

    public SinglyLinkedListNode(E data){
        this.data = data;
        this.next = null;
    }
}

class Solution{
    public static SinglyLinkedListNode<Integer> insertNodeInSorted(SinglyLinkedListNode<Integer> head, int data){
        // ダミーのノードを作ります。dataは仮にintの最小値MIN_VALUEを入れておきます。
        //MAX_VALUE: intが格納できる最大の値(2147483647).だから、最小は0とか1とかかな??
        //値から最小のものを探すのではなく、intが持てる最小の値を格納する。
        SinglyLinkedListNode<Integer> dummyNode = new SinglyLinkedListNode<Integer>(Integer.MIN_VALUE);
        // ダミーノードをhead の前に挿入します。
        dummyNode.next = head;

        SinglyLinkedListNode<Integer> currentNode = dummyNode;

        // 挿入すべき位置までリストを走査します。
        //ifを使わなくても、while内で一行で書ける。
        while (currentNode.next != null && currentNode.next.data < data) {
            currentNode = currentNode.next;
        }

        // 新しいノードを作ります。
        SinglyLinkedListNode<Integer> node = new SinglyLinkedListNode<Integer>(data);
        // currentNode.nextをtempに入れ保管します。
        SinglyLinkedListNode<Integer> temp = currentNode.next;
        // currentNode.nextには新しいノードを入れます。
        currentNode.next = node;
        // tempに入れていた参照を新しいノードのnextにします。
        node.next = temp;

        // ダミーの次のノードから返します。
        return dummyNode.next;
    }
}
```

### delete

片方向リストでは、削除したい要素の前の要素になるまで、o(n)で計算していく必要がある。

```java
//setup
class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
    }

   //次のNode
    public void addNextNode(Node newNode){
        Node tempNode = this.next;
        this.next = newNode;
        newNode.next = tempNode;
    }
}

class SinglyLinkedList{
    public Node head;

    public SinglyLinkedList(int[] arr){
        this.head = arr.length > 0? new Node(arr[0]) : null;

        Node currentNode = this.head;
        for(int i=1; i < arr.length; i++){
            currentNode.next = new Node(arr[i]);
            currentNode = currentNode.next;
        }
    }

    public Node at(int index){
        Node iterator = this.head;
        for(int i = 0; i < index; i++){
            iterator = iterator.next;
            if(iterator == null) return null;
        }
        return iterator;
    }

    public void preappend(Node newNode){
        newNode.next = this.head;
        this.head = newNode;
    }

    // リストの先頭の要素をポップします。O(1)
    public void popFront(){
        this.head = this.head.next;
    }

    public void delete(int index){
        if (index == 0){
            this.popFront();
            return;
        }
        Node iterator = this.head;
        // 目的のデータの手前のインデックスまで、リストの中を反復します。
        for(int i = 0; i < index-1; i++){
            // もし、次のノードがなかった場合、処理を中断します。
            if(iterator.next == null) return;
            iterator = iterator.next;
        }
        // iterator（削除したい要素の1つ前）, 削除したい要素(A), その次の要素(B)
        // iteratorのポインタをAではなくBに変更します。
        iterator.next = iterator.next.next;
    }

    public void printList(){
        Node iterator = this.head;
        String str = "";
        while(iterator != null){
            str += iterator.data + " ";
            iterator = iterator.next;
        }
        System.out.println(str);
    }
}

class Main{

    public static void main(String[] args){

        int[] arr = new int[]{35,23,546,67,86,234,56,767,34,1,98,78,555};
        SinglyLinkedList numList = new SinglyLinkedList(arr);

        numList.printList();

        System.out.println("popFront");
        numList.popFront();
        System.out.println("popFront");
        numList.popFront();
        numList.printList();

        System.out.println("delete index:4");
        numList.delete(4);
        numList.printList();

        System.out.println("delete index: 9");
        numList.delete(9);
        numList.printList();
    }
}
```

- リストを逆順にする。

```java
class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
    }

    public void addNextNode(Node newNode){
        Node tempNode = this.next;
        this.next = newNode;
        newNode.next = tempNode;
    }
}

class SinglyLinkedList{
    public Node head;

    public SinglyLinkedList(int[] arr){
        this.head = arr.length > 0? new Node(arr[0]) : null;

        Node currentNode = this.head;
        for(int i=1; i < arr.length; i++){
            currentNode.next = new Node(arr[i]);
            currentNode = currentNode.next;
        }
    }

    public Node at(int index){
        Node iterator = this.head;
        for(int i=1; i < index; i++){
            iterator = iterator.next;
            if(iterator == null) return null;
        }
        return iterator;
    }

    public void preappend(Node newNode){
        newNode.next = this.head;
        this.head = newNode;
    }

    public void popFront(){
        this.head = this.head.next;
    }

    public void delete(int index){
        if (index == 0) this.popFront();
        Node iterator = this.head;
        for(int i = 0; i < index-1; i++){
            if(iterator.next == null) return;
            iterator = iterator.next;
        }
        iterator.next = iterator.next.next;
    }

    public void reverse(){
        if(this.head == null || this.head.next == null) return;

        // オブジェクトなので、=は実際の値を格納しているわけではなく、メモリアドレスを指している点に十分注意ください。
        // A -> B -> C を、C -> B -> Aに変更する場合は、向きに少し混乱するのでゆっくり解読しましょう。

        //末尾がnullだったのを、先頭をnullにする。
        Node reverse = this.head;
        this.head = this.head.next;
        reverse.next = null;

        while(this.head != null){
            // =はメモリアドレスを指します。紙に書いてロジックを確認しましょう。
            Node temp = this.head;
            this.head = this.head.next;
            temp.next = reverse;
            reverse = temp;
        }
        // 処理が終わったら、headのnextを反転したリストを含むtempHeadに割り当てましょう。
        this.head = reverse;
    }

    public void printList(){
        Node iterator = this.head;
        String str = "";
        while(iterator != null){
            str += iterator.data + " ";
            iterator = iterator.next;
        }
        System.out.println(str);
    }
}

class Main{

    public static void main(String[] args){

        int[] arr = new int[]{35,23,546,67,86,234,56,767,34,1,98,78,555};
        SinglyLinkedList numList = new SinglyLinkedList(arr);

        numList.printList();
        numList.reverse();
        numList.printList();
    }
}
```

## doubly linked list

- 次の pointer に加えて、前の pointer も持つ連結リスト。

```java
class Node{
    // 前後を追跡します。
    public int data;
    public Node prev;
    public Node next;

    public Node(int data){
        this.data = data;
    }
}

// リストは少なくとも1つのノードを持っている必要があります。
// ヌルリストをサポートしたい場合は、それに応じてコードを追加してください。
class DoublyLinkedList{
    public Node head;
    public Node tail;

    public DoublyLinkedList(int[] arr){
        // 今回は末尾を追跡します。
        if(arr.length <= 0){
            this.head = null;
            this.tail = this.head;
            return;
        }

        this.head = new Node(arr[0]);
        Node currentNode = this.head;
        for(int i=1; i < arr.length; i++){
            currentNode.next = new Node(arr[i]);
            // 次のノードの前のノードをcurrent Nodeに割り当てます。
            currentNode.next.prev = currentNode;
            currentNode = currentNode.next;
        }
        // このcurrent Nodeは最後のnodeです。
        this.tail = currentNode;
    }

    public void printList(){
        Node iterator = this.head;
        String str = "";
        while(iterator != null){
            str += iterator.data + " ";
            iterator = iterator.next;
        }
        System.out.println("[" + str + "]");
    }
}

class Main{
    public static void main(String[] args){
        int[] arr = new int[]{35,23,546,67,86,234,56,767,34,1,98,78,555};
        DoublyLinkedList numList = new DoublyLinkedList(arr);

        numList.printList();//[35 23 546 67 86 234 56 767 34 1 98 78 555 ]
        System.out.println(numList.head.data);//35
        System.out.println(numList.head.next.data);//23
        System.out.println(numList.head.next.prev.data);//35
        System.out.println(numList.tail.data);//555
        System.out.println(numList.tail.prev.data);//78

    }
}
```

### index

- singly linked list の時と同じで、線形探索(o(n))を行います。

```java
class Node{
    public int data;
    public Node prev;
    public Node next;

    public Node(int data){
        this.data = data;
    }
}

class DoublyLinkedList{
    public Node head;
    public Node tail;

    public DoublyLinkedList(int[] arr){
        if(arr.length <= 0){
            this.head = null;
            this.tail = this.head;
            return;
        }

        this.head = new Node(arr[0]);
        Node currentNode = this.head;
        for(int i=1; i < arr.length; i++){
            currentNode.next = new Node(arr[i]);
            currentNode.next.prev = currentNode;
            currentNode = currentNode.next;
        }
        this.tail = currentNode;
    }

    public Node at(int index){
        Node iterator = this.head;
        // 片方向リストと同じ処理
        for(int i=0; i < index; i++){
            iterator = iterator.next;
            if(iterator == null) return null;
        }
        return iterator;
    }

    public void printList(){
        Node iterator = this.head;
        String str = "";
        while(iterator != null){
            str += iterator.data + " ";
            iterator = iterator.next;
        }
        System.out.println("[" + str + "]");
    }
}

class Main{
    public static void main(String[] args){
        int[] arr = new int[]{35,23,546,67,86,234,56,767,34,1,98,78,555};
        DoublyLinkedList numList = new DoublyLinkedList(arr);

        numList.printList();
        System.out.println(numList.at(0).data);
        System.out.println(numList.at(2).data);
        System.out.println(numList.at(12).data);

    }
}
```

- 逆表示

```java
class Node{
    public int data;
    public Node prev;
    public Node next;

    public Node(int data){
        this.data = data;
    }
}

class DoublyLinkedList{
    public Node head;
    public Node tail;

    public DoublyLinkedList(int[] arr){
        if(arr.length <= 0){
            this.head = null;
            this.tail = this.head;
            return;
        }

        this.head = new Node(arr[0]);
        Node currentNode = this.head;
        for(int i=1; i < arr.length; i++){
            currentNode.next = new Node(arr[i]);
            currentNode.next.prev = currentNode;
            currentNode = currentNode.next;
        }
        this.tail = currentNode;
    }

    public Node at(int index){
        Node iterator = this.head;
        for(int i=0; i < index; i++){
            iterator = iterator.next;
            if(iterator == null) return null;
        }
        return iterator;
    }

    public void reverse(){
        Node reverse = this.tail;
        Node iterator = this.tail.prev;

        Node currentNode = reverse;
        while(iterator != null){
            currentNode.next = iterator;

            iterator = iterator.prev;
            if(iterator != null) iterator.next = null;

            currentNode.next.prev = currentNode;
            currentNode = currentNode.next;

        }
        this.tail = currentNode;
        this.head = reverse;
        this.head.prev = null;
    }

    public void printInReverse(){
        String str = "";
        Node iterator = this.tail;
        while(iterator != null){
            str += iterator.data + " ";
            iterator = iterator.prev;
        }
        System.out.println("[" + str + "]");
    }

    public void printList(){
        Node iterator = this.head;
        String str = "";
        while(iterator != null){
            str += iterator.data + " ";
            iterator = iterator.next;
        }
        System.out.println("[" + str + "]");
    }
}

class Main{
    public static void main(String[] args){
        int[] arr = new int[]{35,23,546,67,86,234,56,767,34,1,98,78,555};
        DoublyLinkedList numList = new DoublyLinkedList(arr);

        numList.printList();
        numList.printInReverse();

        numList.printList();
        numList.reverse();
        numList.printList();
        numList.printInReverse();
    }
}
```
