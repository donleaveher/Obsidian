### 线性表
```java
public class ArrayList<T>{
	//存放同一类型的数据
	private int size = 0;
	private int capacity = 10;
	private Object[] array = new Object[capacity];
	
	public void add(T element, int index){
		if(index >= size||index<0){
			throw new IndexOutOfBoundsException("Insert exception");
		}
		if(size>=capacity){
		//enlarge capacity to 1.5 times
			int newCapacity = capacity + (capacity>>1);
			Object[] newArray = new Object[newCapacity];
			System.arraycopy(array, 0, newArray, 0, size);
			array = newArray;
			capacity = newCapcity;
		}
		for(int i = size; i > index; i--){
			array[i] = array[i-1];
		}
		array[index] = element;
		size++;
	}
}
```

### 链表
```java
// Create a Generic class
public class Linkedlist<E>{
	private Node<E> head = new Node<>(Null);
	private int size = 0;
	private static class Node<E>{
		private E element;
		private Node<E> next;
		
		public Node(E e){
			this.element = e
		}
	}
	public void add(E elemenet, int index){
		if(index<0||index>size){
			throw new IndexOutOfBoundsException("Index error");
		}
		Node<E> prev = head;
		for(int i = 0; i<index; i++)
			prev = prev.next;
		Node<E> node = new<E> Node(element);
		node.next = prev.next;
		prev.next = node;
		size++;
	}
	public E remove(int index){
		if(index<0||index>size){
			throw new IndexOutOfBoundsException("Index error");
		}
		for(int i = 0; i<index; i++)
			prev = prev.next;
		E e = prev.next.element;
		prev.next = prev.next.next;
		size--;
		return e;	
		
	}
	public E get(int index){
		if(index<0||index>size){
			throw new IndexOutOfBoundsException("Index error");
		}
		Node<E> node = head
		for(int i = index; i>=0; i--)
			node = node.next
		return node.element
	}
}
```

### 栈
- 线性表的表尾部插入与删除
- 依次以 1,2,3,4 的顺序插入表中，以4,3,2,1的顺序删除(FLO, First in , Last out)
```java
public class stack <E>{
	private final Node<E> head = new Node<>(null);
	
	public void push(E element){
		Node<E> node = new Node<>(element);
		node.next = head.next;
		head.next = node;
	}
	public E pop(){
		if (isEmpty){
			throw NoSuchElement Exception("")
		}
		E e = head.next.element;
		head.next = head.next.next;
	}
	
	public boolean isEmpty(){
		return head.next == null;
	}
	
	private static class Node<E>{
		private E element;
		private Node<E> next;
		
		public Node(E e){
			this.element = e
		}
	}
} 
```

### 队列
- 队尾插入，队首删除
```java
public class queue<E>{
	private final Node<E> head = new Node<>(null);
	
	public void offer(E element){
		Node<E> tail = head;
		while(tail.next != null){
			tail = tail.next;
		}
		tail.next = new Node<>(element);
	}
	public E poll(){
		if (isEmpty){
			throw NoSuchElement Exception("")
		}
		E e = head.next.element;
		head.next = head.next.next;
		return e;
	}
	
	private static class Node<E>{
		private E element;
		private Node<E> next;
		
		public Node(E e){
			this.element = e
		}
	}
}
```