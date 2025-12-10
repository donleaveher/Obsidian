***Input & Output***
```java
import java.util.Scanner;
	public class Salary{
		public static void main(String [] args){
			int wage;
			Scanner scnr = new Scanner(System.in);
			wage = scnr.nextInt();
			System.out.print("Salary is ");
			System.out.println(wage * 40 * 52);
			System.out.print("Salary is " + (wage*40*52)):
		}
	}
```
***Tip***:
- print(): Multiple output statements continue printing on the same output line.
- println(): Start a new output line after the outputted values, called a newline.

***Compiler error***
- Sometimes the compiler error message refers to a line that is actually many lines past where the error actually occurred. Not finding an error at the specified line, the programmer should look to _previous_ lines.

***String***
```java
str.equals(str1); //compare str and str1 content
str == str1;      //compare str and str1 address

str1.concat(str2);

split() methods

String s = "i have promises to keep";
s.split();//{"I", "have", "promises", "to", "keep"}
```
***Array***
```java
dataType[] arr1 =new dataType[numElements];
//Example
int[] arr1 = new int[3];
String[] arr2 = new String[4];
/*
A programmer can declare an array reference variable without allocating the array at that time and later assign the variable with an allocated array.

All array elements are initialized with default int value, or 0.
*/
```
***Object***
```java
public class Restaurant {                         // Info about a restaurant
   // Internal fields
   public void setName(String restaurantName) {   // Sets the restaurant's name
      ...
   }
   public void setRating(int userRating) {        // Sets the rating (1-5, with 5 best)
      ...
   }
   public void print() {                          // Prints name and rating on one line
      ...
   }
}

public class Restaurant {
   private String name;
   private int rating;
#Construction/Overloaded
   public Restaurant() {
		name = "NoName";    
		rating = -1;
	}
	public Restaurant(String n){
		name = n;
	}
   public void setName(String restaurantName) {
      name = restaurantName;
   }

   public void setRating(int userRating) {
      rating = userRating;
   }

   public void print() {
      System.out.println(name + " -- " + rating);
   }
}
```
***Derived Classes -- Inheritance***
```java
public class GenericItem {
   private String itemName;
   private int itemQuantity;

   public void setName(String newName) {
      itemName = newName;
   }
   public void setQuantity(int newQty) {
      itemQuantity = newQty;
   }
   public void printItem() {
      System.out.println(itemName + " " + itemQuantity);
   }
}
public class ProduceItem extends GenericItem { 
   private String expirationDate;

   public void setExpiration(String newDate) {
      expirationDate = newDate;
   }

   public String getExpiration() {
      return expirationDate;
   }  
}
```
**Inheritance Example**
```java
public class Business{
	private String name;
	private String address;
	public void setName(String name1){
		name = name1;
	}
	public void setAddress(String address1){
		address = address1;
	}
	public String getDescription(){
		return name+"--"+address;
	}
}
public class Restaurnt extends Business{
	private int rating;
	public void setRating(int userRating){
		rating = userRating;
	}
	public int getRating(){
		return rating;
	}
}
```
***The difference of Composition and Inheritance***
```java
// Composition
// The 'has-a' relationship. A MotherInfo object 'has a' String object and 'has // a' ArrayList of ChildInfo objects, but no inheritance is involved.
public class ChildInfo {
   public String firstName;
   public String birthDate;
   public String schoolName;

   ...
}
public class MotherInfo {
   public String firstName;
   public String birthDate;
   public String spouseName;
   public ArrayList<ChildInfo> childrenData;
   ...
}

// Inheritance
// The 'is-a' relationship. A MotherInfo object 'is a' kind of PersonInfo. The // MotherInfo class thus inherits from the PersonInfo class. Likewise for the
// ChildInfo class.
public class PersonInfo {
   public String firstName;
   public String birthdate;

   ...
}
public class ChildInfo extends PersonInfo {
   public String schoolName;

   ...
}
public class MotherInfo extends PersonInfo {
   public String spousename;
   public ArrayList<ChildInfo> childrenData;
  ...
}
```
**Call a base class method**
```java
// An overriding method can call the overridden method by using the super
// keyword. Ex: `super.getDescription()`. The super keyword is a reference 
// variable used to call the parent class's methods or constructors.
public class Restaurant extends Business{
   ...
   @Override
   public String getDescription() {
      return super.getDescription() + "\n  Rating: " + rating;
   }
   ...
}
##
```

