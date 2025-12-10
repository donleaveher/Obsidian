```cpp
#include<iostream>
#include<thread>
#include<string>
void printHello(std::string s1){
	std::cout<<s1<<endl;
	return;
}
int main(){
	std::thread thread1(printHello,"Hello");
	bool isJoin = thread1.joinable();
	if(isJoin)
		// waiting for thread complete
		thread1.join();
		// thread1.detach()
	return 0;
}
```
***The commen error in Threading***
```cpp
#include<iostream>
#include<thread>
#include<string>
void foo(int& x){
	x += 1;
}
std::thread t;
void foo2(int* x){
	std::cout<<*x<<std::endl;
}

int main(){
	int a = 1;
	//传递引用变量, 注意变量类型
	std::thread thread1(foo, std::ref(a));
	thread1.join();
	int* ptr = new int(1);
	std::thread t(foo, ptr);
	// 手动释放内存，导致内存所指值不在是1
	delete ptr;
	t.join();
	return 0;
}
```
```cpp
#include<iostream>
#include<thread>
#include<string>
#include<memory>
class A{
private:
	friend void thread_foo();
	void foo(){
		std::cout<<"Hello"<<std::endl;
	}
};
void thread_foo()}{
	std::shared_ptr<A> ptr = new std::make_shared<A>();
	std::thread t(&A::foo, ptr);
	t.join();
}
int main(){
	thread_foo();
	return 0;
}
```
***互斥量解决多线程数据共享问题***
```cpp
#include<iostream>
#include<thread>
#include<string>
互斥锁
#include<mutex>
int a=0;
std::mutex mtx;
void func(){
	for(int i=0;i<10000;i++){
		mtx.lock();
		a++;
		mtx.unlock();
	}
}
int main(){
	std::thread t1(func);
	std::thread t2(func);
	t1.join();
	t2.join();
	return 0;
}
```
***互斥量死锁***
![[Pasted image 20251009151738.png]]
 