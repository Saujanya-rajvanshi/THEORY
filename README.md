# THEORY

### OOPS THEORY
[OOPS](#Oops)
<BR>
[THEORY NOTES- oops theory part 1 ](https://drive.google.com/file/d/1h-4RdVIQCNu_loshweVu5TvqvYxHTY2d/view)
<BR>
[notes](https://www.geeksforgeeks.org/cpp/object-oriented-programming-in-cpp/)
<BR>
[.............................. - oops theory part 2 ](https://drive.google.com/file/d/1L5Syt7UWG4FJBDth6tfoBn8FfuEMGLUL/view)
<BR>
[LECTURE - oops vedio leture 1](https://www.youtube.com/watch?v=i_5pvt7ag7E&t=1s)
<BR>
[...................- oops vedio lecture 2](https://www.youtube.com/watch?v=b3GccK5_KSQ)

### DBMS THEORY
[REPOSITORY DBMS](#DBMS)
<BR>
[THEORY NOTES - dbms theory](https://drive.google.com/file/d/1y3KKghRhQjKfbWhvLipMOCCemKd_XdTm/view)
<BR>
[LECTURE - dbms vedio lecture](https://www.youtube.com/watch?v=dl00fOOYLOM&t=34400s)

### OS  THEORY
[REPOSITORY OS](#OS)
<BR>
[THEORY NOTES- OS theory notes](https://drive.google.com/file/d/1kksqpGT_YBQsFwsyVyftikPRP-sZZF-e/view)
<BR>
[LECTURE - OS vedio lecture](https://www.youtube.com/watch?v=3obEP8eLsCw)

### CN THEORY
[REPOSITORY - CN](#CN)
<BR>
[THEORY NOTES - CN theory ]()
<BR>
[LECTURE - CN vedio lecture](https://www.youtube.com/watch?v=IPvYjXCsTg8&t=290s)


// study
// revise 
// practice




# Oops
Object-Oriented Programming (OOP) is a programming paradigm 
* that organizes software using objects
* which combine data (attributes) and methods (functions) that operate on that data
* enabling modularity, reusability, abstraction, and data security.

#### index
- [syntax](#syntax)
- [acess modifiers](#acess-modifiers)
- [setter and getter](#setter-and-getter)
- [padding and greedy alignment](#padding-and-greedy-alignment)
- [static and dynamic](#static-and-dynamic)
- [constructor](#constructor)
- [this](#this)
- [shallow and deep copy](#shallow-and-deep-copy)
- [shallow vs deep copy](#shallow-vs-deep-copy)
- [destructor](#destructor)
- [static keywords](#static-keywords)
- [four pillars](#four-pillars)

   
### syntax 
```cpp
#include <iostream>
using namespace std;

// making class
class Teacher {
    // class properties
    public :
    double salary;
    string name;
    string dept;
    string subject;
    
};

int main() {
    // object value
    Teacher t1 ;
    t1.name = "Saujanya";
    t1.subject = "C++";
    t1.dept = "Computer Science";
    cout << t1.name << endl;
    return 0;
}
```
💡 size of class is sum of all properties
💡 empty class - no properties - size is 1 for identification


## acess modifiers
```cpp
#include <iostream>
using namespace std;

class Teacher {
    // using access modifers
    private:   // private access
    double salary;
    public:   // public access 
    string name;
    string dept;
    string subject;

    void setdept(int h, char pswd) { //protected access
        if(name == "saujanya") {
        dept = h;
        }
    }
};

int main() {
    Teacher t1 ;
    t1.name = "Shradha";
    t1.subject = "C++";
    t1.dept = "Computer Science";
    cout << t1.name << endl;
    return 0;
}
```
💡other files class in vs code can be accesed by #include<file.cpp>


# setter and getter
**Getter** and **Setter** are **public member functions** to **access and modify private data members** of a class, enabling **encapsulation** and controlled data access.
* **Getter** → returns the value of a private variable
* **Setter** → sets or updates the value of a private variable (often with validation)

``` Cpp
#include <iostream>
using namespace std;

// making class
class Teacher {
    // class properties
    private:
    double salary;
    public:
    string name;
    string dept;
    string subject;
    
void changeDept (string newDept) {
    dept = newDept;
}

//setter
void setSalary (double s) {
    salary = s;
}

//getter
double getSalary() {
return salary;
}

};
int main() {
    // object value
    Teacher t1 ;
    t1.name = "Shradha";
    t1.subject = "C++";
    t1.dept = "Computer Science";
    cout << t1.name << endl;
    return 0;
}
```

#### padding and greedy alignment
---

## 🔹 Padding (in OOPS / Memory)
**Padding** is the extra unused memory added by the compiler **between class/struct data members** to satisfy **alignment rules** and make memory access faster.
* CPU accesses memory faster when data is **properly aligned**
* Avoids **multiple memory fetches**
* Improves **performance**

### Example (C++)

```cpp
#include <iostream>
using namespace std;

class A {
    char c;   // 1 byte
    int i;    // 4 bytes
};

int main() {
    cout << sizeof(A);
}
```

### Memory layout (32/64-bit system)

```
| c | pad pad pad | i |
 1B      3B        4B
```
✔ Total size = **8 bytes**, not 5
✔ Padding = **3 bytes**

💡padding depends on:
* Data type sizes
* Alignment requirements
* Order of members
* Target architecture/compiler
* Padding is added only when needed for alignment, not a fixed number of bytes.
---

## 🔹 Alignment
**Alignment** means placing data in memory addresses that are multiples of their size.
* CPUs don’t read memory byte-by-byte logically — they read in words (e.g., 4 bytes, 8 bytes).

| Data Type | Alignment |
| --------- | --------- |
| char      | 1 byte    |
| short     | 2 bytes   |
| int       | 4 bytes   |
| double    | 8 bytes   |

---

## 🔹 Greedy Alignment

### What is Greedy Alignment?

**Greedy alignment** is a strategy where the compiler places **each data member at the next valid aligned address**, even if it causes unused gaps (padding).
➡ Compiler is **greedy for alignment**, not memory saving.


### Example (Bad Order → More Padding)

```cpp
class B {
    char c;
    double d;
    int i;
};
```

Memory layout:

```
| c | pad x7 | d | i | pad x4 |
```

✔ More padding
✔ More memory used

### Optimized (Less Padding)

```cpp
class C {
    double d;
    int i;
    char c;
};
```

Memory layout:

```
| d | i | c | pad x3 |
```

✔ Less padding
✔ Same data, less memory

---

## Key Differences 

| Concept            | Padding            | Greedy Alignment         |
| ------------------ | ------------------ | ------------------------ |
| Meaning            | Extra unused bytes | Placement strategy       |
| Purpose            | Speed              | Correct alignment        |
| Controlled by      | Compiler           | Compiler                 |
| Programmer control | ❌                  | Partially (member order) |

---

## How to Reduce Padding

* Arrange members **largest → smallest**
* Use `#pragma pack(1)` (⚠️ performance cost)

```cpp
#pragma pack(1)
class P {
    char c;
    int i;
};
```
---

### static and dynamic
**Static memory allocation**
* Memory decided at compile time.
* Size and lifetime are fixed before the program runs.
* * memory area is stack/data.

**Dynamic memory allocation**
* memory decided at runtime.
* Size and lifetime are controlled by the programmer.
* Program requests memory from heap, OS provides a memory block
* Address is returned to the program
* Memory exists until explicitly released

```cpp
#include <iostream>
using namespace std;

class Teacher {
private:
    double salary;

public:
    string name;
    string dept;
    string subject;

    // setters
    void setName(string n) {
        name = n;
    }

    void setSubject(string s) {
        subject = s;
    }
};

int main() {
    // static memory allocation
    Teacher t1;
    t1.name = "Alice";
    t1.subject = "Math";

    // dynamic memory allocation
    Teacher* t2 = new Teacher;
    t2->setName("Bob");
    t2->setSubject("Physics");

    cout << "Static object name: " << t1.name << endl;
    cout << "Static object subject: " << t1.subject << endl;
    
    cout << "Dynamic object name: " << t2->name << endl;
    cout << "Dynamic object subject: " << t2->subject << endl;

    delete t2;   // free dynamic memory
    return 0;
}
```

##### constructor
* when a function is created a function (constructor gets build) like name t1.Teacher()
* object creation used for initialisation
* no return type
* input parameter can or cannot be 

```cpp
public:
Teacher() {
cout << "Hi, I am constructor\n";
}
```
```cpp
public:
Teacher () {
    dept = "Computer Science";
}
```
``` cpp
public:
//non-parameterized
Teacher() {
dept = "Computer Science";

//parameterized
Teacher(string n, string d, string s, double sal) {
name = n;
dept =xd;
subject = s;
salary = sal;
}
```
```cpp
//copy constructor
Teacher(Teacher &org0bj) {
    cout << "i am custom copy constructor ... \n";
    this->name = org0bj.name;
    this->dept = org0bj.dept;
    this->subject = org0bj.subject;
    this->salary = org0bj. salary;
}
```
💡 & (ampersand) is used in function parameters — specifically pass by reference — and how it prevents unnecessary copying and traps

# this
---

## 🔹 `this` Keyword (C++)

### What is `this`?

`this` is an **implicit pointer** inside a non-static member function that **points to the current calling object**.

➡ It holds the **address of the current object**.

---

## 🔹 Why `this` is used?

1. To **differentiate data members and parameters**
2. To **return the current object**
3. To **pass current object as argument**
4. To **enable method chaining**

---

## 🔹 Example 1: Resolving name conflict

```cpp
class Student {
    int id;
public:
    void setId(int id) {
        this->id = id;
    }
};
```

✔ `this->id` → data member
✔ `id` → function parameter

---

## 🔹 Example 2: Returning current object

```cpp
class Test {
    int x;
public:
    Test& set(int x) {
        this->x = x;
        return *this;
    }
};
```

Usage:

```cpp
obj.set(10).set(20);
```

✔ Enables **method chaining**

---

## 🔹 Example 3: Passing current object

```cpp
class Demo {
public:
    void show(Demo* obj) {
        cout << "Object passed";
    }

    void call() {
        show(this);
    }
};
```

✔ `this` passes **current object address**

---

## 🔹 Important Rules (Exam Points)

* `this` is a **pointer**
* Available only in **non-static** member functions
* Cannot be used in **static functions**
* Type: `ClassName*`

---

## 🔹 One-Line Definition (Very Important)

> **`this` is a pointer that stores the address of the current calling object.**

---

## 🔹 `this` vs Normal Variable

| Without `this`    | With `this`  |
| ----------------- | ------------ |
| Ambiguous         | Clear        |
| Shadowing problem | No confusion |

---

## 🔹 Common Viva Questions

**Q. Why `this` is not used in static functions?**
👉 Static members do not belong to any object.

**Q. Can we change `this`?**
👉 ❌ No, it is a constant pointer.

---

### shallow and deep copy
```cpp
#include <iostream>
using namespace std;

class Student {
public:
    string name;
    double* cgpaPtr;

    // parameterized constructor
    Student(string name, double cgpa) {
        this->name = name;
        cgpaPtr = new double;
        *cgpaPtr = cgpa;
    }

    // deep copy constructor
    Student(const Student &obj) {
        this->name = obj.name;
        cgpaPtr = new double(*obj.cgpaPtr);
    }

    void getInfo() {
        cout << "Name: " << name << ", CGPA: " << *cgpaPtr << endl;
    }

    // destructor
    ~Student() {
        delete cgpaPtr;
    }
};

int main() {
    Student s1("rahul kumar", 8.9);
    Student s2(s1);   // deep copy

    s1.getInfo();

    *(s2.cgpaPtr) = 9.2;   // change only s2
    s1.getInfo();         // unchanged

    s2.name = "neha";
    s2.getInfo();

    return 0;
}
```

### destructor
A destructor is a special member function of a class that is automatically called when an object is destroyed (goes out of scope or is deleted) and is used to release resources like dynamically allocated memory.

```cpp
//destructor
~Student() {
    cout << "Hi, I delete everything\n";
}
```
```cpp
#include <iostream>
using namespace std;

class Student {
public:
    string name;
    double* cgpaPtr;

    // constructor
    Student(string name, double cgpa) {
        this->name = name;
        cgpaPtr = new double(cgpa);
        cout << "Constructor called for " << name << endl;
    }

    // deep copy constructor
    Student(const Student &obj) {
        name = obj.name;
        cgpaPtr = new double(*obj.cgpaPtr);
        cout << "Copy constructor called for " << name << endl;
    }

    void getInfo() {
        cout << "Name: " << name << ", CGPA: " << *cgpaPtr << endl;
    }

    // destructor
    ~Student() {
        delete cgpaPtr;
        cout << "Hi, I delete everything for " << name << endl;
    }
};

int main() {
    Student s1("rahul kumar", 8.9);
    Student s2(s1);

    s1.getInfo();
    s2.getInfo();

    return 0;   // destructors called automatically here
}

```

### static keywords
The static keyword gives a variable or function a lifetime of the entire program
* it retains its value even after the scope where it is declared ends.
* to accesss you dont need to create object
* can accesss only static member


```cpp
#include <iostream>
#include <string>
using namespace std;

void fun() {
    static int x = 0; //init statement - 1 run
    cout << "x :" << x << endl;
    x++;
}

int main() {
    fun();
    fun();
    fun();
return 0;
}

```
```cpp
class Student : public Person {
public:
    int rollno;

    void getInfo() {
        cout << "name : << name << endl;
        cout << "age : " << age << endl;
        cout << "rollno : " << rollno << endl;
}
```

## four pillars
- [encapsulation](#encapsulation)
- [inherittance](#inherittance)
- [polymorphism](#polymorphism)
- [abstraction](#abstraction)

### encapsulation
* wrapping up of data & member function in a single unit called class
* fully encapsulated class -> all data member are private

<img width="435" height="149" alt="image" src="https://github.com/user-attachments/assets/68b3afc3-0d3d-4995-b564-e2be3362ddd2" />

```cpp
#include <iostream>
using namespace std;

class Student {
private:
    string name;   // hidden data

public:
    void setName(string n) {
        name = n;
    }

    string getName() {
        return name;
    }
};

class GradStudent : public Student {
private:
    string researchArea;   // hidden data

public:
    void setResearchArea(string r) {
        researchArea = r;
    }

    string getResearchArea() {
        return researchArea;
    }
};

int main() {
    GradStudent s1;

    s1.setName("Tony Stark");
    s1.setResearchArea("Quantum Physics");

    cout << s1.getName() << endl;
    cout << s1.getResearchArea() << endl;

    return 0;
}
```


### inherittance
* When properties & member functions of base class are passed on to the derived class.

###### multilevel inheritance
```cpp
class GradStudent : public Student {
public:
    string researchArea;
};

int main() {
    GradStudent s1;
    s1.name = "tony stark";
    s1.researchArea = "quantum physics";
    cout << s1.name << endl;
    cout << s1.researchArea << endl;
    return 0;
}
```
###### multiple inheritance
```cpp
class Student {
public:
    string name;
    int rollno;
};

class Teacher {
public:
    string subject;
    double salary;
};

class TA : public Student, public Teacher {
public:
    string researchArea;
};
```
###### hierarchial inheritance
```cpp
class Person {
public:
    string name;
    int age;
};

class Student : public Person {
public:
    int rollno;
}

class Teacher : public Person{
public:
    string subject;
}
```
###### Ambiguity
Ambiguity occurs in C++ when a derived class inherits two or more base classes that have functions or variables with the same name, and the compiler cannot decide which one to use.
This commonly happens in multiple inheritance.

```cpp
#include <iostream>
using namespace std;

class A {
public:
    void func() {
        cout << "I am A" << endl;
    }
};

class B {
public:
    void func() {
        cout << "I am B" << endl;
    }
};

class C : public A, public B {
};

int main() {
    C obj;
    // obj.func();  // Ambiguous call

    obj.A::func(); // Calls A's func
    // obj.B::func(); // Calls B's func

    return 0;
}
```

### polymorphism 
```cpp
#include <iostream>
using namespace std;

class Print {
public:
    void show(int x) {
        cout << "int : " << x << endl;
    }

    void show(char ch) {
        cout << "char : " << ch << endl;
    }
};

int main() {
    Print p1;
    p1.show(101);
    return 0;
}
```

### 

---

## Function Overloading 

**Function overloading** is a feature of C++ that allows **multiple functions with the same name** but **different parameter lists** (number, type, or order of parameters).
The compiler decides **which function to call at compile time**, based on the arguments passed.
👉 It improves **readability and flexibility** of the program.

* **How Functions Can Be Overloaded**
Functions can be overloaded by:
1. **Different number of arguments**
2. **Different types of arguments**
3. **Different order of arguments**

❌ Function overloading **cannot** be done by return type alone.

* **Logic (How Compiler Works)**

* When a function is called,
* The compiler matches:

  * Function name
  * Number of parameters
  * Data types of parameters
* Then it calls the **best matched function**

This is called **Compile-Time Polymorphism**.

---

## Example 1: Function Overloading with Different Number of Arguments

```cpp
#include <iostream>
using namespace std;

// Function with two parameters
int add(int num1, int num2) {
    return num1 + num2;
}

// Function with three parameters
int add(int num1, int num2, int num3) {
    return num1 + num2 + num3;
}

int main() {
    cout << add(10, 20) << endl;
    cout << add(10, 20, 30) << endl;
    return 0;
}
```

## Example 2: Function Overloading with Different Data Types

```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}

int main() {
    cout << add(5, 3) << endl;
    cout << add(2.5, 3.5) << endl;
    return 0;
}
```

Below is a **clean, exam-ready explanation of Operator Overloading in C++** with **definition, rules, list, and example**, exactly matching what your screenshot shows (CodeStudio → OOPS → Operator Overloading).

---

## Operator Overloading 

###  **Definition**

**Operator overloading** is a feature of C++ that allows programmers to **redefine the behavior of operators** (`+`, `-`, `*`, etc.) for **user-defined data types (objects)**.
It makes objects behave like **built-in data types**.
👉 It is a form of **compile-time polymorphism**.


* **Why Operator Overloading?**

* Improves **code readability**
* Makes user-defined objects **intuitive to use**
* Enables **natural syntax** (e.g., `c1 + c2`)


## General Syntax

```cpp
return_type operator operator_symbol (arguments) {
    // logic
}
```

---

## Operators That **CAN** Be Overloaded in C++

Some commonly overloaded operators:

```
+  -  *  /  %  
== != < > <= >=
++ -- += -= *= /=
<< >> [] ()
&& || !
-> new delete
```

✔ Most arithmetic, relational, logical, and bitwise operators can be overloaded.

---

## Operators That **CANNOT** Be Overloaded in C++

| Operator | Meaning           |
| -------- | ----------------- |
| `::`     | Scope resolution  |
| `.`      | Member access     |
| `.*`     | Pointer to member |
| `?:`     | Ternary operator  |

These operators have **fixed meanings** decided by the compiler.

---

## Example: Operator Overloading (Addition of Complex Numbers)

```cpp
#include <iostream>
using namespace std;

class Complex {
public:
    int real, imag;

    Complex(int r = 0, int i = 0) {
        real = r;
        imag = i;
    }

    // Overload + operator
    Complex operator + (Complex const &obj) {
        Complex temp;
        temp.real = real + obj.real;
        temp.imag = imag + obj.imag;
        return temp;
    }
};

int main() {
    Complex c1(3, 4), c2(1, 2);
    Complex c3 = c1 + c2;

    cout << "Real: " << c3.real << endl;
    cout << "Imaginary: " << c3.imag << endl;

    return 0;
}
```

### Output

```
Real: 4
Imaginary: 6
```

## Important Rules 

✔ At least **one operand must be a user-defined type**
✔ Operator precedence **cannot be changed**
✔ Number of operands **cannot be changed**
✔ Some operators must be overloaded as **member functions** (`=`, `[]`, `()`)


## Function Overloading vs Operator Overloading

| Feature      | Function Overloading | Operator Overloading |
| ------------ | -------------------- | -------------------- |
| Purpose      | Same function name   | Same operator        |
| Polymorphism | Compile-time         | Compile-time         |
| Used for     | Functions            | Operators            |




---

## 🔵 Runtime Polymorphism (C++)

**Runtime polymorphism** is also called **dynamic polymorphism**.
It occurs when the **function call is resolved at runtime**, not at compile time.

👉 In C++, runtime polymorphism is achieved using **method overriding** with **virtual functions**.

---

## Method Overriding

**Method overriding** is a feature in which a **child (derived) class redefines a method of the parent (base) class** with the **same name, same parameters, and same return type** to provide its own implementation.

The decision of which function to call depends on the **object type at runtime**.

## Rules for Method Overriding (Very Important)

1. Function name must be **same** in parent and child class
2. Function parameters must be **same**
3. Return type must be **same**
4. Must use **inheritance**
5. Parent class function must be declared as **virtual**
6. Access is usually through **base class pointer**


## How Runtime Polymorphism Works (Logic)

* Base class pointer points to derived class object
* Compiler decides the function call **at runtime**
* Uses **virtual function table (v-table)** internally


## 🧪 Example: Runtime Polymorphism using Method Overriding

```cpp
#include <iostream>
using namespace std;

class Parent {
public:
    virtual void show() {
        cout << "This is Parent class show function" << endl;
    }
};

class Child : public Parent {
public:
    void show() {
        cout << "This is Child class show function" << endl;
    }
};

int main() {
    Parent* p;
    Child obj;
    p = &obj;

    p->show();   // Runtime decision
    return 0;
}
```

---

### Output

```
This is Child class show function
```

* **What if `virtual` is not used?**
Without `virtual`, **compile-time binding** happens and parent class function is called.

## Compile-Time vs Runtime Polymorphism

| Feature     | Compile-Time                    | Runtime           |
| ----------- | ------------------------------- | ----------------- |
| Binding     | Compile time                    | Runtime           |
| Achieved by | Function / Operator Overloading | Method Overriding |
| Keyword     | No keyword                      | `virtual`         |
| Inheritance | Not required                    | Required          |

---





### abstract
```cpp
#include <iostream>
#include <string>
using namespace std;

class Shape { //abstract class
virtual void draw() = 0; //pure virtual function

};

class Circle : public Shape {
public:
void draw() {
    cout << "drawing a circle\n";
};

int main() {
    Circle c1;
    c1.draw();
return 0;
}
```










# DBMS
- [introduction to database](#Introduction-to-DBMS)
- [DBMS Architecture](#DBMS-Architecture)

---

## Introduction to DBMS

### Data
* Raw, unorganized facts
* No meaning without processing
* Measured in bits & bytes

**Types**
* Quantitative → numerical (weight, cost)
* Qualitative → descriptive (name, gender)

### Information
* Processed & meaningful data
* Used for decision-making

### Data vs Information

| Basis           | Data                                 | Information                 |
| --------------- | ------------------------------------ | --------------------------- |
| Definition      | Collection of raw facts              | Processed data with meaning |
| Nature          | Raw and unorganized                  | Organized and structured    |
| Relationship    | Individual and sometimes unrelated   | Provides big-picture view   |
| Meaning         | Meaningless on its own               | Meaningful after processing |
| Dependency      | Does not depend on information       | Depends on data             |
| Form            | Numbers, graphs, figures, statistics | Words, language, ideas      |
| Decision Making | Not sufficient for decisions         | Used for decision-making    |

### Database
* Organized electronic storage of data
* Easily accessed, updated, managed

### DBMS
* Software to store & manage databases
* Supports insert, delete, update, retrieve

### DBMS vs File System (Why DBMS?)
* No redundancy
* Easy data access
* Better security
* Handles concurrency
* Maintains integrity

---

## DBMS Architecture

### view of data(3-Schema Architecture)
system hides certain details of how the data is stored and maintained, through several levels of abstraction.
1. **Physical Level**
   * How data is stored
2. **Logical Level**
   * What data is stored
   * Relationships
3. **View Level**
   * User-specific views
   * Security
<img width="559" height="387" alt="image" src="https://github.com/user-attachments/assets/ad52331c-ebcb-4d26-8026-dc9243b2f346" />


### Schema vs Instance

* **Schema** → DB structure (static)
* **Instance** → DB data at a time (dynamic)

### Data Models
design at logical level 
data , data relationship , data semantic & consistency
* ER Model, Relational Model, Object-Oriented Model

### DB Languages

* **DDL** → Create structure, specify database schema 
* **DML** → Insert, update, delete
* **SQL** → Combines both

### how is datas accesssed from application program 
apps (written in host languages C,C++,Java) interacts with DB.
<br>API is provided to send DML / DDL Statements to DB and retrieve the result.
<br>     (i)  open database connectivity (DDBC), Microsoft "C" .
<br>     (ii) JAVA database connectivity (JDBC),java

### DBA
* autharization control
* Schema design
* Security
* Backup & maintenance

### DBMS Architectures

* **1-Tier** → Single machine
* **2-Tier** → Client + DB server
* **3-Tier** → Client + App server + DB (best)
<img width="582" height="306" alt="image" src="https://github.com/user-attachments/assets/4e8bb4e6-7023-4844-8892-8b9d38f741fd" />


---

## ER Model

### 🔅 Entity

* Real-world object
* Identified by **Primary Key**
* eg -> Student

**Types**

* Strong Entity → independent
* Weak Entity → depends on strong entity

<img width="691" height="247" alt="image" src="https://github.com/user-attachments/assets/d9e3f9b4-827a-4ce9-8e48-fed464bc794e" />


### 🔅 Attributes
An attribute represents a characteristic or feature of an entity.
A property of an entity
eg -> Roll_No, Name, Age

Types of Attributes (important for exams)

1. Simple Attribute <br> 
Cannot be divided <br> 
Example: Age

2. Composite Attribute <br> 
Can be divided into sub-parts <br> 
Example: Address → Street, City, Pincode

3. Single-valued Attribute <br> 
One value only <br> 
Example: Roll_No

4. Multi-valued Attribute <br> 
Multiple values <br> 
Example: Phone_Number

5. Derived Attribute <br> 
Calculated from another attribute <br> 
Example: Age (derived from Date_of_Birth)

6. Key Attribute <br> 
Uniquely identifies an entity <br> 
Example: Student_ID

7. null value : not applicable <br> 
example : middle name 

<img width="828" height="432" alt="image" src="https://github.com/user-attachments/assets/a307959f-3a27-4a3d-ab60-34dab937a460" />

### 🔅 Relationships

* Association between entities

* **Cardinality**
* one to one
* one to many
* many to one
* many to many

* **Degree**
* Unary, Binary, Ternary

### 🔅 Participation
aka minimium cardinality constraints.
* Partial -> not all  entity envolved
* Total (mandatory) -> all entitty envolved
* **weak entity** has total participation constraints.

<img width="910" height="342" alt="image" src="https://github.com/user-attachments/assets/74f2bfe4-f808-46a4-b5fc-7a826bcf69f9" />


<img width="872" height="474" alt="image" src="https://github.com/user-attachments/assets/65ae1467-af6b-48e1-a77f-f81f22ae4d7b" />

---

## 📘 LEC-4: Extended ER

* **Specialisation** → Top-down
* **Generalisation** → Bottom-up
* **Inheritance** → attributes passed
* **Aggregation** → relationship as entity

---

## 📘 LEC-7: Relational Model

### Basic Terms

* Table → Relation
* Row → Tuple
* Column → Attribute
* Degree → No. of columns
* Cardinality → No. of rows

### Keys

* Super Key
* Candidate Key
* Primary Key
* Alternate Key
* Foreign Key
* Composite Key
* Surrogate Key

### Integrity Constraints

* Domain
* Entity (PK not NULL)
* Referential (FK rules)

---

## 📘 LEC-8: ER → Relational Mapping

* Strong entity → Table
* Weak entity → FK + composite PK
* Composite attribute → split
* Multivalued → new table
* Derived → ignored
* Generalisation → 2 methods
* Aggregation → relationship table

---

## 📘 LEC-9: SQL Basics

### SQL Commands

* **DDL** → CREATE, ALTER, DROP
* **DML** → INSERT, UPDATE, DELETE
* **DQL** → SELECT
* **DCL** → GRANT, REVOKE
* **TCL** → COMMIT, ROLLBACK

### Clauses

* WHERE
* GROUP BY
* HAVING
* ORDER BY
* DISTINCT

### Joins

* INNER
* LEFT
* RIGHT
* FULL (emulated)
* CROSS
* SELF

### Subqueries

* WHERE
* FROM
* SELECT
* Correlated Subquery

### Views

* Virtual table
* No data storage
* Auto-updated

---

## 📘 LEC-11: Normalisation

### Why?

* Remove redundancy
* Avoid anomalies

### Anomalies

* Insertion
* Deletion
* Update

### Functional Dependency

* X → Y

### Normal Forms

* **1NF** → Atomic values
* **2NF** → No partial dependency
* **3NF** → No transitive dependency
* **BCNF** → Stronger than 3NF

---




# CN 

# OS
