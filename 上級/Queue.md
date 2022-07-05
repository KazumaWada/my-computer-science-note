# Queue

- stuck のように、head に要素が追加される。(Enqueue)(人が列の最後尾に並ぶイメージ)-> 末尾の要素が押し出されて実行される。(Dequeue)(先頭の人にお店に入っていい順番が回ってきた時)
- リストの末尾に要素を挿入する関数 o(1)
- リストの先頭を取得して削除する関数 o(1)

## 片方向リストを使って、queue のデータ構造を実装していく。

```java
// ここから開発しましょう。
class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
        this.next = null;
    }
}

class Queue{
    public Node head;
    public Node tail;

    public Queue(){
        this.head = null;
        this.tail = null;
    }

   //先頭
    public Integer peekFront(){
        if(this.head == null) return null;
        return this.head.data;
    }
    //末尾
    public Integer peekBack(){
        if(this.tail == null) return this.peekFront();
        return this.tail.data;
    }
    //リストの末尾に要素を挿入する関数
    public void enqueue(int data){
        //先頭がなかったら(一番下)
        if(this.head == null){
            this.head = new Node(data);
        }
        //末尾がなかったら(一番上)
        else if(this.tail == null){
            this.tail = new Node(data);
            this.head.next = this.tail;
        }
        else{
            ////Dequeue////
            ////末尾に要素を挿入/////
            this.tail.next = new Node(data);
            this.tail = this.tail.next;
        }
    }
    //リストの先頭を取得して削除する関数
    public Integer dequeue(){
        if(this.head == null) return null;
        Node temp = this.head;

        if(this.head.next == null){
            this.head = null;
            this.tail = null;
        }
        //this.head.nextはどんな時でも必ずnullだよね??末尾なんだから。。
        //ってことで、headにnullを格納しているのか。
        else this.head = this.head.next;

        return temp.data;
    }
}
class Main{
    public static void main(String[] args){
        Queue q = new Queue();
        System.out.println(q.peekFront());//null
        System.out.println(q.peekBack());//null

        q.enqueue(4);//
        System.out.println(q.peekFront());//4
        System.out.println(q.peekBack());//4

        q.enqueue(50);//
        System.out.println(q.peekFront());//4
        System.out.println(q.peekBack());//50

        q.enqueue(64);
        System.out.println(q.peekFront());//4
        System.out.println(q.peekBack());//64

        System.out.println("dequeued :" + q.dequeue());//dequeued :4
        System.out.println(q.peekFront());//50
        System.out.println(q.peekBack());//64

    }
}
```

# Deque(両端 queue)

- 両方から挿入、削除ができる queue
  EnqueueFront
  EnqueueBack
  DequeueFront
  DequeueBack
- 双方向リストを使って(prev)、計算量を少なくする。

```java
// - push: 頂上に挿入
// - peek: 頂上にある物を読み取る
// - pop: 頂上にある要素を取り出す

//双方向リスト
class Node{
    public int data;
    public Node prev;
    public Node next;

    public Node(int data){
        this.data = data;
    }
}

//queue
class Deque{
    public Node head;
    public Node tail;

    public Deque{
        this.head = null;
        this.tail = null;
    }

    //先頭のデータを読み取る
    public Integer peekFront(){
        if(this.head == null)return null;
        return this.head.data;
    }

    public Integer peekBack(){
        if(this.head == null) return null;
        return this.tail.data;
    }

    //先頭に挿入
    public void enqueueFront(int data){
        //先頭が空だったら新しく作る
        if(this.head == null){
            this.head = new Node(data);
            this.tail = this.head;
        }
        //先頭にNodeがあったら、
        else{
            Node node = new Node(data);
            this.head.prev = node;
            node.next = this.head;
            //ここの動作がいまいちわからん
            this.head = node;
        }
    }

    //末尾に追加
    public void enqueueBack(int data){
        if(this.head == null){
            this.head = new Node(data);
            this.tail = this.head;
        }
        else{
            Node node = new Node(data);
            this.tail.next = node;
            node.prev = this.tail;
            //ここの動作がいまいちわからん
            this.tail = node;
        }
    }

    //先頭を削除
    public Integer dequeueFront(){
        if(this.head == null)return null;

        Node temp = this.head;
        this.head = this.head.next;
        if(this.head != null) this.head.prev = null;
        else this.tail = null;
        return temp.data;
    }

    //末尾を削除
    public Integer dequeueBack(){
        if(this.tail == null) return null;

        Node temp = this.tail;
        this.tail = this.tail.prev;

        if(this.tail != null) this.tail.next = null;
        else this.head = null;
        return temp.data;
    }
}
```

