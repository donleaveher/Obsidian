## List
```cpp
class ListNode{
public:
	int val;
	ListNode *next;
	ListNode(int x) : val(x), next(null){}
};
遍历数组
ListNode* head = createLinkedList({1,2,3,4,5,6});
for(ListNode* p = head; p!=nullptr; p = p->next){
	cout<<p->val<<endl;
}
增加在头节点
ListNode* newNode = new ListNode(0);
newNode->next = head;
head = newNode;
插入到尾节点
p = head
while(p!=nullptr){
	p = p->next;
}
p->next = new ListNode();
在中间插入元素
ListNode* p = head;
int index;
for(int i = 0; i<index-1; i++)
	p = p->next
ListNode* newnode = new ListNode();
newnode->next = p->next;
p->next = newnode; 
删除尾节点
p->next = nullptr;
删除中间节点
p->next = p->next->next;
删除头节点
head = head->next;
```

## Doubly ListNode
```cpp
class DoublyListNode{
public:
	int val;
	DoublyListNode *prev, *next;
	DoublyListNode(int x): val(x), next(NULL), prev(NULL){}
};
DoublyListNode* createDoublyListNode(const vector<int>& arr){
	if(arr.empty())
		return NULL;
	DoublyListNode* head = new DoublyListNode(arr[0])
	DoublyListNode* cur = head;
	for(int i = 1; i<arr.size(); i++){
		DoublyListNode* newNode = new DoublyListNode(arr[i]);
		cur->next = newNode;
		newNode->prev = cur;
		cur = newNode;
	}
	return head;
}

查找
DoublyListNode* head = creatDoublyLinkedList({1,2,3,4,5})
DoublyListNode* tail = nullptr;
for(DoublyListNode* p = head; p!=nullptr; p=p->next){
	cout<<p->val<<endl;
	tail = p;
}
for(DoublyListNode* p = tail; p!=nullptr; p=p->prev){
	cout<<p->val<<endl;
}
```
## 环形数组
```cpp
vector<int> arr = {1,2,3,4,5};
while(i<arr.size()){
	cout<<arr[i]<<endl;
	i = (i+1)%arr.size();
}
```
```cpp
#include<iostream>
#include<stdexcept>
#include<vetor>
#include<ostream>
template<typename T>
class CycleArray{
	std::vector<T> arr;
	int start;
	int end;
	int count;
	// auto resize function
	void resize(int newSize){
		std::vector<T> newArr(newSize);
		for(int i=0; i<count; i++){
			newSize[i] = arr[(start+i)%arr.size()];
		}
		arr = std::move(newArr);
		start = 0;
		end = count;
	}
public:
	CycleArray() : CycleArray(1){}
	explicit CycleArray(int size):
		 arr(size), start(0), end(0), count(0){} 
	void addFirst(const T &val){
		if(isFull())
			resize(arr.size()*2);
		start = (start-1+arr.size())%arr.size();
		arr[start] = val;
		count++;
	}
	void removeFirst(){
		if(isEmpty())
			throw std::runtime_error("Array is empty");
		arr[start] = T();
		start = (start+1)%arr.size();
		count--;
		if(count>0&&count==arr.size()/4)
			resize(arr.size()/2);
	}
	void addLast(const T &val){
		if(isFull()){
			resize(arr.size()*2);
		}
		arr[end] = val;
		end = (end+1)%arr.size();
		count++;
	}
	void removeLast(){
		if(isEmpty())
			throw std::runtime_error("Array is empty");
		end = (end-1+arr.size())%arr.size();
		count--;
		if(count>0&&count == arr.size()/4){
			resize(arr.size()/2);
		}
	}
	T getFirst()const{
		if(isEmpty()){
			throw std::runtime_error("Array is empty");
		}
		return arr[start];
	}
	T getLast()const{
		if(isEmpty())
			throw std::runtime_error("Array is empty");
		return arr[(end-1+arr.size())%arr.size()];
	}
	
	bool isFull()const{
		return count == arr.size();
	}
	int size()const{
		return count;
	}
	bool isEmpty()const{
		return count == 0;
	}
	
}
```
## 栈
```cpp
#include<List>
#include<iostream>
template<typename E>
class MyLinkedStack{
private:
	std::list<E> list;
	
public:
	void push(const E &val){
		list.push_back(val);
	}
	E pop(){
		E value = list.back();
		list.pop_back();
		return value;
	}
	E peek(){
		return list.back();
	}
	int size()const{
		return list.size();
	}
}
```

```cpp
using vector to achieve stack
#include<vector>
template<typename E>
class MyArrayStack{
private:
	std::vector<E> list;
public:
	void push(const E& val){
		list.push_back(e);
	}
	E pop(){
		E topElement = list.back();
		list.pop_back();
		return topELement;
	}
	E peek()const{
		return list.back();
	}
	int size()const{
		return list.size()
	}
}
```
## 队列
```cpp
#include<iostream>
#include<list>
template<typename E>
class MyLinkedQueue{
private:
	std::list<E> list;
public:
	void push(const E &val){
		list.push_back(val);
	}
	E pop(){
		E front = list.front();
		list.pop_front();
		return front;
	}
	E peek(){
		return lis.front();
	}
	int size(){
		return list.size();
	}
}
```

```cpp
#include<deque>
template<typename E>
class MyArrayQueue{
private:
	CycleArray<E> arr;
public:
	MyArrayQueue(){
		arr = CycleArray<E>();
	}
	void push(E t){
		arr.addLast(t);
	}
	E pop(){
		return arr.removeFirst();
	}
	E peek(){
		return arr.getFirst();
	}
	int size(){
		return arr.size();a
	}
}
```