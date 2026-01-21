# THEORY

### OOPS THEORY
[REPOSITORY OOPS](#Oops)
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
- [ER Model](#ER-Model)
- [Extended ER](#Extended-ER)
- [Steps to Make ER Diagram](#Steps-to-Make-ER-Diagram)
- [Relational Model](#Relational-Model)
- [ER to Relational Mapping](#ER-to-Relational-Mapping)
- [SQL](#SQL)
- [Normalisation](#Normalisation)
- [Transaction](#Transaction)
- [How to implement Atomicity and Durability in Transactions](#How-to-implement-Atomicity-and-Durability-in-Transactions)
- [Indexing in DBMS](#Indexing-in-DBMS)
- [NoSQL](#NoSQL)
- [Types of Databases](#Types-of-Databases)
- [Clustering in DBMS](#Clustering-in-DBMS)
- [Partitioning & Sharding in DBMS (DB Optimisation)](#Partitioning-Sharding-in-DBMS-DB-Optimisation)

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


<img width="872" height="474" alt="image" src="https://github.com/user-attachments/assets/65ae1467-af6b-48e1-a77f-f81f22ae4d7b" />

---

## Extended ER

* **Specialisation** → Top-down <br>
Specialisation is splitting up the entity set into further sub entity sets on the basis of their functionalities,
specialities and features. <br>
It is a Top-Down approach.
  
* **Generalisation** → Bottom-up <br>
 properties of two entities are overlapping .

* **Inheritance** → attributes passed <br>
Attribute Inheritance <br>
Both Specialisation and Generalisation, has attribute inheritance. <br>
he attributes of higher level entity sets are inherited by lower level entity sets. <br>
E.g., Customer & Employee inherit the attributes of Person

* **Aggregation** → relationship as entity
relationships among relationships <br>
Avoid redundancy 

---

## Steps to Make ER Diagram

* **1) Identify Entity Sets**
* **2) Identify attributes and their types**
* **3) Identify relational and constraints**


### **Example: ER Model of Banking System**

1. Banking system has **branches**
2. Bank has **customers**
3. Customer is **associated with some bank**
4. Customer **has accounts / takes loan**
5. Bank has **employees**
6. Accounts are of two types:
   * Saving Account
   * Current Account
7. Loan:
   * Loan originated by **branch**
   * Loan → **one or more customers**
   * Loan has **payment schedule**

### **1) Entity Set**

1. Branch 2. Customer 3. Employee 4. Saving Account <br>
5. Current Account 6. Loan 7. Payment (weak entity – loan)

### **2) Attributes & Their Types**

1. branch -> name, city, assest, liabilities
2. customer -> cust-id, name, address(composite), contact no(multivalued), DOB , age                              
3. employee -> name contact no. , dependent name(multivalued), years of service(years of services), start-date(single-value) 
4. Saving Account -> acc_number, balance, interest_rate, daily_withdrawal_limit
5. Current Account -> acc_no, balance, per_transaction_charges, overdraft_amount
6. Generalized Entity "Account" -> acc_number, balance
7. Loan -> loan_number, amount
8. Weak Entity "Payment" -> payment_no, date, amount

### **3) Relationship & Constraints**
1. Customer borrows Loan
   * M : N

2. Loan originated by Branch
   * N : 1

3. Loan – Payment
   * 1 : N

4. Customer deposits Account

5. Employee managed by Employee (recursive relationship)

<img width="1125" height="687" alt="image" src="https://github.com/user-attachments/assets/03627f2f-c891-49a3-9979-8458f2524a97" />


---

## Relational Model

### Basic Terms

* **Table** → Relation, A single row / unique record.
* **Row** → Tuple, relationship among a set of values.
* **Column** → Attribute, attributes of the relation.
* **Degree** → No. of columns / attribute.
* **Cardinality** → No. of rows / tuples
* **Relational Key** → Set of attributes which can uniquely identify an each tuple.

### properties 

* unique key
* atomic values
* tuple unique
* sequence any
* integrity constraints

### Keys

* **Super Key (SK) :** combine unique key, can be null  
* **Candidate Key (CK) :** minimum subset of super keys, cannot be null
* **Primary Key (PK) :** selected out of CK set, has least no. of attributes 
* **Alternate Key (AK) :** [CK] - PK 
* **Foreign Key (FK) :** relational key
* **Composite Key :** PK formed using at least 2 attributes.
* **Compound Key :**  PK which is formed using 2 FK.
* **Surrogate Key :** Synthetic PK, Generated automatically by DB, usually an integer value, May be used as PK. 

### Integrity Constraints

* CRUD ( Create Read Update Delete) 
* **Domain Constraints**
* **Entity Constraints**  PK != NULL
* **Referential Constraints** (FK rules) <br>
    * **insert constraints ->** value cant be inserted in child if not present in parent table.
    * **delete constraints ->** value cant be deleted from parent table if the value is lying in child table.

💡 on delete dascade <br>
can we delete value from parent table if the value is lying in the child table w/o violating delete constraints ? <br>
yes -> delete value from parent table -> delete corresponding entry from child table too <br>
<br>
create table order (----- cust id int refrencing customer on delete cascode) <br>
<br>
can F.K. have NULL (value)
on delete null <br>
    - null constraints  <br>
    - unique constraints  <br>
    - default constraints <br>
    - check constraints <br>
    - primary key  <br>

---

## ER to Relational Mapping

* Strong entity → becomes an individual table with entity name, attrbute becomes column <br>
  **PK is used as relation's PK FK**
* Weak entity → table formed with all entity attribute <br>
  **FK + composite PK** PK of corresponding strong entity will be added as FK. 
* single valued attribute → column directly in tables 
* Composite attribute → handled by attribute itself in original relation. **split**
* Multivalued attribute → new table(named as original attribute name) are created for each multivalued attribute <br>
  PK as FK
  PK = FK + multivalued name 
* Derived attribute → not consider in tables 
* Generalisation → M1 create a table for the higher level entity <br>
                   M2 if generalisation is disjoint and complete , table <br>
                   drawback of M2 - stored twice                   
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

## Normalisation

Normalisation is a step towards DB optimisation.

* **Functional Dependency (FD)** <br>
    PK to other attribute / relation <br>
    X -> Y, theleft side of FD - Determinant, the right side of the production - Dependent.
* **Types of FD**
    * Trivial FD : A → B has trivial functional dependency if B is a subset of A. A->A, B->B are also Trivial FD.
    * Non-trivial FD : A → B has a non-trivial functional dependency if B is not a subset of A. [A intersection B is NULL].
* **Rules of FD (Armstrong’s axioms)**
    * Reflexive : If ‘A’ is a set of attributes and ‘B’ is a subset of ‘A’. Then, A→ B holds. <br>
                  If A ⊇ B then A → B. <br>
    * Augmentation : If B can be determined from A, then adding an attribute to this functional dependency won’t change anything. <br>
                     If A→ B holds, then AX→ BX holds too. ‘X’ being a set of attributes. <br>
    * Transitivity : If A determines B and B determines C, we can say that A determines C. <br>
                     If A→ B and B→ C then A→ C. <br>

* Why Normalisation? -> To avoid redundancy in the DB, not to store redundant data. 
* redundant data? -> Insertion, deletion and updation anomalies arises.
 
*  **Anomalies** abnormalities, there are three types of anomalies introduced by data redundancy.
    * Insertion anomaly : can not be inserted into the DB without the presence of other data.
    * Deletion anomaly : The delete anomaly refers to the situation where the deletion of data results in the unintended loss of some other important data.
    * Updation anomaly (or modification anomaly) : The update anomaly is when an update of a single data value requires multiple rows of data to be updated.
2. Due to updation to many places, may be Data inconsistency arises, if one forgets to update the data at all the
intended places.
5. Due to these anomalies, DB size increases and DB performance become very slow.
6. To rectify these anomalies and the effect of these of DB, we use Database optimisation technique called
NORMALISATION.
6. What is Normalisation?
1. Normalisation is used to minimise the redundancy from a relations. It is also used to eliminate undesirable
characteristics like Insertion, Update, and Deletion Anomalies.
2. Normalisation divides the composite attributes into individual attributes OR larger table into smaller and links them
using relationships.
3. The normal form is used to reduce redundancy from the database table.

* **Types of Normal forms**
* 1. 1NF
    1. Every relation cell must have atomic value.
    2. Relation must not have multi-valued attributes.
* 2. 2NF
    1. Relation must be in 1NF.
    2. There should not be any partial dependency.
        1. All non-prime attributes must be fully dependent on PK.
        2. Non prime attribute can not depend on the part of the PK.
* 3. 3NF
    1. Relation must be in 2NF.
    2. No transitivity dependency exists.
        1. Non-prime attribute should not find a non-prime attribute.
* 4. BCNF (Boyce-Codd normal form)
     1. Relation must be in 3NF.
     2. FD: A -> B, A must be a super key.
         1. We must not derive prime attribute from any prime or non-prime attribute.

8. Advantages of Normalisation
1. Normalisation helps to minimise data redundancy.
2. Greater overall database organisation.
3. Data consistency is maintained in DB.

---

## Transaction
* Transaction
    * A unit of work done against the DB in a logical sequence.
    * Sequence is very important in transaction.
    * It is a logical unit of work that contains one or more SQL statements. The result of all these statements in a
transaction either gets completed successfully (all the changes made to the database are permanent) or if at any
point any failure happens it gets rollbacked (all the changes being done are undone.)

* ACID Properties
    * To ensure integrity of the data, we require that the DB system maintain the following properties of the transaction.
    * Atomicity : Either all operations of transaction are reflected properly in the DB, or none are.
    * Consistency : Integrity constraints must be maintained before and after transaction.
                    DB must be consistent after transaction happens.
    * Isolation : Even though multiple transactions may execute concurrently, the system guarantees that, for every pair of
transactions Ti and Tj, it appears to Ti that either Tj finished execution before Ti started, or Tj started execution
after Ti finished. Thus, each transaction is unaware of other transactions executing concurrently in the system.
2. Multiple transactions can happen in the system in isolation, without interfering each other.
    * Durability : After transaction completes successfully, the changes it has made to the database persist, even if there are
system failures.

* Transaction states

<img width="795" height="438" alt="image" src="https://github.com/user-attachments/assets/2fc4883f-938c-4b9a-9579-ccbfa9cfcb45" />

1. Active state : The very first state of the life cycle of the transaction, all the read and write operations are being
performed. If they execute without any error the T comes to Partially committed state. Although if any
error occurs then it leads to a Failed state.

2. Partially committed state
1. After transaction is executed the changes are saved in the buffer in the main memory. If the changes made
are permanent on the DB then the state will transfer to the committed state and if there is any failure, the T
will go to Failed state.

3. Committed state
1. When updates are made permanent on the DB. Then the T is said to be in the committed state. Rollback
can’t be done from the committed states. New consistent state is achieved at this stage.

4. Failed state
1. When T is being executed and some failure occurs. Due to this it is impossible to continue the execution of
the T.

5. Aborted state
1. When T reaches the failed state, all the changes made in the buffer are reversed. After that the T rollback
completely. T reaches abort state after rollback. DB’s state prior to the T is achieved.

6. Terminated state
1. A transaction is said to have terminated if has either committed or aborted.

## How to implement Atomicity and Durability in Transactions

Recovery Mechanism Component of DBMS supports atomicity and durability.

2. Shadow-copy scheme
1. Based on making copies of DB (aka, shadow copies).
2. Assumption only one Transaction (T) is active at a time.
3. A pointer called db-pointer is maintained on the disk; which at any instant points to current copy of DB.
4. T, that wants to update DB first creates a complete copy of DB.
5. All further updates are done on new DB copy leaving the original copy (shadow copy) untouched.
6. If at any point the T has to be aborted the system deletes the new copy. And the old copy is not affected.
7. If T success, it is committed as,
1. OS makes sure all the pages of the new copy of DB written on the disk.
2. DB system updates the db-pointer to point to the new copy of DB.
3. New copy is now the current copy of DB.
4. The old copy is deleted.
5. The T is said to have been COMMITTED at the point where the updated db-pointer is written to disk.

8. Atomicity
1. If T fails at any time before db-pointer is updated, the old content of DB are not affected.
2. T abort can be done by just deleting the new copy of DB.
3. Hence, either all updates are reflected or none.

9. Durability
1. Suppose, system fails are any time before the updated db-pointer is written to disk.
2. When the system restarts, it will read db-pointer & will thus, see the original content of DB and none of the effects of T will
be visible.
3. T is assumed to be successful only when db-pointer is updated.
4. If system fails after db-pointer has been updated. Before that all the pages of the new copy were written to disk. Hence,
when system restarts, it will read new DB copy.
10. The implementation is dependent on write to the db-pointer being atomic. Luckily, disk system provide atomic updates to entire
block or at least a disk sector. So, we make sure db-pointer lies entirely in a single sector. By storing db-pointer at the beginning
of a block.
11. Inefficient, as entire DB is copied for every Transaction.

3. Log-based recovery methods
1. The log is a sequence of records. Log of each transaction is maintained in some stable storage so that if any failure occurs, then
it can be recovered from there.
2. If any operation is performed on the database, then it will be recorded in the log.
3. But the process of storing the logs should be done before the actual transaction is applied in the database.
4. Stable storage is a classification of computer data storage technology that guarantees atomicity for any given write operation
and allows software to be written that is robust against some hardware and power failures.

6. Deferred DB Modifications
1. Ensuring atomicity by recording all the DB modifications in the log but deferring the execution of all the write operations
until the final action of the T has been executed.
2. Log information is used to execute deferred writes when T is completed.
3. If system crashed before the T completes, or if T is aborted, the information in the logs are ignored.
4. If T completes, the records associated to it in the log file are used in executing the deferred writes.
5. If failure occur while this updating is taking place, we preform redo.

7. Immediate DB Modifications
1. DB modifications to be output to the DB while the T is still in active state.
2. DB modifications written by active T are called uncommitted modifications.
3. In the event of crash or T failure, system uses old value field of the log records to restore modified values.
4. Update takes place only after log records in a stable storage.
5. Failure handling
1. System failure before T completes, or if T aborted, then old value field is used to undo the T.
2. If T completes and system crashes, then new value field is used to redo T having commit logs in the logs.
CodeHelp

## Indexing in DBMS

1. Indexing is used to optimise the performance of a database by minimising the number of disk accesses required when a query is
processed.
2. The index is a type of data structure. It is used to locate and access the data in a database table quickly.
3. Speeds up operation with read operations like SELECT queries, WHERE clause etc.
4. Search Key: Contains copy of primary key or candidate key
of the table or something else.
5. Data Reference: Pointer holding the address of disk block
where the value of the corresponding key is stored.
6. Indexing is optional, but increases access speed. It is not the
primary mean to access the tuple, it is the secondary mean.
7. Index file is always sorted.

9. Indexing Methods
1. Primary Index (Clustering Index)
1. A file may have several indices, on different search keys. If the data file containing the records is sequentially ordered, a
Primary index is an index whose search key also defines the sequential order of the file.
2. NOTE: The term primary index is sometimes used to mean an index on a primary key. However, such usage is
nonstandard and should be avoided.
3. All files are ordered sequentially on some search key. It could be Primary Key or non-primary key.
4. Dense And Sparse Indices
1. Dense Index
1. The dense index contains an index record for every search key value in the data file.
2. The index record contains the search-key value and a pointer to the first data record with that search-key value.
The rest of the records with the same search-key value would be stored sequentially after the first record.
3. It needs more space to store index record itself. The index records have the search key and a pointer to the actual
record on the disk.
2. Sparse Index
1. An index record appears for only some of the search-key values.
2. Sparse Index helps you to resolve the issues of dense Indexing in DBMS. In this method of indexing technique, a
range of index columns stores the same data block address, and when data needs to be retrieved, the block
address will be fetched.
5. Primary Indexing can be based on Data file is sorted w.r.t Primary Key attribute or non-key attributes.
6. Based on Key attribute
1. Data file is sorted w.r.t primary key attribute.
2. PK will be used as search-key in Index.
3. Sparse Index will be formed i.e., no. of entries in the index file = no. of blocks in datafile.
7. Based on Non-Key attribute
1. Data file is sorted w.r.t non-key attribute.
2. No. Of entries in the index = unique non-key attribute value in the data file.
3. This is dense index as, all the unique values have an entry in the
index file.
4. E.g., Let’s assume that a company recruited many employees in
various departments. In this case, clustering indexing in DBMS
should be created for all employees who belong to the same
dept.
8. Multi-level Index
1. Index with two or more levels.
2. If the single level index become enough large that the binary
search it self would take much time, we can break down
indexing into multiple levels.
2. Secondary Index (Non-Clustering Index)
1. Datafile is unsorted. Hence, Primary Indexing is not possible.
2. Can be done on key or non-key attribute.
3. Called secondary indexing because normally one indexing is already
applied.
4. No. Of entries in the index file = no. of records in the data file.
5. It's an example of Dense index.
CodeHelp

9. Advantages of Indexing
1. Faster access and retrieval of data.
2. IO is less.
10. Limitations of Indexing
1. Additional space to store index table
2. Indexing Decrease performance in INSERT, DELETE, and UPDATE query.

## NoSQL 

<img width="617" height="638" alt="image" src="https://github.com/user-attachments/assets/4915b60b-5298-4f6c-ba9c-41ed5f0ee6c1" />

## Types of Databases

1. Relational Databases
1. Based on Relational Model.
2. Relational databases are quite popular, even though it was a system designed in the 1970s. Also known as relational database
management systems (RDBMS), relational databases commonly use Structured Query Language (SQL) for operations such as
creating, reading, updating, and deleting data. Relational databases store information in discrete tables, which can be JOINed
together by fields known as foreign keys. For example, you might have a User table which contains information about all your
users, and join it to a Purchases table, which contains information about all the purchases they’ve made. MySQL, Microsoft SQL
Server, and Oracle are types of relational databases.
3. they are ubiquitous, having acquired a steady user base since the 1970s
4. they are highly optimised for working with structured data.
5. they provide a stronger guarantee of data normalisation
6. they use a well-known querying language through SQL
7. Scalability issues (Horizontal Scaling).
8. Data become huge, system become more complex.
2. Object Oriented Databases
1. The object-oriented data model, is based on the object-oriented-programming paradigm, which is now in wide use.
Inheritance, object-identity, and encapsulation (information hiding), with methods to provide an interface to objects, are
among the key concepts of object-oriented programming that have found applications in data modelling. The object-oriented
data model also supports a rich type system, including structured and collection types. While inheritance and, to some extent,
complex types are also present in the E-R model, encapsulation and object-identity distinguish the object-oriented data model
from the E-R model.
2. Sometimes the database can be very complex, having multiple relations. So, maintaining a relationship between them can be
tedious at times.
1. In Object-oriented databases data is treated as an object.
2. All bits of information come in one instantly available object package instead of multiple tables.
3. Advantages
1. Data storage and retrieval is easy and quick.
2. Can handle complex data relations and more variety of data types that standard relational databases.
3. Relatively friendly to model the advance real world problems
4. Works with functionality of OOPs and Object Oriented languages.
4. Disadvantages
1. High complexity causes performance issues like read, write, update and delete operations are slowed down.
2. Not much of a community support as isn’t widely adopted as relational databases.
3. Does not support views like relational databases.
5. e.g., ObjectDB, GemStone etc.
3. NoSQL Databases
1. NoSQL databases (aka "not only SQL") are non-tabular databases and store data differently than relational tables. NoSQL
databases come in a variety of types based on their data model. The main types are document, key-value, wide-column, and
graph. They provide flexible schemas and scale easily with large amounts of data and high user loads.
2. They are schema free.
3. Data structures used are not tabular, they are more flexible, has the ability to adjust dynamically.
4. Can handle huge amount of data (big data).
5. Most of the NoSQL are open sources and has the capability of horizontal scaling.
6. It just stores data in some format other than relational.
7. Refer LEC-15 notes...
4. Hierarchical Databases
1. As the name suggests, the hierarchical database model is most appropriate for use cases in which the main focus of information
gathering is based on a concrete hierarchy, such as several individual employees reporting to a single department at a
company.
2. The schema for hierarchical databases is defined by its tree-like organisation, in which there is typically a root “parent”
directory of data stored as records that links to various other subdirectory branches, and each subdirectory branch, or child
record, may link to various other subdirectory branches.
3. The hierarchical database structure dictates that, while a parent record can have several child records, each child record can only
have one parent record. Data within records is stored in the form of fields, and each field can only contain one value. Retrieving
hierarchical data from a hierarchical database architecture requires traversing the entire tree, starting at the root node.
4. Since the disk storage system is also inherently a hierarchical structure, these models can also be used as physical models.
5. The key advantage of a hierarchical database is its ease of use. The one-to-many organisation of data makes traversing the
database simple and fast, which is ideal for use cases such as website drop-down menus or computer folders in systems like
CodeHelp

Microsoft Windows OS. Due to the separation of the tables from physical storage structures, information can easily be added or
deleted without affecting the entirety of the database. And most major programming languages offer functionality for reading
tree structure databases.
6. The major disadvantage of hierarchical databases is their inflexible nature. The one-to-many structure is not ideal for complex
structures as it cannot describe relationships in which each child node has multiple parents nodes. Also the tree-like
organisation of data requires top-to-bottom sequential searching, which is time consuming, and requires repetitive storage of
data in multiple different entities, which can be redundant.
7. e.g., IBM IMS.
5. Network Databases
1. Extension of Hierarchical databases
2. The child records are given the freedom to associate with multiple parent records.
3. Organised in a Graph structure.
4. Can handle complex relations.
5. Maintenance is tedious.
6. M:N links may cause slow retrieval.
7. Not much web community support.
8. e.g., Integrated Data Store (IDS), IDMS (Integrated Database Management System),
Raima Database Manager, TurboIMAGE etc.
CodeHelp

## Clustering in DBMS

1. Database Clustering (making Replica-sets) is the process of combining more than one servers or instances connecting a single database.
Sometimes one server may not be adequate to manage the amount of data or the number of requests, that is when a Data Cluster is needed.
Database clustering, SQL server clustering, and SQL clustering are closely associated with SQL is the language used to manage the database
information.
2. Replicate the same dataset on different servers.
3. Advantages
1. Data Redundancy: Clustering of databases helps with data redundancy, as we store the same data at multiple servers. Don’t confuse this
data redundancy as repetition of the same data that might lead to some anomalies. The redundancy that clustering offers is required and is
quite certain due to the synchronisation. In case any of the servers had to face a failure due to any possible reason, the data is available at other
servers to access.
2. Load balancing: or scalability doesn’t come by default with the database. It has to be brought by clustering regularly. It also depends on the
setup. Basically, what load balancing does is allocating the workload among the different servers that are part of the cluster. This indicates that
more users can be supported and if for some reasons if a huge spike in the traffic appears, there is a higher assurance that it will be able to
support the new traffic. One machine is not going to get all of the hits. This can provide scaling seamlessly as required. This links directly to
high availability. Without load balancing, a particular machine could get overworked and traffic would slow down, leading to decrement of
the traffic to zero.
3. High availability: When you can access a database, it implies that it is available. High availability refers the amount of time a database is
considered available. The amount of availability you need greatly depends on the number of transactions you are running on your database
and how often you are running any kind of analytics on your data. With database clustering, we can reach extremely high levels of availability
due to load balancing and have extra machines. In case a server got shut down the database will, however, be available.
4. How does Clustering Work?
1. In cluster architecture, all requests are split with many computers so that an individual user request is executed and produced by a number of
computer systems. The clustering is serviceable definitely by the ability of load balancing and high-availability. If one node collapses, the
request is handled by another node. Consequently, there are few or no possibilities of absolute system failures.
CodeHelp

## Partitioning & Sharding in DBMS (DB Optimisation)

1. A big problem can be solved easily when it is chopped into several smaller sub-problems. That is what the partitioning technique does. It divides a
big database containing data metrics and indexes into smaller and handy slices of data called partitions. The partitioned tables are directly used by
SQL queries without any alteration. Once the database is partitioned, the data definition language can easily work on the smaller partitioned slices,
instead of handling the giant database altogether. This is how partitioning cuts down the problems in managing large database tables.
2. Partitioning is the technique used to divide stored database objects into separate servers. Due to this, there is an increase in performance,
controllability of the data. We can manage huge chunks of data optimally. When we horizontally scale our machines/servers, we know that it gives us
a challenging time dealing with relational databases as it’s quite tough to maintain the relations. But if we apply partitioning to the database that is
already scaled out i.e. equipped with multiple servers, we can partition our database among those servers and handle the big data easily.
3. Vertical Partitioning
1. Slicing relation vertically / column-wise.
2. Need to access different servers to get complete tuples.
4. Horizontal Partitioning
1. Slicing relation horizontally / row-wise.
2. Independent chunks of data tuples are stored in different servers.
5. When Partitioning is Applied?
1. Dataset become much huge that managing and dealing with it become a tedious task.
2. The number of requests are enough larger that the single DB server access is taking huge time and hence the system’s response time become
high.
6. Advantages of Partitioning
1. Parallelism
2. Availability
3. Performance
4. Manageability
5. Reduce Cost, as scaling-up or vertical scaling might be costly.
7. Distributed Database
1. A single logical database that is, spread across multiple locations (servers) and logically interconnected by network.
2. This is the product of applying DB optimisation techniques like Clustering, Partitioning and Sharding.
3. Why this is needed? READ Point 5.
8. Sharding
1. Technique to implement Horizontal Partitioning.
2. The fundamental idea of Sharding is the idea that instead of having all the data sit on one DB instance, we split it up and introduce a
Routing layer so that we can forward the request to the right instances that actually contain the data.
3. Pros
1. Scalability
2. Availability
4. Cons

1. Complexity, making partition mapping, Routing layer to be implemented in the system, Non-uniformity that creates the necessity of Re-
Sharding

2. Not well suited for Analytical type of queries, as the data is spread across different DB instances. (Scatter-Gather problem)
CodeHelp








# CN 

# OS
