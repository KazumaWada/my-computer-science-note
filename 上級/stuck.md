# how to described stuck's lits

そもそも stuck は再帰の時にやったように、頂上に stuck して、一番最初に取り出されるものも頂上からだった。

- push: 頂上に挿入
- peek: 頂上にある物を読み取る
- pop: 頂上にある要素を取り出す
  > push、peek、pop の 3 つを見てわかる通り、スタックの頂上の要素だけが自由に読み書きできます。

```java
class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
        this.next = null;
    }
}

class Stack {
    public Node head;

    public Stack(){
        this.head = null;
    }


    //push: 頂上に挿入
    public void push(int data){
        //今のheadをtempに格納。
        Node temp = this.head;
        //newを先頭に持ってくる
        this.head = new Node(data);
        newの矢印をかつてheadだった値につなぐ。
        this.head.next = temp;//Node(data)&&head -> temp
    }

    //pop:頂上にある要素を取り出す
    public Integer pop(){
        if(this.head == null) return null;
        Node temp = this.head;
        this.head = this.head.next;
        return temp.data;
    }
//////////////////////////////////////////////////////////
    public Integer peek(){
        if (this.head == null) return null;
        return this.head.data;
    }
//////////////////////////////////////////////////////////
}





}



class Main{

    public static void main(String[] args){

        Stack stack = new Stack();
        stack.push(2);//頂上に挿入
        System.out.println(stack.peek());//頂上の値を読み取る。

        stack.push(4);
        stack.push(3);
        stack.push(1);
        stack.pop();//1
        System.out.println(stack.peek());//3
    }
}
```

- 配列を受け取って、その逆を返す。

```java
//[1 2 3 4 5 6 ]
//[6 5 4 3 2 1 ]
class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
        this.next = null;
    }
}

class Stack {
    public Node head;

    public Stack(){
        this.head = null;
    }

    public void push(int data){
        Node temp = this.head;
        this.head = new Node(data);
        this.head.next = temp;
    }

    public Integer pop(){
        if (this.head == null) return null;
        Node temp = this.head;
        this.head = this.head.next;
        return temp.data;
    }

    public Integer peek(){
        if (this.head == null) return null;
        return this.head.data;
    }
}

class Main{

    public static int[] reverse(int[] arr){
        Stack stack = new Stack();
        //配列をpushしていく。
        for (int i = 0; i < arr.length; i++) stack.push(arr[i]);
        //新しい配列の要素を作ったのかな??全部でlength+1だから、その次はlengthみたいな??
        //それともjava特有の書き方で、配列を新しく作るときにその配列の個数を入力したのかな。
        int[] reversed = new int[arr.length];
        int i = 0;
        //頂上にある物を読み取る。
        while(stack.peek() != null){
            //頂上にある要素を取り出していく。
            //上で新しく作っていたintという名の字配列にpopしたデータを入れて行っているのかな??
            reversed[i++] = stack.pop();
        }

        return reversed;
    }

    public static void printList(int[] arr){
        System.out.print("[");
        for(Integer num: arr){
            System.out.print(num + " ");
        }
        System.out.println("]");
    }

    public static void main(String[] args){

        int[] arr = new int[]{1,2,3,4,5,6};
        printList(arr);
        printList(reverse(arr));
    }
}
```

- 上記のようなコードで「元に戻る」などの機能が実装されている。stuck に push された一番上の要素を取ってくれば、元に戻ることができる。
