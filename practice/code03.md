```java
import java.util.Arrays;

class Node{
    public int data;
    public Node next;

    public Node(int data){
        this.data = data;
    }
}
//<E>について載っているものがあった。
//https://so-zou.jp/software/tech/programming/java/collection/list/array-list.htm#:~:text=public%20boolean%20add%20%28E%20e%29%20add%20-%20ArrayList,20%5D%20array.add%20%281%2C%205%29%3B%20%2F%2F%20%5B10%2C%205%2C%2020%5D
//https://docs.oracle.com/javase/jp/7/api/java/util/ArrayList.html

//E	get(int index) -> リスト内の指定された位置にある要素を返します。
class SinglyLinkedListNode<E>{
    public Node head;

    public SinglyLinkedListNode(Node head){
        this.head = head;
    }
}

class Solution{
    public static SinglyLinkedListNode<Integer> getLinkedList(int[] arr){
        // 関数を完成させてください
        //int arr = new int[]{3,2,1,5,6,4};
        //nodeを作って、singlyLinkedListNodeに入れている。
        SinglyLinkedListNode numList = new SinglyLinkedListNode(new Node(arr));
        // SinglyLinkedListNode はthis.headだから、arr[0]じゃない??
        //numlist = [12,2,0,88,88,49];

        Node currentNode = numList.head;
        for(int i = 0; i < numList.length; i++){
            System.out.println(currentNode.data);
            currentNode = currentNode.next;
        }
    }
}

```

- recursion の見本

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