| Scenario             | Code                | Explanation                                                                                                                                   |
| -------------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Using `this`**     | `this.name = name;` | Assigns the value of the parameter `name` to the instance variable `name`. This is the correct and standard approach when names are the same. |
| **Not Using `this`** | `name = name;`      | Assigns the parameter `name` to itself. The instance variable remains uninitialized. This is a common logical error.                          |
| **Different Names**  | `name = n;`         | Assigns the value of parameter `n` to the instance variable `name`. `this` is not necessary here because there is no name conflict.           |
***Inner Class***
```java
public class Test{
	private final String name;
	public Test(String name){
		this.name = name;
	}

	public class Inner{
		String name;
		public void test(String name){
			//依然是就近原则，最近的是参数，那就是参数了
			System.out.println("....." + name);
			System.out.println("方法参数的name = "+name);
			System.out.println("成员内部类的name = "+this.name);
			System.out.println("成员内部类的name = "+Test.this.name);
			//如果需要指定为外部的对象，那么需要在前面添加外部类型名称 }
		}
	}
}
public static void main(String[] args){
	Test test = new Test();
	Test.Inner inner = test.new Inner();
	
	inner.test();// is valid
}
```
***Static Inner Class***
```java
public class Test{
	private final String name;
	public Test(String name){
		this.name = name;
	}
	
	public static class Inner{
		public void test(){
			System.out.println("I am the static inner class");
			
			System.out.println("I am the static inner class"+name);
			// Invalid 静态内部类由于是静态的，所以相对外部来说，
			// 整个内部类中都处于静态上下文（注意只是相当于外部来说）
			// 是无法访问到外部类的非静态内容的：
		}
	}
}
public static void main(String[] args){
	//静态内部类的类名同样是之前的格式，但是可以直接new了
	Test.Inner inner = new Test.Inner();
}
```
***Local Inner Class***
```java
public class Test {
    public void hello(){
        class Inner{   //局部内部类跟局部变量一样，先声明后使用
            public void test(){
                System.out.println("我是局部内部类");
            }
        }
        
        Inner inner = new Inner();   //局部内部类直接使用类名就行
        inner.test();
    }
}
```
***Anonymous Inner Class***
```java
public abstract class Student {
    public abstract void test();
}

public class Demo {
    public static void main(String[] args) {
        // 创建一个实现了 Runnable 接口的匿名内部类
        Runnable myRunnable = new Runnable() {
            @Override
            public void run() {
                // 这是线程要执行的代码
                System.out.println("匿名内部类实现的线程正在运行...");
            }
            
            int a; //因为本质上就相当于是子类，所以说子类定义一些子类的属性完全没问题 
            @Override
            public void test(){
	            System.out.println(name + "我是匿名内部类的实现!"); 
            }
        };

        Thread thread = new Thread(myRunnable);
        thread.start();
    }
}
```
***Lambda  Expression***
```java
public static void main(String[] args) {
	Study study = () -> System.out.println("我是学习方法！");
	
    Study study = (a) -> {
        System.out.println("我是学习方法");
        return "今天学会了"+a;    //实际上这里面就是方法体，该咋写咋写
    };
    System.out.println(study.study(10));
    
    Study study = (a) -> "今天学会了"+a;
}
```
***Exception***
```java
public static void main(String[] args) {
    test(1, 0);   //当b为0的时候，还能正常运行吗？
}

private static int test(int a, int b){
    return a/b;   //没有任何的判断而是直接做计算
}
```
***Generic***
```java
public class Score{
	String name;
	String id;
	Object score;
	//因为Object是所有类型的父类，因此既可以存放Integer也能存放String
	public Score(String name, String id, Object value){
		this.name = name;
		this.id = id;
		this.score = value;
	}
}
//Pattern class
public class Score<T>{
	String name;
	String id;
	T value;
	public Score(String name, String id, T value){
		this.name = name;
		this.id = id;
		this.value = value;
	}
}
public static void main(String[] args) {
    Score<String> score = new Score<String>("计算机网络", "EP074512", "优秀");
  	//因为现在有了类型变量，在使用时同样需要跟上<>并在其中填写明确要使用的类型
  	//这样我们就可以根据不同的类型进行选择了
    String value = score.value;   //一旦类型明确，那么泛型就变成对应的类型了
    System.out.println(value);
    
    Test<?>test = new Test<String>();
    test = new Test<String>();
    Object o = test.value;
    //但是注意，如果使用通配符，那么由于类型不确定，所以说具体类型同样会变成Object
}

public class Test<A, B, C> {   //多个类型变量使用逗号隔开
    public A a;
    public B b;
    public C c;
}
public static void main(String[] args) {
    Test<String, Integer, Character> test = new Test<>();  //使用钻石运算符可以省略其中的类型
    test.a = "lbwnb";
    test.b = 10;
    test.c = '淦';
}
Tips: 泛型只能确定为一个引用类型，基本类型是不支持的：int, double ······.
	  如果是基本类型的数组，因为数组本身是引用类型，所以说是可以的：
public static void main(String[] args) {
    Test<int[]> test = new Test<>();
}
```
***Generic and Polymorphism***
```java
public interface Study<T>{
	T test();
}
public static A implements Study<Integer>{
	@Override
	public Integer test(){
		return null;
	}
}

public class Main {
    public static void main(String[] args) {
        A<String> a = new A<>();
        String i = a.test();
    }

    static class A<T> implements Study<T> {   
      	//让子类继续为一个泛型类，那么可以不用明确
        @Override
        public T test() {
            return null;
        }
    }
}

static class A<T> {
    
}
static class B extends A<String> {

}
```
***Generic Methods***
```java
public class Main {
    public static void main(String[] args) {
        String str = test("Hello World!");
    }

    private static <T> T test(T t){   
    //在返回值类型前添加<>并填写泛型变量表示这个是一个泛型方法
        return t;
    }
}

public static void main(String[] args) {
    String[] strings = new String[1];
    Main main = new Main();
    main.add(strings, "Hello");
    System.out.println(Arrays.toString(strings));
}

private <T> void add(T[] arr, T t){
    arr[0] = t;
}
```
***Generic Limited***
```java
public class Score<T extend Number>{
	//设定类型参数上界，必须是Number或是Number的子类
	private final String name;
	private final String id;
	private final T value;
	
	public Score(String name, String id, T value){
		this.name = name;
		this.id = id;
		this.value = value;
	}
	public T getValue(){
		return value;
	}
}
```
***Sorting an Arraylist***
```java
public static void main(String[] args){
	Scanner scnr = new Scanner(System.in);
	final int Num = 5;
	ArrayList<Integer>userInts = new ArrayList<Integer>();
	
	userInts.add(scnr.nextInt());
	Collections.sort(userInts);
	userInts.get()
}

```