- queue を使って、リストの最大値を求める。

```java
//繰り返し処理で先頭に最大値を置いて行く
class Main{
    public static int getMax(int[] arr){
        Deque deque = new Deque();//上の段のコード全てがDequeの関数
        // 最初の要素を両端キューの最初に追加します。
        deque.enqueueFront(arr[0]);

        // 最大値は両端キューの先頭へ、その他の値は末尾へ向かいます。
        for(int i = 1; i < arr.length; i++){
            if(arr[i] > deque.peekFront()) deque.enqueueFront(arr[i]);
            else deque.enqueueBack(arr[i]);
        }

        return deque.peekFront();
    }

    public static void main(String[] args){
        int[] arr = new int[]{34,35,64,34,10,2,14,5,353,23,35,63,23};

        //353
        System.out.println(getMax(arr));
    }
}
```

## 応用

- サイズ 3 の整数たちの中で最大値を求める。(sliding window)

入力: [1, 2, 3, 1, 4, 5, 2, 3, 6], K = 3
出力: 3, 3, 4, 5, 5, 5, 6

1, 2, 3 の最大値は 3 です。
2, 3, 1 の最大値は 3 です。
3, 1, 4 の最大値は 4 です。
1, 4, 5 の最大値は 5 です。
4, 5, 2 の最大値は 5 です。
5, 2, 3 の最大値は 5 です。
2, 3, 6 の最大値は 6 です。

- queue を使わないと、o(n\*k)の計算量がかかってしまう。両端 queue を使うと、o(n)で解決することができる。

- sliding window とは?
  上の例文を用いて説明すると、
  スライドして出た新しい値より既存の小さい値は、全て削除することができる。
  右にスライドして行った場合、
  左にある値は、常に現在の最大値であることがわかる。

```java
class Main{

    public static ArrayList<Integer> getMaxWindows(int[] arr, int k){
        ArrayList<Integer> results = new ArrayList<>();
        if(k > arr.length) return results;

        Deque deque = new Deque();

        // dequeの初期化
        for (int i=0; i < k; i++){
            // 新しい値と既存の値を比較して、新しい値以下は全て削除するので、dequeの末尾は新しい値より大きい値になります。
            // dequeの先頭は最大値です。(新しい値より大きいので削除されないから。)
            while(deque.peekBack() != null && arr[deque.peekBack()] <= arr[i]){
                deque.dequeueBack();
            }
            deque.enqueueBack(i);

        }

        for(int i=k; i < arr.length; i++){
            // dequeの先頭は最大値
            results.add(arr[deque.peekFront()]);

            // ウィンドウ外にある要素は取り除きます。
            while(deque.peekFront() != null && deque.peekFront() <= i-k) deque.dequeueFront();
            // 現在の値とそれより小さい全てのdequeの値をチェック
            while(deque.peekBack() != null && arr[deque.peekBack()] <= arr[i]) deque.dequeueBack();
            deque.enqueueBack(i);
        }

        // 最後のmax
        results.add(arr[deque.peekFront()]);
        return results;
    }

    public static void main(String[] args){

        // [64, 64, 64, 34, 14, 353, 353, 353, 353, 63]
        int[] arr = new int[]{34,35,64,34,10,2,14,5,353,23,35,63,23};
        System.out.println(getMaxWindows(arr,4));

    }
}

class Main{
    public static ArrayList<Integer> getMaxWindows(int[] arr, int k){
        ArrayList<Integer> results = new ArrayList<>();
        //そもそもk個以上の要素がなかったら、
        if(k > arr.length) return results;
        Deque deque new Deque();

        //dequeueの初期化
        //k個分のブロックを繰り返す。
        for(int i=0; i<k; i++){
                 //末尾のデータが存在 && iの要素が末尾の数字より大きい
            while(deque.peekBack() != null && arr[deque.peekBack])
            //末尾の要素(deque.peekBack)は削除される。
            deque.dequeueBack();
        }
        //↑上の関数によって、一つだけの要素(最大値)が残る。
        //↓
        deque.enqueueBack(i);
    }

   //最大値から繰り返すって事?
    for(int i=k; i<arr.length; i++){
        results.add(arr[deque])
    }
}
```
