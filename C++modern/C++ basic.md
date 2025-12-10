## Character operations
```cpp
#include<cctype>
isdigit(c): true if c in range from 0 to 9
isalpha(c): true if c is a-z or A-Z
isspace(c): true if whitespace including '\n'
toupper(c): uppercase version
tolower(c): lowercase version

userStr = "Hey #1?"
userStr.at(0) equal to 'H'
```
## String access operations
```cpp
s1 = "Hey"
s1.size(): the length of str, return 3
s1.push_back('?'): add character to the end of str, "Hey?"
s1.append("!!!!"): add one string to the end of str, "Hey!!!!"
s2 = s1+"1234": using + operation can add two list and return a new str

Loop of str
numLetters = 0;
for (i = 0; i < inputWord.size(); ++i) {
	if (isalpha(inputWord.at(i))) {
         numLetters += 1;
     }
}
userText.find(str)
if find str in userText, == string::pos
else != string::pos
userIndex = userText.find(str1): the first str1 occur in userText
usertext.replace(userIndex, length, replace_str)
```

## Random numbers
```cpp
rand(): in the C standard library
rand()% N yields N possible values from 0 to N - 1
(rand()% N) + 10 yields N possible values from 10 to 10 + N - 1

rand()generate integers are known as pseudo-random. each time a program runs, calls to rand()yield the same sequence of values.
For the first call to rand(), no previous random integer exists, so the function uses a built-in integer known as the seed. By default, the seed is 1. A programmer can change the seed using the function srand(), as in srand(2) or srand(99).

#include<ctime>
srand(time(0))
```

## File input
```cpp
#include<fstream>
ifstream inFs: Input file stream
inFs.open("str")
if(!inFs.is_open())

inFs stream like cin stream
inFs>>fileNum1
inFs>>fileNum2
inFs.close();
inFS,fail(): if the previous stream operation had an error, return true
inFS.eof(): if the previous stream operation reached the end of file return true
while (!inFS.fail()) {
      cout << "num: " << fileNum << endl;
      inFS >> fileNum;
   }
   if (!inFS.eof()) {
      cout << "Input failure before reaching end of file." << endl;
   }

   cout << "Closing file myfile.txt." << endl;

   // Done with file, so close it
   inFS.close();
   
ofstream outFS
outFS.open("str")
outFS << str1 << endl;
```

## Functions
- Function is used to reduce the redundancy and keep the main program simple.
***Step***
1. define a function, name, type, variable.
```cpp
template<typename T>
T function_name(T x1, T x2.... ){
	...
	...
	return T
}
```
***Modularity***
```cpp
double CalcCircularBaseArea(double radius){}

double CalcCylinderVolume(double baseRadius, double height) {
   return CalcCircularBaseArea(baseRadius) * height;
}

double CalcCylinderSurfaceArea(double baseRadius, double height) {
   return (2 * M_PI * baseRadius * height) + (2 * CalcCircularBaseArea(baseRadius));
}
```
***Reference***
```cpp
template<typename T>
void function_name(T& x, T& y){}
```
***Testing***
```cpp
#include<cassert>
double function1(){}
assert(function1() == x)
```

***Inline Member Function***
![[Pasted image 20251004022108.png]]

![[Pasted image 20251004025521.png]]
![[Pasted image 20251004031122.png]]
![[Pasted image 20251004063017.png]]
![[Pasted image 20251004084747.png]]
![[Pasted image 20251004211307.png]]
![[Pasted image 20251005021148.png]]