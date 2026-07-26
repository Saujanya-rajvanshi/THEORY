# THEORY

### 1. OOPS THEORY
- [git hub theory repository](#Oops)
- [Project]()
  
### 2. OS  THEORY
- [git hub theory repository](#OPERATING-SYSTEM)
- [Project]()
  
### 3. DBMS THEORY
- [git hub theory repository](#DBMS)
- [Project - QueryVault](https://github.com/Saujanya-rajvanshi/QueryVault) 

### 4. CN THEORY
- [git hub theory repository](#CN)
- [Project]() 

* striver question
  - [cs core theory question](https://docs.google.com/document/d/1sQlRDw6--HwyxeFL7b4kBsOG-Tz7rXMbpWNnfvJErA4/edit?tab=t.0)


# SQL 





###### Oops
# 🎗 OOPS

Object-Oriented Programming (OOP) is a programming paradigm 
* that organizes software using objects
* which combine data (attributes) and methods (functions) that operate on that data
* enabling modularity, reusability, abstraction, and data security.

```
Implement classes and write your own OOP code

Revise SOLID principles

Practice real-world LLD problems
Elevator System
Parking Lot
BookMyShow / Seat Booking

Be comfortable modeling systems using OOP concepts
```

#### Index

##### Fundamentals (Core Basics)
- [Class](#class)
- [Object](#object)
- [syntax](#syntax)

##### Object Lifecycle
- [
Constructor](#constructor)
- [this Pointer](#this-pointer)
- [Destructor](#destructor)

##### Core Concepts
- [Four Pillars of OOP](#four-pillars-of-oop)
- [Access Modifiers](#access-modifiers)
- [Getter & Setter](#getter--setter)

##### Memory & Object Behavior
- [Static vs Dynamic Allocation](#static-vs-dynamic-allocation)
- [Padding & Memory Alignment](#padding--memory-alignment)

##### Copying & Memory Handling
- [Shallow Copy & Deep Copy](#shallow-and-deep-copy)

##### Advanced Concepts
- [Local vs Global Variables](#local-vs-global-variables)
- [Memory Layout of a Program](#memory-layout-of-a-program)
- [Static Keyword](#static-keyword)
- [const keyword](#const-keyword)
- [Mscros keyword](#Macros-keyword)
- [Can Constructor be Made Private](#can-constructor-be-made-private)
- [Friend Keyword in C++](#friend-keyword-in-c)
- [Virtual Constructor vs Virtual Destructor](#virtual-constructor-vs-virtual-destructor)
- [Inline Functions](#inline-functions)


---
- [OOPS in C](#OOPS-in-C)
- [OOPS in python](#OOPS-in-python)
- [OOPS in JAVA](#OOPS-in-JAVA)
---









#### 🦋 Fundamentals (Core Basics)
## Class

* A **class** is a **user-defined data type**.
* It defines **properties (data members)** and **functions (member functions)**.
* It is a **logical blueprint**, not a real entity.
* **No memory is allocated** when a class is declared.

**Example:**

```cpp
class Student {
public:
    
};
```

---

## Object

* An **object** is a **runtime entity**.
* It is an **instance of a class**.
* Memory is allocated **when an object is created**.
* Objects can access **data members and member functions**.

**Example:**

```cpp
Student s;   // object creation
```

### Memory Note 

* **Without `new`** → memory allocated on **stack**
* **With `new`** → memory allocated on **heap**

```cpp
Student s;              // stack memory
Student* s = new Student(); // heap memory
```

## syntax

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
💡 size of class is sum of all properties <br>
💡 empty class - no properties - size is 1 byte for identification <br>

<br><br>
**Memory breakdown (approx)**  <br>
Member	Size (approx) <br>
double	8 bytes <br>
string	24–32 bytes <br>
string	24–32 bytes <br>
string	24–32 bytes <br><br>

👉 Total (rough) = 8 + 24 + 24 + 24 = 80 bytes (or more depending on system)

---

#### 🦋 Object Lifecycle

## constructor

A **constructor** is a **special member function of a class** that is **automatically called when an object is created** to **initialize the object’s data members**.

* Same name as the class
* **No return type** (not even `void`)
* Called **automatically** during object creation
* Used for **initialization**
* Can have **parameters or no parameters**
* Can be **overloaded** (multiple constructors)
 

```cpp
public:
Teacher() {
    cout << "Hi, I am constructor\n";
}
```

##### parametrized and non-parametrized

``` cpp
public:
//non-parameterized
Teacher() {
    dept = "Computer Science";
}

//parameterized
Teacher(string n, string d, string s, double sal) {
    name = n;
    dept = d;
    subject = s;
    salary = sal;
}
```

##### copy constructor

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

| Feature               | `Teacher t3(t2);` | `Teacher t4 = t2;`          |
| --------------------- | ----------------- | --------------------------- |
| Type                  | Direct init       | Copy init                   |
| Temporary object      | ❌ No              | ⚠️ Conceptually yes         |
| Compiler optimization | Less              | More chances (RVO, elision) |
| Copy constructor call | ✅                 | ✅                           |


ampersand (&) — specifically pass by reference — and how it prevents unnecessary copying and traps <br>
without ampersand (&) This will call copy constructor again <br>
That again needs a copy → infinite recursion <br>

* construction calls -> 1st base class -> 2nd derived class
* destruction calls ->  1st derived class -> 2nd base class

---

## this Pointer

#### What is `this`?
`this` is an **implicit pointer** inside a non-static member function that **points to the current calling object**.
➡ It holds the **address of the current object**.

#### Why `this` is used?
1. To **differentiate data members and parameters**
2. To **return the current object**
3. To **enable method chaining**
4. To **pass current object as argument**

#### Example 1: Resolving name conflict

```cpp
class Student {
    int id;
public:
    void setId(int id) {
        this->id = id;
    }
};

- `this->id` → data member
- `id` → function parameter

```

#### Example 2: Returning current object , enable method chaining

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

- Chaining is just syntactic convenience, not logic change.
- Enables **method chaining**

```


#### Example 3: Passing current object

```cpp
class Demo {
public:
    void show(Demo* obj) {
        cout << "Object passed" << endl;
        cout << "Address received: " << obj << endl;
    }

    void call() {
        cout << "Address using this: " << this << endl;
        show(this);
    }
};

int main() {
    Demo d;
    d.call();
    return 0;
}

`this` passes **current object address**

```


#### Important Rules (Exam Points)

* `this` is a **pointer**
* Available only in **non-static** member functions
* Cannot be used in **static functions**
* Static members do not belong to any object.
* Type: `ClassName*`
* **Can we change `this`?** No, it is a constant pointer.

---

## Destructor

A **destructor** is a special member function of a class that is **automatically called when an object is destroyed** (goes out of scope or is explicitly deleted) and is used to **release resources such as dynamically allocated memory, file handles, or connections**.

* Name is same as class with `~` (tilde)
* **No return type**
* **No parameters**
* Called **automatically**
* Used for **cleanup / deallocation**
* Only **one destructor per class** (no overloading)

```cpp
//destructor
~Student() {
    cout << "Hi, I delete everything\n";
}
```

#### When it is called?

```cpp
int main() {
    Student s1;  // constructor called
}               // destructor called automatically here
```

### where destructor is not called last

#### Case 1: Inner Scope (VERY IMPORTANT)

```cpp
int main() {
    cout << "Start\n";

    {
        A obj;
        cout << "Inside block\n";
    }  // destructor called here

    cout << "End\n";
}
```
```
Start
Constructor
Inside block
Destructor
End
```

#### Case 2: Dynamic Object (`new/delete`)

```cpp
int main() {
    A* obj = new A();

    cout << "Before delete\n";

    delete obj;   // destructor called here

    cout << "After delete\n";
}
```

```
Constructor
Before delete
Destructor
After delete
```

#### Case 4: Program crash / exit

```cpp
exit(0);

Destructor **may NOT run at all**

```

---

### practice

```cpp id="9m3k2s"
#include <iostream>
#include <string>
using namespace std;

class Student {
public:
    int id;
    int age;
    string name;
    int nos;
    int* gpa;

    //-----Default Constructor
    Student() {
        cout << "Student Default ctor called" << endl;
        gpa = new int(0);
    }

    //-----Parameterized Constructor
    Student(int id, int age, string name, int nos, float gpa) {
        cout << "Student Parameterised ctor called" << endl;

        this->id = id;
        this->age = age;
        this->name = name;
        this->nos = nos;

        this->gpa = new int(gpa);  // -----heap allocation
    }

    //-----Copy Constructor (Deep Copy)
    Student(const Student &srcobj) {
        cout << "Student Copy ctor called" << endl;

        this->id = srcobj.id;
        this->age = srcobj.age;
        this->name = srcobj.name;
        this->nos = srcobj.nos;

        this->gpa = new int(*(srcobj.gpa));  //----- deep copy
    }

    //-----Methods
    void study() {
        cout << name << " Studying" << endl;
    }

    void sleep() {
        cout << name << " Sleeping" << endl;
    }

    //-----Destructor
    ~Student() {
        cout << "Student Destructor called" << endl;
        delete gpa;   //-----free memory
    }
};

int main() {

    // ========================= STACK OBJECT =========================
    Student A(1, 15, "Ranu", 6, 9);

    Student B = A;   // copy constructor

    *(A.gpa) = 10;

    cout << "A GPA: " << *(A.gpa) << endl;
    cout << "B GPA: " << *(B.gpa) << endl;

    A.study();
    B.sleep();

    cout << "-------------------" << endl;

    // ========================= DYNAMIC OBJECT (HEAP) =========================
    Student *C = new Student(2, 14, "Babban", 7, 8);

    cout << C->name << endl;
    cout << C->age << endl;
    cout << "C GPA: " << *(C->gpa) << endl;

    C->study();

    //-----IMPORTANT
    delete C;   // destructor called manually

    return 0;
}
```


```text id="d4hl2m"
Student Parameterised ctor called
Student Copy ctor called
A GPA: 10
B GPA: 9
Ranu Studying
Ranu Sleeping
-------------------
Student Parameterised ctor called
Babban
14
C GPA: 8
Babban Studying
Student Destructor called   // for C
Student Destructor called   // for B
Student Destructor called   // for A
```


---












#### 🦋 Core Concepts
## Four Pillars of OOP
- [Encapsulation](#Encapsulation)
- [Inherittance](#Inheritance)
- [Polymorphism](#Polymorphism)
- [Abstraction](#Abstraction)


## Encapsulation

* Encapsulation is **binding data and functions into a single unit (class)**.
* Data is **not accessed directly**; it is accessed via **member functions**.
* Achieves **data hiding** using access specifiers.

**Access Specifiers in C++:**

* `private` → accessible only within the class
* `protected` → accessible in class + derived class
* `public` → accessible everywhere

**Benefits:**

* Data security
* Controlled access
* Better maintainability
  
<img width="435" height="149" alt="image" src="https://github.com/user-attachments/assets/68b3afc3-0d3d-4995-b564-e2be3362ddd2" />

**Example:**

```cpp
class Student {
private:
    int id;

public:
    void setId(int x) {
        id = x;
    }
    int getId() {
        return id;
    }
};
```



### practice
```cpp
#include <iostream>
#include <string>
using namespace std;

class Student {
private:
    //-------Private Data (Encapsulation)
    int id;
    int age;
    string name;
    int nos;
    int* gpa;
    string gf;

public:

    //-------Getter for GPA
    int getGpa() {
        return *gpa;   //-------return value stored in heap
    }

    //-------Setter for GPA
    void setGpa(float a) {
        *gpa = a;   //-------modify value at memory location
    }

    //-------Getter for Age
    int getAge() {
        return age;
    }

    //-------Parameterized Constructor
    Student(int id, int age, string name, int nos, float gpa, string gf) {
        this->id = id;
        this->age = age;
        this->name = name;
        this->nos = nos;
        this->gf = gf;

        this->gpa = new int(gpa);  
        //-------dynamic allocation (heap)
    }

    //-------Destructor
    ~Student() {
        cout << "Destructor called" << endl;
        delete gpa;   //-------free memory
    }
};

int main() {

    Student A(1, 12, "Ranu", 5, 7.8, "Meenu");

    cout << A.getGpa() << endl;   // 7

    A.setGpa(6.7);

    cout << A.getGpa() << endl;   // 6

    cout << A.getAge() << endl;   // 12

    return 0;
}
```

otput flow :

```cpp
7
6
12
Destructor called
```

---




## Inheritance

* **Inheritance** allows one class to acquire properties and functions of another class.
* Helps in **code reusability** and **hierarchical classification**.

**Example:**

```cpp
class Person {
public:
    string name;
};

class Student : public Person {
public:
    int id;
};
```


### Types of Inheritance :

1. **Single inheritance :** When one class inherits another class, it is known as single inheritance.
2. **Multiple inheritance :** Multiple inheritance is the process of deriving a new class that inherits attributes from two or more classes.
3. **Hierarchical inheritance :** Hierarchical inheritance is defined as the process of deriving more than one class from a single base class.
4. **Multilevel inheritance :** Multilevel inheritance is a process of deriving a class from another derived class.
5. **Hybrid inheritance :** Hybrid inheritance is a combination of single, multiple, and hierarchical inheritance.


#### 1. Single Inheritance

```cpp
class Student {
public:
    string name;
};

class GradStudent : public Student {
public:
    string researchArea;
};
```



#### 2. Multiple Inheritance

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


#### 3. Hierarchical Inheritance

```cpp
class Person {
public:
    string name;
    int age;
};

class Student : public Person {
public:
    int rollno;
};

class Teacher : public Person {
public:
    string subject;
};
```



#### 4. Multilevel Inheritance

```cpp
class Student {
public:
    string name;
};

class GradStudent : public Student {
public:
    string researchArea;
};

class PhDStudent : public GradStudent {
public:
    string thesisTopic;
};

int main() {
    PhDStudent s1;
    s1.name = "Tony Stark";
    s1.researchArea = "Quantum Physics";
    s1.thesisTopic = "Time Travel";

    cout << s1.name << endl;
    cout << s1.researchArea << endl;
    cout << s1.thesisTopic << endl;

    return 0;
}
```


#### 5. Hybrid Inheritance (Conceptual Example)

```cpp
class Person {
public:
    string name;
};

class Student : public Person {
};

class Teacher {
};

class TA : public Student, public Teacher {
};
```


#### Ambiguity
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

    // obj.func();   //------ Error: Ambiguous

    obj.A::func();   //------ Calls A's func
    obj.B::func();   //------ Calls B's func

    return 0;
}
```
```
I am A
I am B
```

### practice

```cpp
#include <iostream>
#include <string>
using namespace std;

//------------- Base Class
class Vehicle {
protected:
    string name;
    string model;
    int noOfTyres;

public:
    //------------- Constructor
    Vehicle(string _name, string _model, int _noOfTyres) {
        cout << "I am inside Vehicle ctor" << endl;

        this->name = _name;
        this->model = _model;
        this->noOfTyres = _noOfTyres;
    }

    //------------Methods
    void start_engine() {
        cout << "Engine is starting " << name << " " << model << endl;
    }

    void stop_engine() {
        cout << "Engine is stopping " << name << " " << model << endl;
    }
};

//--------------Derived Class: Car
class Car : public Vehicle {
protected:
    int noOfDoors;
    string transmissionType;

public:
    //----------Constructor chaining (IMPORTANT)
    Car(string _name, string _model, int _noOfTyres, int _noOfDoors, string _transmissionType) : Vehicle(_name, _model, _noOfTyres)   //------------Base constructor call
    {
        cout << "I am inside Car ctor" << endl;

        this->noOfDoors = _noOfDoors;
        this->transmissionType = _transmissionType;
    }

    void startAC() {
        cout << "AC has started of " << name << endl;  //----------protected access
    }
};

//------------Derived Class: MotorCycle
class MotorCycle : public Vehicle {
protected:
    string handleBarStyle;
    string suspensionType;

public:
    //-------------Constructor chaining
    MotorCycle(string _name, string _model, int _noOfTyres,
               string _handleBarStyle, string _suspensionType)
        : Vehicle(_name, _model, _noOfTyres)
    {
        cout << "Motorcycle ctor called" << endl;

        this->handleBarStyle = _handleBarStyle;
        this->suspensionType = _suspensionType;
    }

    void wheelie() {
        cout << "Wheelie kar rahi hai " << name << endl;
    }
};

int main() {

    //------------Car Object
    Car A("Maruti 800", "LXI", 4, 4, "Manual");

    A.start_engine();
    A.startAC();
    A.stop_engine();

    cout << endl;

    //-------------- Motorcycle Object
    MotorCycle M("BMW", "VXI", 2, "U", "Hard");

    M.start_engine();
    M.wheelie();
    M.stop_engine();

    return 0;
}
```

output flow :
```cpp
I am inside Vehicle ctor
I am inside Car ctor
Engine is starting Maruti 800 LXI
AC has started of Maruti 800
Engine is stopping Maruti 800 LXI

I am inside Vehicle ctor
Motorcycle ctor called
Engine is starting BMW VXI
Wheelie kar rahi hai BMW
Engine is stopping BMW VXI
```


---


## Polymorphism 

* Polymorphism means **one interface, many forms**
* Same function behaves **differently based on context**
* Derived from:
    * Poly → many
    * Morphism → forms

#### Types of Polymorphism

1. **Compile-Time (Static Binding)**
2. **Runtime (Dynamic Binding)**


### 1. Compile-Time Polymorphism (Static Binding)

* Resolved **at compile time**, Faster (no runtime overhead)
* Achieved using:
  * Function Overloading
  * Operator Overloading

#### 1.1 Function Overloading

Function overloading allows **same function name** with **different parameters**

* Must differ in:
  * Number of parameters
  * Type of parameters
  * Order of parameters
* Cannot differ only by return type

```cpp
int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}
```



### 1.2 Operator Overloading

Allows operators (`+`, `-`, etc.) to work with **objects**

##### Syntax

```cpp
return_type operator operator_symbol(arguments) {
    // logic
}
```

* Improves readability
* Natural syntax (`a + b`)
* Makes objects behave like built-in types

#### Operators That Can Be Overloaded

```
+  -  *  /  %  
== != < > <= >=
++ -- += -= *= /=
<< >> [] ()
&& || !
-> new delete
```

#### Operators That Cannot Be Overloaded

```
:: ( Scope resolution )  
.  ( Member access )
.* ( Pointer to member )
?: ( Ternary )
```

### Example

```cpp
#include <iostream>
using namespace std;

class Complex {
public:
    int real, imag;

    Complex(int r = 0, int i = 0) {    // initialise value of c1, c2
        real = r;
        imag = i;
    }

    Complex operator + (Complex const &obj) {     // c1.operator+(c2), obj = second object (right side)
        Complex temp;
        temp.real = real + obj.real;  // real parts → 3 + 1 = 4
        temp.imag = imag + obj.imag;  // imag parts → 4 + 2 = 6
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

**Output**

```
Real: 4
Imaginary: 6
```

#### Rules

* At least one operand must be object
* Precedence cannot change
* Number of operands cannot change

### 2. Runtime Polymorphism (Dynamic Binding)

* Resolved **at runtime**
* Slightly slower (uses indirection)
* Achieved using:
  * Method Overriding
  * Virtual Functions


#### 2.1 Method Overriding

Child class **redefines** parent class function

##### Rules

* Same function name
* Same parameters
* Same return type
* Requires inheritance
* Base function must be `virtual`

## **2.2 Virtual Functions**

A **virtual function** is a member function that is declared using `virtual` keyword and allows **runtime decision (dynamic binding)**.

* Enables **runtime polymorphism**
* Ensures the **correct function is called based on object type**
* Supports **dynamic binding**

### **Working Mechanism**

* A **base class pointer** can point to a **derived class object**
* Uses **v-table (virtual table)** internally
* Function call decision happens **at runtime**
  
### (With Virtual)

* **“Real object decides”**
* Runtime checks actual object (`Child`)
* Calls **derived class function**
* This is **runtime binding**

#### **Example (With Virtual)**

```cpp
#include <iostream>
using namespace std;

class Parent {
public:
    virtual void show() {
        cout << "Parent class" << endl;
    }
};

class Child : public Parent {
public:
    void show() {
        cout << "Child class" << endl;
    }
};

int main() {
    Parent* p;
    Child obj;

    p = &obj;
    p->show();   // Runtime binding

    return 0;
}
```

### **Output**

```
Child class
```

### (Without Virtual)

* **“Left side (pointer type) decides”**
* Compiler only sees `Parent*`
* Ignores actual object (`Child`)
* This is **compile-time binding**

#### example **Without Virtual**

```cpp
class Parent {
public:
    void show() {
        cout << "Parent class" << endl;
    }
};

class Child : public Parent {
public:
    void show() {
        cout << "Child class" << endl;
    }
};
```

```cpp
Parent* p = new Child();
p->show();
```

### **Output**

```
Parent class
```

| Case              | Decision Taken By | Binding Type | Output        |
| ----------------- | ----------------- | ------------ | ------------- |
| With `virtual`    | Object type, Real object decides       | Runtime      | Derived class |
| Without `virtual` | Pointer type, Left side decides      | Compile-time | Base class    |


### 4. Types of Binding

| Type          | Time         | Example              |
| ------------- | ------------ | -------------------- |
| Early Binding | Compile time | Function Overloading |
| Late Binding  | Runtime      | Virtual Functions    |

### 5. Data Binding (Conceptual)

* Connects **UI + logic**
* Changes in logic reflect in UI
* Used in frameworks (React, Angular)

### 6. Connection with Class Syntax

Polymorphism exists **inside classes**

```cpp
#include <iostream>
using namespace std;

class Teacher {
public:
    double salary;
    string name;
    string dept;
    string subject;
};

int main() {
    Teacher t1;
    t1.name = "Saujanya";

    cout << t1.name << endl;
    return 0;
}
```

#### Final Keyword

1. In C++, the final specifier is used in two main contexts: with classes and with virtual member
functions.
2. **Prevents Class Inheritance:** When you declare a class as final, it means that no other class
can inherit from it.
3. **Preventing Virtual Function Overriding:** The final specifier can also be used with virtual
functions to prevent them from being overridden in derived classes.

---

## Abstraction

* Abstraction means **showing only essential details** and hiding unnecessary details.
* Focuses on **what an object does**, not **how it does it**.
* Helps in solving **complex real-world problems efficiently**.
* It is a design and programming method that separates the interface from the implementation.

**Achieved using:**

* Classes
* Abstract classes
* Interfaces (using pure virtual functions)

### Abstraction using Classes

* 1. Grouping data members and member functions into classes using access specifiers.
* 2. A class can choose which data members are visible to the outside world and which are hidden.

```cpp
class AbstractionExample{
    private:
        int num;
        char ch;

    public:
        void setMyValues(int n, char c) {
            num = n; ch = c;
        }

       void getMyValues () {
           cout << "Numbers is: " << num << endl;
           cout << "Char is: " << ch << endl;
    }
};
```

### Abstract classes

* 1. Class that contains at least one pure virtual function, and these classes cannot be
instantiated. so, Bird *b2 = new Bird(); is not applicable
* 2. It has come from the idea of Abstraction.
* C++ doesn’t have a keyword like interface (unlike Java), but we create it using an abstract class with:

```cpp
#include <iostream>
using namespace std;

// Abstract class
class Bird {
public:
    virtual void eat() = 0;   // Pure virtual function
    virtual void fly() = 0;   // Pure virtual function
};

// Derived class
class Sparrow : public Bird {
public:
    void eat() {
        cout << "Sparrow is eating\n";
    }

    void fly() {
        cout << "Sparrow is flying\n";
    }
};

int main() {
    Bird* b;
    Sparrow s;

    b = &s;
    b->eat();
    b->fly();

    return 0;
}
```


---

## Access Modifiers

Access modifiers control **visibility (who can access data/functions)**.

### Types

#### 1. Public

* Accessible **from anywhere**
* No restriction

#### 2. Private

* Accessible **only inside the same class**
* Not accessible outside or in derived class

#### 3. Protected

* Accessible **inside class + derived (child) class**
* Not accessible outside


#### Default 

* `class` → **private by default**
* `struct` → **public by default**

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

---

## Getter & Setter

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

---




#### 🦋 Memory & Object Behavior

## Static vs Dynamic Allocation

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

---

## Padding & Memory Alignment

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

### Alignment
**Alignment** means placing data in memory addresses that are multiples of their size.
* CPUs don’t read memory byte-by-byte logically — they read in words (e.g., 4 bytes, 8 bytes).

| Data Type | Alignment |
| --------- | --------- |
| char      | 1 byte    |
| short     | 2 bytes   |
| int       | 4 bytes   |
| double    | 8 bytes   |

### Greedy Alignment

**Greedy alignment** is a strategy where the compiler places **each data member at the next valid aligned address**, even if it causes unused gaps (padding).
➡ Compiler is **greedy for alignment**, not memory saving.


#### Example (Bad Order → More Padding)

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

#### Optimized (Less Padding)

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

* Less padding
* Same data, less memory


## Key Differences 

| Concept            | Padding            | Greedy Alignment         |
| ------------------ | ------------------ | ------------------------ |
| Meaning            | Extra unused bytes | Placement strategy       |
| Purpose            | Speed              | Correct alignment        |
| Controlled by      | Compiler           | Compiler                 |
| Programmer control | ❌                  | Partially (member order) |


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











#### 🦋 Copying & Memory Handling
## shallow and deep copy

### **1. Constructor (Normal Constructor)**

Initialize a **new object**

```cpp
Student s1(10);   // constructor called
```

### **2. Copy Constructor**

Purpose : Create a **new object as a copy of an existing object**
<br><br>
When called

* `Student s2 = s1;`
* `Student s2(s1);`

```cpp
Student(const Student &obj) {
    this->x = obj.x;
}
```

### **3. Shallow Copy (Default Behavior)**

* Copies **values directly**
* If pointer exists → copies **address only**
* Problem : Both objects share same memory → **danger (double delete, bugs)**

### **4. Deep Copy**

* Purpose : Copy **actual data**, not just address
* What happens : New memory is created, Values are copied

```cpp
Student(const Student &obj) {
    this->data = new int(*obj.data);  // deep copy
}
```
---










#### 🦋  Advanced Concepts

## Static Keyword

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

---




## **Local vs Global Variables**

### **Local Variables**

* Declared **inside a function or block**
* Scope is limited to that block/function
* Cannot be accessed outside

```cpp
#include <iostream>
using namespace std;

void func() {
    int x = 10; // local variable
    cout << x;
}

int main() {
    func();
    // cout << x; // Error
}
```

### **Global Variables**

* Declared **outside all functions**
* Accessible throughout the program

```cpp
#include <iostream>
using namespace std;

int x = 20; // global variable

void func() {
    cout << x;
}

int main() {
    func();
    cout << x;
}
```

```cpp
#include <iostream>
using namespace std;

int x = 2; // GLOBAL VARIABLE

void fun()
{
    int x = 60;
    cout << x << endl;     // 60, local to fun
    ::x = 40;              // modify global
    cout << ::x << endl;   // 40, global
}

int main()
{
    ::x = 4;        // modify global
    int x = 20;     // local to main
    {
        int x = 50;     // new block (different scope)
        {
            int x = 44; // inner block (different scope)
        }      
        cout << x << endl;   // 50
        cout << x << endl;   // 50
        cout << ::x << endl; // 4
    }
    fun(); // call function
    return 0;
}
```
```
50
50
4
60
40
```

### **Difference**

| Feature  | Local Variable                   | Global Variable          |
| -------- | -------------------------------- | ------------------------ |
| Scope    | Inside function/block            | Entire program           |
| Lifetime | Exists during function execution | Exists till program ends |
| Access   | Limited                          | Accessible everywhere    |
| Memory   | Stack                            | Data segment             |

---


## **Memory Layout of a Program**

A C++ program is divided into different memory sections:

### **1. Text Segment**

* Stores **compiled program code (instructions)**
* Read-only

### **2. Data Segment**

Stores global and static variables

#### **a) Initialized Data**

* Global/static variables with values

```cpp
int x = 10;
```

#### **b) Uninitialized Data (BSS)**

* Default initialized to 0

```cpp
int y;
```


### **3. Heap**

* Used for **dynamic memory allocation** (`new`, `malloc`)
* Managed manually by programmer

```cpp
int* ptr = new int(10);
```

### **4. Stack**

* Stores:

  * Local variables
  * Function calls
* Works in **LIFO (Last In First Out)**

```cpp
void func() {
    int x = 5; // stored in stack
}
```

### **5. Memory Flow**

* Stack grows **downward**
* Heap grows **upward**

### **Diagram (Conceptual)**

```
High Address
-------------
|   Stack   |
-------------
|           |
|           |
|   Heap    |
-------------
|   BSS     |
-------------
|   Data    |
-------------
|   Text    |
-------------
Low Address
```

### **Key Points**

* Stack is **fast but limited**
* Heap is **flexible but slower**
* Global/static → Data segment
* Local → Stack
* Dynamic → Heap



## const keyword

* `const` is used to make a variable **constant (read-only)**
* Value must be **initialized at declaration**
* Cannot be modified later in the program

```cpp
const int x = 5;
x = 10; // Error
```

#### **Types of const Usage**

### **1. const Variable**

* Value cannot be changed after initialization

```cpp
const int a = 10;
// a = 20; // Error
```

### **2. const Pointer**

```
int *a = new int;
*a = 2;
cout << *a << endl;
delete a; // if not the memory leek
int b = 5;
a = &b;
cout << *a << endl;
```

#### **CONST data, NON-CONST pointer.
```cpp
int x = 10;
const int *a = new int(2) ;
const int *a = new int(2); // CONST data, NON-CONST pointer.
cout << *a << endl;
// *a = 20; // error cant change the content of the pointer 
// cout  << *a << endl;
int b = 20;
a = &b;
cout << *a << endl;
```

#### **NON-CONST data, CONST pointer**

```cpp
int *const a = new int(2);
cout << *a << endl;
*a = 20; // chal jayega
cout << *a << endl;
int b = 50;
a = &b; // nahi chalega, CONST pointer.
```

#### **CONST data, CONST pointer**

```cpp
// CONST pointer, CONST data
const int *const a = new int(10);
cout << *a << endl;
*a = 50;
int b = 100;
a = &b;
```

### **3. const in Function Parameters**

* Prevents modification of arguments

```cpp
void print(const int x) {
    // x = 10; // Error
    cout << x;
}
```

#### **With reference**

```cpp
void print(const int &x) {
    // x = 20; // Error
}
```

### **4. const Member Function**

* Cannot modify object data members
* Used in classes

```cpp
class Test {
public:
    int x;

    void display() const {
        // x = 10; // Error
        cout << x;
    }
};
```
```cpp
// initialization list
abc(int _x, int _y, int _z = 0) : x(_x), y(new int(_y)), z(_z) {}
```

### **5. const Objects**

* Can only call **const member functions**

```cpp
class Test {
public:
    void show() const {
        cout << "Const function";
    }

    void modify() {
        cout << "Modify";
    }
};

int main() {
    const Test obj;
    obj.show();   // Allowed
    // obj.modify(); // Error
}
```

### **6. const with Return Type**

* Prevents modification of returned value

```cpp
const int getValue() {
    return 10;
}
```

#### **Why Use const**

* Prevents accidental changes
* Makes code safer and predictable
* Helps compiler optimization
* Improves readability

#### **Important Points**

* Must initialize at declaration
* Works with variables, pointers, functions, objects
* Widely used in **OOP and APIs**
* `const` correctness is important in interviews


---


## **MACROS Keyword**

* Macros are **preprocessor directives**
* Defined using `#define`
* Processed **before compilation** (by preprocessor)
* Perform **text substitution**, not actual variable/function creation

#### **Types of Macros**

### **1. Object-like Macros (Constants)**

* Used to define constant values

```cpp
#define PI 3.14

int main() {
    cout << PI; // replaced by 3.14
}
```

### **2. Function-like Macros**

* Work like functions but are just text replacement

```cpp
#define SQUARE(x) (x * x)

int main() {
    cout << SQUARE(5); // 25
}
```

## **Important Difference from Functions**

* No type checking
* No function call overhead
* Can lead to unexpected results

```cpp
#define SQUARE(x) x * x

int main() {
    cout << SQUARE(2 + 3); // 2 + 3 * 2 + 3 = 11 (wrong)
}
```

Correct way:

```cpp
#define SQUARE(x) ((x) * (x))
```

### **3. Multi-line Macros**

* Use `\` for line continuation

```cpp
#define PRINT \
cout << "Hello"; \
cout << "World";
```

### **4. Conditional Macros**

* Used for conditional compilation

```cpp
#define DEBUG

#ifdef DEBUG
cout << "Debug Mode";
#endif
```

### **5. Undefining Macros**

* Remove a macro definition

```cpp
#define X 10
#undef X
```

#### **Advantages**

* Faster execution (no function call)
* Code reusability
* Useful for constants and debugging

#### **Disadvantages**

* No type safety
* Hard to debug
* Can cause unexpected bugs
* Not recommended over modern alternatives

#### **Modern Alternatives**

* `const` variables
* `constexpr`
* Inline functions

```cpp
constexpr int square(int x) {
    return x * x;
}
```

#### **Key Points**

* Macros are **text substitution only**
* Handled before compilation
* Use carefully in competitive programming
* Prefer safer alternatives in real projects




## **Can Constructor be Made Private**

### **Concept**

* Yes, constructors **can be private** in C++
* Prevents object creation from outside the class

### **Why Use**

* To **control object creation**
* Used in:

  * **Singleton design pattern**
  * Factory methods

### **Example**

```cpp
#include <iostream>
using namespace std;

class Test {
private:
    Test() {
        cout << "Constructor called";
    }

public:
    static Test createObject() {
        return Test();
    }
};

int main() {
    // Test obj; // Error (constructor is private)
    Test obj = Test::createObject(); // Allowed
}
```

---

## **Friend Keyword**

### **Concept**

* `friend` allows a function or class to access **private and protected members**
* CAN ALSO BE DONE BY SINGELTON CLASS

### **Types**

* Friend function
* Friend class

### **Friend Function Example**

```cpp
#include <iostream>
using namespace std;

class Test {
private:
    int x;

public:
    Test() { x = 10; }

    friend void show(Test obj);
};

void show(Test obj) {
    cout << obj.x; // accessing private member
}
```

### **Friend Class Example**

```cpp
class A {
private:
    int x = 10;

    friend class B;
};

class B {
public:
    void show(A obj) {
        cout << obj.x;
    }
};
```

### **Key Points**

* Not inherited
* Breaks encapsulation (use carefully)
* Declared inside class, defined outside

## **Virtual Constructor vs Virtual Destructor**

### **Virtual Constructor**

* **Not possible in C++**
* Constructors cannot be virtual because:

  * Object is not fully created yet
  * Virtual mechanism needs a fully constructed object

### **Virtual Destructor**

* **Used in inheritance**
* Ensures proper deletion of derived class objects

### **Why Needed**

* When deleting object using **base class pointer**

### **Example**

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual ~Base() {
        cout << "Base Destructor\n";
    }
};

class Derived : public Base {
public:
    ~Derived() {
        cout << "Derived Destructor\n";
    }
};

int main() {
    Base* obj = new Derived();
    delete obj;
}
```

### **Output**

```
Derived Destructor
Base Destructor
```

### **Key Points**

* Always use **virtual destructor in base class**
* Prevents memory leaks

---








## **Inline Functions**

### **Concept**

* `inline` suggests compiler to **replace function call with function body**
* Reduces function call overhead

### **Syntax**

```cpp
inline int add(int a, int b) {
    return a + b;
}
```

### **Example**

```cpp
#include <iostream>
using namespace std;

inline int square(int x) {
    return x * x;
}

int main() {
    cout << square(5);
}
```

### **Advantages**

* Faster execution (no function call overhead)
* Useful for small functions

### **Disadvantages**

* Increases code size
* Compiler may ignore `inline`
* Not suitable for large/complex functions

### **When to Use**

* Small, frequently used functions
* Getter/setter functions

### **Important Points**

* Inline is a **request, not a command**
* Functions inside class are **implicitly inline**
* Avoid recursion with inline



---

















# OOPS in python
## 🎗 OOP — Python vs C++

### ✅ CONCEPTS THAT STAY

* Class & Object
* Encapsulation
* Inheritance
* Polymorphism
* Abstraction

### ❌ C++-ONLY FEATURES

| C++ Feature              | Python              |
| ------------------------ | ------------------- |
| Access specifiers        | ❌ (convention only) |
| Constructors overloading | ❌                   |
| Destructors              | ❌                   |
| Multiple constructors    | ❌                   |

### ✅ Python OOP

```python
class A:
    def __init__(self, x):
        self.x = x
```

📌 **Exam Line:**

> Python supports OOP but with **dynamic binding and duck typing**.

---

- [OOPS in JAVA](#OOPS-in-JAVA)



















# OPERATING SYSTEM

## INDEX

#### 🪵 Basics of OS
- [Harware and Software](#Harware-and-Software)
- [Definiton](#Definiton)
- [Types of OS](#Types-of-OS)
- [Multi-Tasking vs Multi-Threading](#Multi-Tasking-vs-Multi-Threading)
- [Components of OS](#Components-of-OS)
- [32 Bit vs 64 Bit OS](#32-Bit-vs-64-Bit-OS)
- [Storage Devices Basics](#Storage-Devices-Basics)
- [What happens when you turn on your computer](#What-happens-when-you-turn-on-your-computer)

#### 🪵 System Calls & Modes
- [System Calls](#System-Calls)

#### 🪵 Process Management
- [Introduction to Process](#Introduction-to-Process)
- [Process States Process Queues](#Process-States-Process-Queues)
- [Swapping | Context-Switching | Orphan process | Zombie process](#Swapping-Context-Switching-Orphan-process-Zombie-process)
- [Intro to Process Scheduling | FCFS | Convoy Effect](#Intro-to-Process-Scheduling-FCFS-Convoy-Effect)
- [CPU Scheduling | SJF | Priority | RR](#CPU-Scheduling-SJF-Priority-RR)
- [MLQ | MLFQ](#MLQ-MLFQ)

#### 🪵 Synchronization
- [Introduction to Concurrency](#Introduction-to-Concurrency)
- [Critical Section Problem and How to address it](#Critical-Section-Problem-and-How-to-address-it)
- [Conditional Variable and Semaphores for Threads synchronization](#Conditional-Variable-and-Semaphores-for-Threads-synchronization)
- [The Dining Philosophers problem](#The-Dining-Philosophers-problem)
- [Deadlock Part-1](#Deadlock-Part-one)
- [Deadlock Part-2](#Deadlock-Part-two)

#### 🪵 Memory Management
- [Memory Management Techniques Contiguous Memory Allocation](#Memory-Management-Techniques-Contiguous-Memory-Allocation)
- [Free Space Management](#Free-Space-Management)
- [Paging Non Contiguous Memory Allocation](#Paging-Non-Contiguous-Memory-Allocation)
- [Segmentation Non-Contiguous Memory Allocation](#Segmentation-Non-Contiguous-Memory-Allocation)
- [What is Virtual Memory Demand Paging Page Faults](#What-is-Virtual-Memory-Demand-Paging-Page-Faults)
- [Page Replacement Algorithms](#Page-Replacement-Algorithms)
- [Thrashing](#Thrashing)

#### 🪵 File System 
- File concept
- File attributes
- File allocation methods
- Directory structure
- Disk scheduling

```
4 Key Topics:
Processes & Threads
CPU Scheduling
Deadlocks & Prevention
Memory Management

Know standard OS problems (e.g. Producer-Consumer)

Understand how OS solves concurrency & memory issues
```

# Harware and Software

## **Where the OS Actually Lives**

The OS exists in **two places depending on system state**:

* Disk = storage (permanent)
* RAM = execution (temporary, fast)

## **When System is OFF → OS on Disk**

* The OS is stored as **files on storage (SSD/HDD)**
* Nothing is running

### **What exists on disk**

* Kernel (core of OS)
* Bootloader
* System libraries
* Drivers

So at this stage:

* OS = **just data (files)**
* CPU is not executing anything

### **When System Turns ON → OS moves to RAM** **Step-by-step process**

### **1. Power ON**

* CPU starts executing firmware (**BIOS/UEFI**)
* Firmware is stored on motherboard (ROM)

### **2. Bootloader Loads**

* BIOS/UEFI loads **bootloader** (like GRUB) from disk
* Bootloader decides which OS to load

### **3. Kernel Loaded into RAM**

* Bootloader loads **kernel from disk → RAM**
* Kernel is decompressed and prepared

### **4. Kernel Starts Running**

* Kernel:

  * Initializes hardware
  * Sets up memory
  * Switches CPU mode (protected mode)

### **5. OS Becomes Active**

* Kernel starts first process (like `init` or `systemd`)
* Now full OS is running


**Application software** performs specific task for the user. <br>
**System software** operates and controls the computer system and provides a platform to run
application software. <br>


## Definiton

#### Why OS?
* resourse managment
* bulky apps, hardware interaction code writing problem
* memory isolation and protection
* avoid (do not repeat youself) voilation

#### What is an Operating System?
* System software that manages hardware and software resources.
* Acts as interface between user and hardware.
* Provides abstraction, protection and resource management (CPU, memory, files, I/O).
* Goals: high CPU utilization, less starvation, better throughput. 
* **Operating System** is a manager , It manages 4 main things :<br>
    * 🧠 CPU → Processes + Scheduling + Synchronization + Deadlock
    * 💾 Memory → Paging + Segmentation + Virtual Memory
    * 📂 Files → File System + Disk Management
    * 💿 Devices → I/O + System Calls + Kernel Mode <br>
That’s it.<br>
Everything in OS is about managing these 4.<br>

#### An operating system function 
- Access to the computer hardware.
- interface between the user and the computer hardware
- Resource management (Aka, Arbitration) (memory, device, file, security, process etc)
- Hides the underlying complexity of the hardware. (Aka, Abstraction)
- facilitates execution of application programs by providing isolation and protection.

<img width="330" height="173" alt="image" src="https://github.com/user-attachments/assets/3a2a6feb-bcd3-4e44-89e2-5260d7c31e7c" />

## Types of OS

#### 🍂 Based on Number of Programs Executing
* Single process operating system - [MS DOS, 1981]
* Batch-processing operating system - [ATLAS, Manchester Univ., late 1950s - early 1960s]
* Multiprogramming operating system - [THE, Dijkstra, early 1960s]
* Multitasking operating system - [CTSS, MIT, early 1960s]
#### 🍂 Based on Number of CPUs
* Multi-processing operating system - [Windows NT]
#### 🍂 Based on System Architecture
* Distributed system - [LOCUS]
#### 🍂 Based on Time Constraints
* Real time OS - [ATCS]

### **Single	process	OS**	
only	1	process	executes	at	a	time	from	the	ready	queue. <br>
Basis → Only ONE program runs at a time. <br>
CPU handles one job. No parallel feeling. <br>

### **Batch-processing	OS**	
1. Firstly, user prepares his job using punch cards. 
2. Then, he submits the job to the computer operator.
3. Operator collects the jobs from different users and sort the jobs into batches with
similar needs.
4. Then, operator submits the batches to the processor one by one.
5. All the jobs of one batch are executed together.

- Priorities cannot be set, if a job comes with some higher priority.
- May lead to starvation. (A batch may take more time to complete)
- CPU may become idle in case of I/O operations.
<br>
Basis → Jobs are collected and executed in batches. <br>
No user interaction during execution. <br>

<img width="650" height="209" alt="image" src="https://github.com/user-attachments/assets/b1d2c6ef-3ad4-4d43-9225-ca9b80371d60" />

### **Multiprogramming** 
increases CPU utilization by keeping multiple jobs (code and data) in thememory so that the CPU always has one to execute in case some job gets busy with I/O.
- Single CPU
- Context switching for processes.
- Switch happens when current process goes to wait state.
- CPU idle time reduced. <br>
Basis → Multiple programs are kept in memory. <br>
When one waits (I/O), CPU switches to another. <br>
Goal → Increase CPU utilization. <br>

### **Multitasking**
is a logical extension of multiprogramming.
- Single CPU
- Able to run more than one task simultaneously.
- Context switching and time sharing used.
- Increases responsiveness.
- CPU idle time is further reduced. <br>
Basis → CPU switches very fast between tasks to give illusion of parallelism. <br>
Goal → User responsiveness. <br>

### **Multi-processing OS**
more than 1 CPU in a single computer.
- Increases reliability, 1 CPU fails, other can work
- Better throughput.
- Lesser process starvation, (if 1 CPU is working on some process, other can be executed on other CPU. <br>
Basis → Uses multiple CPUs or cores. <br>
True parallel execution. <br>

### **Distributed OS**
- OS manages many bunches of resources, >=1 CPUs, >=1 memory, >=1 GPUs, etc
- Loosely connected autonomous, interconnected computer nodes.
- collection of independent, networked, communicating, and physically separate computational nodes. <br>
Basis → Multiple computers connected, but appear as one system. <br>

### **RTOS**
- Real time error free, computations within tight-time boundaries.
- Air Traffic control system, ROBOTS etc. <br>
Basis → Strict timing requirements. <br>
Output must come within fixed deadline.<br>



### Comparison

| Type                    | CPUs                   | Main Idea                                         | Example                     |
| ----------------------- | ---------------------- | ------------------------------------------------- | --------------------------- |
| **Single Process OS**   | 1                      | Only one process runs at a time                   | MS-DOS                      |
| **Batch Processing OS** | 1                      | Jobs grouped & executed in batches                | Atlas Supervisor            |
| **Multiprogramming OS** | 1                      | Multiple jobs in memory, CPU switches on I/O wait | THE multiprogramming system |
| **Multitasking OS**     | 1                      | Time-sharing between tasks, fast switching        | CTSS                        |
| **Multiprocessing OS**  | ≥ 2                    | Multiple CPUs execute processes simultaneously    | Windows NT                  |
| **Distributed OS**      | ≥ 1 (multiple systems) | Networked independent computers act as one system | LOCUS                       |
| **Real-Time OS (RTOS)** | 1 or more              | Strict time-bound execution                       | Air Traffic Control System  |






## Multi Tasking vs Multi Threading

**Program :** A Program is an executable file which contains a certain set of instructions written to complete the specific job or operation on your computer.
* It’s a compiled code. Ready to be executed.
* Stored in Disk <br>

**Process :** Program under execution. Resides in Computer’s primary memory (RAM). <br>

**Thread :** <br>
* Single sequence stream within a process.
* An independent path of execution in a process.
* Light-weight process.
* Used to achieve parallelism by dividing a process’s tasks which are independent path
of execution.
* E.g., Multiple tabs in a browser, text editor (When you are typing in an editor, spell-checking, formatting of text and saving the text are done concurrently by multiplethreads.)



### **Table 1: Multitasking vs Multithreading**

| **Multitasking**                                                       | **Multithreading**                                                                             |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Execution of more than one task simultaneously is called multitasking. | A process is divided into multiple sub-tasks called threads, each with its own execution path. |
| Concept of more than one **process** being context switched.           | Concept of more than one **thread** being context switched.                                    |
| Number of CPU: **1**                                                   | Number of CPU: **≥ 1** (better with more than 1 CPU)                                           |
| **Isolation and memory protection exists.**                            | **No isolation and memory protection.**                                                        |
| OS allocates separate memory and resources to each process.            | OS allocates memory to a process; all threads share the same memory and resources.             |


**Thread Scheduling :** <br>
Threads are scheduled for execution based on their priority. Even though threads are executing within the runtime, all threads are assigned processor time slices by the operating system. 



### **Table 2: Thread Context Switching vs Process Context Switching**

| **Thread Context Switching**                                                               | **Process Context Switching**                                            |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| OS saves the current state of a thread and switches to another thread of the same process. | OS saves the current state of a process and switches to another process. |
| Does **not** include switching of memory address space.                                    | Includes switching of memory address space.                              |
| Program counter, registers, and stack are switched.                                        | Program counter, registers, stack, and memory space are switched.        |
| **Fast** switching.                                                                        | **Slow** switching.                                                      |
| CPU cache state is preserved.                                                              | CPU cache state is flushed.                                              |

---

## Components of OS

1. **Kernel :** A kernel is that part of the operating system which interacts directly with the hardware and performs the most crucialtasks.
a. Heart of OS/Core component
b. Very first part of OS to load on start-up.
2. **User space :** Where application software runs, apps don’t have privileged access to the underlying hardware. It interacts with kernel.
a. GUI
b. CLI
<br>
A shell, also known as a command interpreter, is that part of the operating system that receives
commands from the users and gets them executed.
<br>
<img width="536" height="536" alt="Gemini_Generated_Image_57e6vf57e6vf57e6" src="https://github.com/user-attachments/assets/3a67c8a9-515f-4f6a-bb2e-bc3d4789d03d" />

### Functions of Kernel:
1. **Process management :**
    * a. Scheduling processes and threads on the CPUs.
    * b. Creating & deleting both user and system process.
    * c. Suspending and resuming processes
    * d. Providing mechanisms for process synchronization or process communication.

2. **Memory management :**
    * a. Allocating and deallocating memory space as per need
    * b. Keeping track of which part of memory are currently being used and by which process.

3. **File management :**
    * a. Creating and deleting files.
    * b. Creating and deleting directories to organize files.
    * c. Mapping files into secondary storage.
    * d. Backup support onto a stable storage media.

4. **I/O management :** to manage and control I/O operations and I/O devices
    * a. Buffering (data copy between two devices), caching and spooling.
        * i. Spooling
            * 1. Within differing speed two jobs.
            * 2. Eg. Print spooling and mail spooling.
        * ii. Buffering
            * 1. Within one job.
            * 2. Eg. Youtube video buffering   
        * iii. Caching
            * 1. Memory caching, Web caching etc.
             



* **Process Management** : Handles creation, scheduling, execution, and coordination of processes and threads.
* **Memory Management** : Allocates, tracks, and manages memory usage among processes efficiently.
* **File Management** : Manages creation, deletion, storage, and organization of files and directories.
* **I/O Management** : Controls input/output devices and optimizes data transfer using buffering, caching, and spooling.
    * **Spooling:** Manages multiple jobs by queuing them (e.g., print queue).
    * **Buffering:** Temporarily stores data during transfer within a single process.
    * **Caching:** Stores frequently used data for faster future access.



### Types of Kernels

1. **Monolithic kernel**
    * a. All functions are in kernel itself.
    * b. Bulky in size.
    * c. Memory required to run is high.
    * d. Less reliable, one module crashes -> whole kernel is down.
    * e. High performance as communication is fast. (Less user mode, kernel mode overheads)
    * f. Eg. Linux, Unix, MS-DOS.

<img width="542" height="356" alt="image" src="https://github.com/user-attachments/assets/26ea94b7-ca7f-44ba-8f1a-226279ea8a60" />

2. **Micro Kernel**
    * a. Only major functions are in kernel.
        * i. Memory mgmt.
        * ii. Process mgmt.
    * b. File mgmt. and IO mgmt. are in User-space.
    * c. smaller in size.
    * d. More Reliable
    * e. More stable
    * f. Performance is slow.
    * g. Overhead switching b/w user mode and kernel mode.
    * h. Eg. L4 Linux, Symbian OS, MINIX etc.
   
<img width="518" height="396" alt="image" src="https://github.com/user-attachments/assets/5f564012-ad1e-4ca5-9c14-b29ee9f3cf88" />


3. **Hybrid Kernel**
    * a. Advantages of both worlds. (File mgmt. in User space and rest in Kernel space. )
    * b. Combined approach.
    * c. Speed and design of mono.
    * d. Modularity and stability of micro.
    * e. Eg. MacOS, Windows NT/7/10
    * f. IPC also happens but lesser overheads

5. **Nano/Exo kernels...**


* **Monolithic:** All-in-one, fast, bulky, less-safe
* **Microkernel:** Minimal, modular, safe, slower
* **Hybrid:** Combined, balanced, optimized, stable


* **Q. How will communication happen between user mode and kernel mode?** 
Ans. Inter process communication (IPC).
1. Two processes executing independently, having independent memory space (Memory
protection), But some may need to communicate to work.
2. Done by shared memory and message passing.

```
|--------------------------|
|      User Space          |
|  (Apps, libraries)       |
|--------------------------|
|   Kernel Space           |
|  (OS core code)          |
|--------------------------|
```

But this separation is enforced by:

* **MMU (Memory Management Unit)**

Hardware component inside CPU.

It:

* Translates virtual → physical addresses
* Prevents user code from touching kernel memory

This is not logical separation.
This is **hardware-enforced protection**.




## System Calls
**How do apps interact with Kernel?** -> using system calls. <br>

**Transitions from US to KS done by software interrupts.** <br>
**System calls** are implemented in C.<br>
**A system call** is a mechanism using which a user program can request a service from the kernel for which it does not have the permission toper form. <br>
User programs typically do not have permission to perform operations like accessing I/O devices and communicatin go the programs.<br>
**System Calls** are the only way through which a process can go into **kernel mode from user mode.** <br>

<img width="665" height="516" alt="image" src="https://github.com/user-attachments/assets/cabb5eb7-d016-4b2d-b3f6-998ab678c0c6" />

Apps **cannot directly talk to hardware or kernel**
→ They use **system calls** as a bridge

## **Example: Creating a File (Two Ways)**

### **1. GUI Method (File Explorer)**

* You right-click → New Folder
* GUI app sends request
* Internally calls system call → `mkdir()`
* Kernel creates directory

### **2. CLI Method (Terminal)**

```bash
mkdir laks
```

* You type command
* `mkdir` program runs (user space)
* It calls system call → `mkdir()`
* Kernel creates directory

### **What actually happens (behind both)**

```
User Action (GUI / CLI)
        ↓
User Space Program
        ↓
System Call (e.g., mkdir)
        ↓
Kernel Space
        ↓
File created
        ↓
Back to User Space
```

* GUI and CLI are just **different interfaces**
* Both use **same system calls internally**
* Kernel does the **actual work**
* CLI is **better for speed and control**, GUI is **better for ease**


### Types of System Calls:

#### **Process Control**

* Create and terminate processes
* Load and execute programs
* Wait for time or events, signal events
* Get/set process attributes
* Allocate and free memory

#### **File Management**

* Create and delete files
* Open and close files
* Read, write, and reposition files
* Get/set file attributes

#### **Device Management**

* Request and release devices
* Read, write, and reposition devices
* Get/set device attributes
* Attach or detach devices

#### **Information Maintenance**

* Get/set time and date
* Get/set system data
* Get/set attributes of process, file, or device

#### **Communication Management**

* Create and delete communication connections
* Send and receive messages
* Transfer status information
* Attach or detach remote devices


<img width="868" height="639" alt="image" src="https://github.com/user-attachments/assets/6f4bb47e-f62d-4e75-a553-eca46450a5a2" />


## What happens when you turn on your computer 

Power On
→ Firmware (BIOS/UEFI)
→ POST
→ Bootloader
→ Kernel
→ User Space

### 1. Power On

* You press the power button.
* Power Supply Unit (PSU) starts supplying electricity.
* CPU receives a reset signal and starts execution.

### 2. CPU Starts Firmware (BIOS / UEFI)

* CPU looks for firmware stored in ROM/flash memory on the motherboard.
* This firmware is:
  * **BIOS** : Basic Input/Output System (older systems) 
  * **UEFI** : Unified Extensible Firmware Interface (modern systems), (It replaces traditional BIOS and provides more features.)

### 3. POST (Power-On Self-Test)

Firmware performs hardware checks:

* RAM detection
* CPU check
* Keyboard, storage detection
* Basic hardware initialization

If something fails (e.g., no RAM):

* Error beep/message
* Boot process stops

### 4. Hardware Initialization

Firmware:

* Loads hardware configuration settings
* Initializes memory controller
* Detects storage devices (HDD/SSD)
* Prepares system for OS loading

### 5. Locate Boot Device

Firmware checks boot order:

Example:

1. SSD
2. USB
3. Network

It looks for:

* **MBR** (Master Boot Record) → Legacy BIOS systems
* **EFI System Partition** → UEFI systems

### 6. Load Bootloader

Firmware loads the bootloader into RAM and transfers control.

Common bootloaders:

* Windows → Windows Boot Manager (bootmgr / bootmgfw.efi)
* Linux → GRUB
* macOS → boot.efi

### 7. Bootloader Loads the Kernel

Bootloader:

* Loads OS Kernel into RAM
* Sets up initial memory structures
* Passes control to the kernel

### 8. Kernel Initialization

Kernel:

* Switches CPU to protected/long mode
* Initializes memory management
* Sets up device drivers
* Initializes process scheduler
* Mounts root filesystem

## 9️. Start User Space

Kernel starts the first user-space process:

* Linux → `init` / `systemd`
* Windows → `smss.exe`

After this:

* Services start
* Login screen appears
* Desktop loads





## 32 Bit vs 64 Bit OS

internally this is physically implemented using 32 parallel electrical lines (wires/transistors) carrying 0s and 1s. <br>
👉 Each bit = one signal line that can be ON (1) or OFF (0)
```32-bit = 32 parallel electrical signals```

1. A 32-bit OS has 32-bit registers, and it can access 2^32 unique memory addresses. i.e., 4,294,967,296 of
physical memory.
2. A 64-bit OS has 64-bit registers, and it can access 2^64 unique memory addresses. i.e.,
17,179,869,184 GB of physical memory.
3. 32-bit CPU architecture can process 32 bits of data & information.
4. 64-bit CPU architecture can process 64 bits of data & information.
* 5. Advantages of 64-bit over the 32-bit operating system: <br>
    * a. **Addressable Memory :** 32-bit CPU -> 2^32 memory addresses, 64-bit CPU -> 2^64 memory addresses.
    * b. **Resource usage :** Installing more RAM on a system with a 32-bit OS doesn't impact performance. However, upgrade that system with excess RAM to the 64 bit version of Windows, and you'll notice a difference.
    * c. **Performance :** All calculations take place in the registers. When you’re performing math in your code, operands are loaded from memory into registers. So, having larger registers allow you to perform larger calculations at the same time. 32-bit processor can execute 4 bytes of data in 1 instruction cycle while 64-bit means that processor can execute 8 bytes of data in 1 instruction cycle. (In 1 sec, there could be thousands to billons of instruction cycles depending upon a processor design)
    * d. **Compatibility :** 64-bit CPU can run both 32-bit and 64-bit OS. While 32-bit CPU can only run 32-bit OS.
    * e. **Better Graphics performance :** 8-bytes graphics calculations make graphics-intensive apps run faster.

## Storage Devices Basics

What are the different memory present in the computer system?

<img width="473" height="695" alt="image" src="https://github.com/user-attachments/assets/56be26a4-f9d5-48f7-bf11-32341731afca" />

1. **Register :** Smallest unit of storage. It is a part of CPU itself. <br>
A register may hold an instruction, a storage address, or any data (such as bit sequence or individual
characters). <br>
Registers are a type of computer memory used to quickly accept, store, and transfer data and
instructions that are being used immediately by the CPU.

3. **Cache :** Additional memory system that temporarily stores frequently used instructions and data for
quicker processing by the CPU.

5. **Main Memory :** RAM.

7. **Secondary Memory :** Storage media, on which computer can store data & programs.

##### Comparison
1. **Cost :**
    * a. Primary storages are costly.
    * b. Registers are most expensive due to expensive semiconductors & labour.
    * c. Secondary storages are cheaper than primary.
   
2. **Access Speed :**
    * a. Primary has higher access speed than secondary memory.
    * b. Registers has highest access speed, then comes cache, then main memory.

4. **Storage size :**
    * a. Secondary has more space.

6. **Volatility :**
    * a. Primary memory is volatile.
    * b. Secondary is non-volatile.


  
## Introduction to Process

**how a program becomes a running entity inside the computer.**

A process is: 
```Program + Memory + CPU State + OS resources```
When the OS starts executing a program, it becomes a process.

* Part 1 — Program vs Process
* Part 2 — How OS Creates a Process :
```
1. Load Program into Memory
OS loads:
    Program code, Global variables, Static data
from disk → RAM.

2️. Allocate Stack
Stack is used for:
    Function calls, Local variables, Return addresses
Example 
main()
  └── function1()
         └── function2()
Each call uses the stack.

3️. Allocate Heap
Heap is used for dynamic memory.
Example in C/C++:
malloc(), new
The OS provides a heap region for the process.

4️. Setup I/O
If the program uses:
    keyboard, files, network
the OS prepares these resources.

5️. OS transfers control
The CPU begins execution at:
    main()
Technically it starts at _start then reaches main().
```

* Part 3 — Process Architecture
<img width="850" height="397" alt="image" src="https://github.com/user-attachments/assets/43c3ed3f-137a-49f3-9387-2ad848184530" />


5. **Architecture** of process:

```
Both stack and heap change size while the program runs.
Stack grows downward
When functions are called:
    main()
      ↓
    func1()
      ↓
    func2()
Each call pushes a stack frame.
So stack keeps expanding downwards.
Heap grows upward
Heap grows when dynamic memory is allocated.
Example:
    malloc()
    new
Each allocation increases heap size upwards.

if one grows too much:
    stack overflow
    heap overflow
they might collide.
So the OS keeps large free space between them.
This allows both to grow safely.
```

* **Attributes** of process:
    * a. Feature that allows identifying a process uniquely.
    * b. Process table
        * i. All processes are being tracked by OS using a table like data structure.
        * ii. Each entry in that table is process control block (PCB).
    * c. PCB: Stores info/attributes of a process.
        * i. Data structure used for each process, that stores information of a process such as process id, program counter, process state, priority etc.

* Part 4 — Process Identification
* Part 5 — Process Table
```
The OS keeps track of processes using a structure called:
Process Table
Think of it like:
----------------------------------
| PID | STATE | MEMORY | PRIORITY |
----------------------------------
|101  | RUN   | 200MB  | 5        |
|102  | WAIT  | 120MB  | 3        |
|103  | READY | 80MB   | 4        |
----------------------------------
Each row represents one process.
```

* Part 6 — Process Control Block (PCB)
```
Each process has a PCB.
PCB = data structure containing all process information.
Stored inside the process table.
PCB Stores
Typical PCB fields:
    Process ID
    Process State
    Program Counter
    CPU Registers
    Memory Info
    Scheduling Priority
    Open Files
PCB is used during context switching.
```
  
**PCB structure :**

<img width="776" height="438" alt="image" src="https://github.com/user-attachments/assets/2063a074-62e8-4962-9664-8add42d59036" />

**Registers in the PCB** : it is a data structure. When a processes is running and it's time slice expires, the
current value of process specific registers would be stored in the PCB and the process would be swapped
out. When the process is scheduled to be run, the register values is read from the PCB and written to the
CPU registers. This is the main purpose of the registers in the PCB.

1. What is a program? Compiled code, that is ready to execute.
2. What is a process? Program under execution.
3. How OS creates a process? Converting program into a process. 







## Process States Process Queues

1. **Process States :** As process executes, it changes state. Each process may be in one of the following
states.
    * a. **New :** OS is about to pick the program & convert it into process. OR the process is being
created.
    * b. **Run :** Instructions are being executed; CPU is allocated.
    * c. **Waiting :** Waiting for IO.
    * d. **Ready :** The process is in memory, waiting to be assigned to a processor.
    * e. **Terminated :** The process has finished execution. PCB entry removed from process table.
  
<img width="776" height="323" alt="image" src="https://github.com/user-attachments/assets/9bae4967-62bd-47fc-a1e5-43448409fed0" />


2. **Process Queues :**
    * a. **Job Queue :**
        * i. Processes in new state.
        * ii. Present in secondary memory.
        * iii. Job Schedular (Long term schedular (LTS)) picks process from the pool and loads them into memory for execution.
    * b. **Ready Queue :**
        * i. Processes in Ready state.
        * ii. Present in main memory.
        * iii. CPU Schedular (Short-term schedular) picks process from ready queue and dispatch it to CPU.
    * c. **Waiting Queue :**
        * i. Processes in Wait state.

3. **Degree of multi-programming :** The number of processes in the memory.
    * a. LTS controls degree of multi-programming.

4. **Dispatcher :** The module of OS that gives control of CPU to a process selected by STS.

## Swapping Context Switching Orphan process Zombie process

## **Swapping**

### 1. Definition

**Swapping** is a memory management technique in which a process is **temporarily moved from main memory (RAM) to secondary storage (disk)** so that memory can be freed for other processes.
Later, the process can be **brought back into RAM and resume execution from where it stopped**.


### 2. Why Swapping is Needed

Swapping is used when:

* The system has **too many processes in memory**.
* The **available RAM becomes insufficient**.
* The OS wants to **improve process scheduling and system performance**.

This helps the system maintain a **better process mix** and continue running smoothly.

### 3. Role of Medium-Term Scheduler (MTS)

In **time-sharing systems**, the **Medium-Term Scheduler** manages swapping.

### Responsibilities of MTS:

* **Select processes to remove from memory**
* **Swap out processes to disk**
* **Swap in processes back to RAM when needed**

This helps control the **degree of multiprogramming**.

### 4. Degree of Multiprogramming

**Degree of multiprogramming** =
Number of processes **present in main memory at the same time**.

If too many processes are loaded:

* Memory becomes overloaded
* System performance decreases

So the OS **reduces the degree of multiprogramming by swapping some processes out**.



### 5. Swapping Operations

#### Swap Out

* Process is **moved from RAM → Disk**
* Memory space becomes available

#### Swap In

* Process is **brought back from Disk → RAM**
* Execution continues from where it stopped



### 6. Swapping Process Flow

```
Process in RAM
      ↓
Medium-Term Scheduler decides
      ↓
Process swapped out to Disk
      ↓
Memory becomes free
      ↓
Later OS needs the process
      ↓
Process swapped back into RAM
      ↓
Execution resumes
```

    * f. Swapping is a mechanism in which a process can be swapped temporarily out of main memory (or move) to secondary storage (disk) and make that memory available to other processes. At some later time, the system swaps back the process from the secondary storage to main memory.

<img width="1274" height="509" alt="image" src="https://github.com/user-attachments/assets/31cc472a-f615-44a5-bcb5-d34d5ee9f20f" />
<br>

## **Context-Switching**

**Context Switching** is the process where the CPU **stops executing one process and starts executing another process**.
To do this, the operating system **saves the state of the current process and loads the state of the next process**.

* b. During this event, the **kernel saves the CPU context of the currently running process into its PCB and loads the saved context of the next scheduled process from its PCB into the CPU registers**.
* c. It is **pure overhead**, because the system does no useful work during the switch.
* d. Speed varies from machine to machine depending on **memory speed, number of CPU registers, and OS implementation**.

### What is Saved (Context)

The **context** includes:

* CPU registers
* Program Counter (PC)
* Process state
* Stack pointer

These values are stored inside the **Process Control Block (PCB)**.

### Performance Factors

The **speed of context switching depends on**:

* CPU architecture
* Number of registers to save
* Memory speed
* OS implementation

### Simple Flow

```
Process A running
      ↓
Interrupt / Scheduler decision
      ↓
Save Process A context → PCB
      ↓
Load Process B context → CPU
      ↓
Process B starts running
```
   

### Orphan Process

* **Definition:**
  A process whose **parent process has terminated while the child process is still running**.

* **Adoption:**
  The orphan process is **adopted by the `init` process (PID 1)**.

* **Reason:**
  The **init process becomes the new parent** and is responsible for **managing and cleaning up the child when it terminates**.

* **Note:**
  `init` is the **first process started by the operating system during boot**.

👉 **Parent dies → child continues → init adopts it.**

  
### Zombie Process / Defunct Process

* **Definition:**
  A process whose **execution has finished but its entry still exists in the process table**.

* **Why it happens:**
  The **parent process has not yet read the child's exit status**.

* **Reason:**
  The OS **keeps the process entry (PCB)** so the parent can retrieve the **termination status**.

* **Removal (Reaping):**
  When the **parent process calls `wait()`**, it reads the child’s exit status and the **OS removes the zombie from the process table**.

* **Note:**
  If the parent delays calling `wait()`, the **terminated child remains a zombie** until it is reaped.

👉 **Child terminates → parent hasn’t called `wait()` → process becomes zombie.**


## Intro to Process Scheduling FCFS Convoy Effect

* **Process Scheduling**
    * Basis of Multi-programming OS.
    * By switching the CPU among processes, the OS can make the computer more productive.
    * Many processes are kept in memory at a time, when a process must wait or time quantum expires, the OS takes the CPU away from that process & gives the CPU to another process & this pattern continues.

* **CPU Scheduler**
    * Whenever the CPU become ideal, OS must select one process from the ready queue to be executed.
    * Done by STS.

### sheduling 

Preemptive Scheduling : The operating system can interrupt a running process and allocate the CPU to another process. <br>
Non-Preemptive scheduling : Once a process gets the CPU, it keeps it until it finishes execution or voluntarily releases it.<br>

* **Non-Preemptive scheduling**
    * Once CPU has been allocated to a process, the process keeps the CPU until it releases CPU either by terminating or by switching to wait-state.
    * Starvation, as a process with long burst time may starve less burst time process.
    * Low CPU utilization.

* **Preemptive scheduling**
    * a. CPU is taken away from a process after time quantum expires along with terminating or switching to wait-state.
    * b. Less Starvation
    * c. High CPU utilization.

* **Goals of CPU scheduling**
    * a. Maximum CPU utilization
    * b. Minimum Turnaround time (TAT).
    * c. Min. Wait-time
    * d. Min. response time.
    * e. Max. throughput of system.

* **Throughput :** No. of processes completed per unit time.
* **Arrival time (AT) :** Time when process is arrived at the ready queue.
* **Burst time (BT) :** The time required by the process for its execution.
* **Turnaround time (TAT) :** Time taken from first time process enters ready state till it terminates. (CT - AT)
* **Wait time (WT) :** Time process spends waiting for CPU. (WT = TAT – BT)
* **Response time :** Time duration between process getting into ready queue and process getting CPU for the first time.
* **Completion Time (CT) :** Time taken till process gets terminated.
* **FCFS (First come-first serve) :**
    * Whichever process comes first in the ready queue will be given CPU first.
    * In this, if one process has longer BT. It will have major effect on average WT of diff processes, called Convoy effect.
    * **Convoy Effect :** is a situation where many processes, who need to use a resource for a short time, are blocked by one process holding that resource for a long time.
  


## CPU Scheduling SJF Priority RR

## 1️. Shortest Job First (SJF)

### Non-Preemptive SJF

#### Definition

The process with the **smallest Burst Time (BT)** is selected and executed **until completion**.

#### Characteristics

* Process with **least BT gets CPU first**.
* Requires **estimation of burst time**, which is difficult in practice.
* Once a process starts executing, it **cannot be interrupted**.

#### Issues

* **Convoy Effect:**
  If a very long job arrives first, shorter jobs must wait.
* **Starvation:**
  Long processes may wait indefinitely if short jobs keep arriving.

#### Scheduling Criteria

Uses:

```
Arrival Time (AT) + Burst Time (BT)
```

### Preemptive SJF

(Also called **Shortest Remaining Time First – SRTF**)

#### Definition

The CPU is always assigned to the process with the **shortest remaining burst time**.

#### Characteristics

* If a **new process arrives with shorter remaining time**, the current process is **preempted**.
* Reduces waiting time for short jobs.

#### Advantages

* **Less starvation compared to non-preemptive SJF**
* **No convoy effect**
* Gives **minimum average waiting time** for a given set of processes.

## 2. Priority Scheduling

Processes are scheduled based on **priority values**.

### Non-Preemptive Priority Scheduling

#### Characteristics

* Priority is **assigned when the process is created**.
* CPU is allocated to the **highest priority process**.
* Once a process starts running, it **continues until completion**.

#### Note

* **SJF is a special case of priority scheduling** where:

```
Priority ∝ 1 / Burst Time
```

(shorter job → higher priority)

### Preemptive Priority Scheduling

#### Characteristics

* If a **higher priority process arrives**, the currently running process is **preempted**.
* CPU is given to the higher priority process immediately.

#### Issue

* **Starvation (Indefinite Waiting)**
  Low-priority processes may never get CPU time.

#### Solution: Aging

**Aging** gradually increases the priority of waiting processes.

Example:

```
Increase priority by 1 every 15 minutes
```

This ensures long-waiting processes eventually run.

## 3️. Round Robin Scheduling (RR)

#### Definition

Each process gets CPU for a **fixed time slice called Time Quantum (TQ)**.

#### Characteristics

* Similar to **FCFS but preemptive**
* Designed for **time-sharing systems**
* Each process gets CPU **in cyclic order**

#### Scheduling Criteria

Uses:

```
Arrival Time (AT) + Time Quantum (TQ)
```

It **does not depend on Burst Time**.

#### Advantages

* **Very low starvation**
* **No convoy effect**
* **Fair CPU distribution**
* **Easy to implement**

#### Disadvantage

* If **Time Quantum is too small**:

  * Frequent **context switches**
  * Higher **overhead**


| Algorithm   | Preemption | Key Idea                | Main Issue              |
| ----------- | ---------- | ----------------------- | ----------------------- |
| SJF         | No         | Shortest job first      | Starvation              |
| SRTF        | Yes        | Shortest remaining time | Complexity              |
| Priority    | Both       | Highest priority first  | Starvation              |
| Round Robin | Yes        | Fixed time slice        | Context switch overhead |


<img width="454" height="526" alt="image" src="https://github.com/user-attachments/assets/67341e19-3740-4e31-9d04-170ab799d6c8" />




## MLQ MLFQ

* Multi-level queue scheduling (**MLQ**)
    * a. Ready queue is divided into multiple queues depending upon priority.
    * b. A process is permanently assigned to one of the queues (inflexible) based on some property of process, memory, size, process priority or process type.
    * c. Each queue has its own scheduling algorithm. E.g., SP -> RR, IP -> RR & BP -> FCFS.
    * d. System process: Created by OS (Highest priority) <br>
         Interactive process (Foreground process): Needs user input (I/O). <br>
         Batch process (Background process): Runs silently, no user input required.
    * e. Scheduling among different sub-queues is implemented as fixed priority preemptive scheduling. E.g., foreground queue has absolute priority over background queue.
    * f. If an interactive process comes & batch process is currently executing. Then, batch process will be preempted.
    * g. Problem: Only after completion of all the processes from the top-level ready queue, the further level ready queues will be scheduled. This came starvation for lower priority process.
    * h. Convoy effect is present.
 
<img width="635" height="347" alt="image" src="https://github.com/user-attachments/assets/f18db95d-a4f0-47b6-bcec-cebb2324bb8b" />
    

* Multi-level feedback queue scheduling (MLFQ)
    * a. Multiple sub-queues are present.
    * b. Allows the process to move between queues. The idea is to separate processes according to the characteristics of their BT. If a process uses too much CPU time, it will be moved to lower priority queue. This scheme leaves I/O bound and interactive processes in the higher-priority queue. In addition, a process that waits too much in a lower-priority queue may be moved to a higher priority queue. This form of ageing prevents starvation.
    * c. Less starvation then MLQ.
    * d. It is flexible.
    * e. Can be configured to match a specific system design requirement.
 
<img width="354" height="401" alt="image" src="https://github.com/user-attachments/assets/43e45b9e-1fbc-4a46-b4dd-1cadfa3d5610" />

<img width="1047" height="250" alt="image" src="https://github.com/user-attachments/assets/ded7077c-87d2-467c-a5a6-6011bf77190c" />

## Introduction to Concurrency

* **Concurrency :** is the execution of the multiple instruction sequences at the same time. It happens in the operating system when there are several process threads running in parallel.
* **Thread :**
    * Single sequence stream within a process.
    * An independent path of execution in a process.
    * Light-weight process.
    * Used to achieve parallelism by dividing a process’s tasks which are independent path of execution.
    * E.g., Multiple tabs in a browser, text editor (When you are typing in an editor, spell checking, formatting of text and saving the text are done concurrently by multiple threads.)

* **Thread Scheduling :** Threads are scheduled for execution based on their priority. Even though
threads are executing within the runtime, all threads are assigned processor time slices by the
operating system.

* **Threads context switching**
    * OS saves current state of thread & switches to another thread of same process.
    * Doesn’t includes switching of memory address space. (But Program counter, registers & stack are included.)
    * Fast switching as compared to process switching
    * CPU’s cache state is preserved.

* **How each thread get access to the CPU?**
    * Each thread has its own program counter.
    * Depending upon the thread scheduling algorithm, OS schedule these threads.
    * OS will fetch instructions corresponding to PC of that thread and execute instruction.
      
* I**I/O or TQ, based context switching is done here as well**
    * We have TCB (Thread control block) like PCB for state storage management while performing context switching.

* **Will single CPU system would gain by multi-threading technique?**
    * Never.
    * As two threads have to context switch for that single CPU.
    * This won’t give any gain.

* **Benefits of Multi-threading**
    * Responsiveness
    * Resource sharing: Efficient resource sharing.
    * Economy: It is more economical to create and context switch threads.
        * 1. Also, allocating memory and resources for process creation is costly, so better to divide tasks into threads of same process.
    * Threads allow utilization of multiprocessor architectures to a greater scale and efficiency.

* **code**
```cpp
#include <iostream>
#include <thread>
#include <unistd.h>

using namespace std;

void taskA() {
    for (int i = 0; i < 10; ++i) {
        sleep(1);
        printf("TaskA: %d\n", i);
        fflush(stdout);
    }
}

void taskB() {
    for (int i = 0; i < 10; ++i) {
        sleep(1);
        printf("TaskB: %d\n", i);
        fflush(stdout);
    }
}

int main() {

    thread t1(taskA);
    thread t2(taskB);

    t1.join();
    t2.join();

    return 0;
}
```














## Critical Section Problem and How to address it

Process synchronization techniques play a key role in maintaining the consistency of shared data <br>
* **Critical Section (C.S)**
    * The critical section refers to the segment of code where processes/threads access shared resources, such as common variables and files, and perform write operations on them. Since processes/threads execute concurrently, any process can be interrupted mid-execution.

* **Major Thread scheduling issue**
    * a. Race Condition
        * i. A race condition occurs when two or more threads can access shared data and they try to change it at the same time. Because the thread scheduling algorithm can swap between threads at any time, you don't know the order in which the threads will attempt to access the shared data. Therefore, the result of the change in data is dependent on the thread scheduling algorithm, i.e., both threads are "racing" to access/change the data.

* **Solution to Race Condition**
    * a. Atomic operations: Make Critical code section an atomic operation, i.e., Executed in one CPU cycle.
    * b. Mutual Exclusion using locks.
    * c. Semaphores

* Can we use a simple flag variable to solve the problem of race condition?
     * a. No.

* **Peterson’s solution** can be used to avoid race condition but holds good for only 2 process/threads.

* **Mutex/Locks**
    * a. Locks can be used to implement mutual exclusion and avoid race condition by allowing only one thread/process to access critical section.
    * b. Disadvantages:
        * i. Contention: one thread has acquired the lock, other threads will be busy waiting, what if thread that had acquired the lock dies, then all other threads will be in infinite waiting.
        * ii. Deadlocks
        * iii. Debugging
        * iv. Starvation of high priority threads.


### Race Condition (Wrong Code)

```cpp
#include <iostream>
#include <thread>
using namespace std;

int count = 0;

void task() {
    for (int i = 0; i < 1000000; i++) {
        count++;   // ❌ race condition
    }
}

int main() {
    thread t1(task);
    thread t2(task);

    t1.join();
    t2.join();

    cout << "Final Count: " << count << endl;
    return 0;
}
```

👉 Output: unpredictable ❌

### Solution 1: Mutex (Correct & Standard)

```cpp
int count = 0;
mutex mtx;

void task() {
    for (int i = 0; i < 1000000; i++) {
        mtx.lock();
        count++;
        mtx.unlock();
    }
}
```

### Solution 2: lock_guard (Best Practice)

```cpp
int count = 0;
mutex mtx;

void task() {
    for (int i = 0; i < 1000000; i++) {
        lock_guard<mutex> lock(mtx);  // auto lock/unlock
        count++;
    }
}
```

### Solution 3: Atomic (Fastest)

```cpp
atomic<int> count(0);

void task() {
    for (int i = 0; i < 1000000; i++) {
        count++;   // thread-safe
    }
}
```

* ❌ Race condition → no synchronization
* ✅ Mutex → safe but slower
* ✅ lock_guard → safest + clean
* ⚡ Atomic → fastest (limited use)
















## Conditional Variable and Semaphores for Threads synchronization

* **Conditional variable**
    * a. The condition variable is a synchronization primitive that lets the thread wait until a certain condition occurs.
    * b. Works with a lock
    * c. Thread can enter a wait state only when it has acquired a lock. When a thread enters the wait state, it will release the lock and wait until another thread notifies that the event has occurred. Once the waiting thread enters the running state, it again acquires the lock immediately and starts executing.
    * d. Why to use conditional variable?
        * i. To avoid busy waiting.
    * e. Contention is not here.


```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <chrono>
using namespace std;

mutex mtx;                 // protects shared data
condition_variable cv;     // used for waiting & notifying
bool done = false;         //condition flag 

void task1() {
    unique_lock<mutex> lock(mtx);            // Locks the mutex (critical section starts)

    // first thread does work
    for (int i = 0; i < 5; i++) {
        cout << "t1 working..." << endl;
        this_thread::sleep_for(chrono::seconds(1));
    }

    done = true;
    cout << "Signaling condition variable (t1)" << endl;

    cv.notify_all();  // wake up waiting threads
}

void task2() {
    unique_lock<mutex> lock(mtx);

    cout << "t2 waiting..." << endl;

    // wait until condition becomes true
    cv.wait(lock, [] { return done; });       // Releases lock, Goes to sleep, Wakes when notified, Re-checks condition (done == true)

    cout << "Condition met (t2)" << endl;
}

int main() {
    thread t1(task1);
    thread t2(task2);

    t1.join();
    t2.join();

    return 0;
}
```
* Without condition variable: <br>
❌ Thread keeps checking (busy waiting) <br>
while(!done) { } <br>
👉 wastes CPU <br><br>

* With condition variable: <br>
✅ Thread sleeps efficiently <br>
👉 CPU not wasted <br><br>

* Important Rule <br>
👉 Always use with mutex + condition <br>
mutex mtx; <br>
condition_variable cv; <br>









* **Semaphores**
    * a. Synchronization method.
    * b. An integer that is equal to number of resources
    * c. Multiple threads can go and execute C.S concurrently.
    * d. Allows multiple program threads to access the finite instance of resources whereas mutex allows multiple threads to access a single shared resource one at a time.
    * e. Binary semaphore: value can be 0 or 1
    * i. Aka, mutex locks
    * f. Counting semaphore
        * i. Can range over an unrestricted domain.
        * ii. Can be used to control access to a given resource consisting of a finite number of instances.
    * g. To overcome the need for busy waiting, we can modify the definition of the wait () and signal () semaphore operations. When a process executes the wait () operation and finds that the semaphore value is not positive, it must wait. However, rather than engaging in busy waiting, the process car block itself. The block- operation places a process into a waiting queue associated with the semaphore, and the state of the process is switched to the Waiting state. Then control is transferred to the CPU scheduler, which selects another process to execute.
    * h. A process that is blocked, waiting on a semaphore S, should be restarted when some other process executes a signal () operation. The process is restarted by a wakeup () operation, which changes the process from the waiting state to the ready state. The process is then placed in the ready queue.

```cpp
#include <iostream>
#include <thread>
#include <semaphore>
#include <chrono>

using namespace std;

counting_semaphore<2> sem(2);

void task(string name) {
    for (int i = 0; i < 5; i++) {

        sem.acquire();

        cout << name << " working " << i << endl;

        sem.release();

        this_thread::sleep_for(chrono::milliseconds(200));
        this_thread::yield();  // force switching
    }
}

int main() {
    thread t1(task, "T1");
    thread t2(task, "T2");
    thread t3(task, "T3");
    thread t4(task, "T4");
    thread t5(task, "T5");

    t1.join();
    t2.join();
    t3.join();
    t4.join();
    t5.join();
}
```

## producer consumer problem and its solution 

There are **two types of processes (threads)**:
* **Producer** → creates data
* **Consumer** → uses (removes) data
👉 Both share a **common buffer (like a box)**
   Real-life Example : Chef 👨‍🍳 (Producer) → cooks food, Customer 🍽️ (Consumer) → eats food, Table = buffer

### The Problem

There are **2 main issues**:

* 1. Buffer Overflow : Producer keeps adding even when buffer is full, No space → problem
* 2. Buffer Underflow : Consumer tries to remove when buffer is empty, Nothing to consume → problem
* 3. Race Condition : Both access buffer at same time, Data becomes wrong

## Solution (Using Semaphores)

We use **3 tools**:

### 1. `empty`
Counts empty slots
* Initially = buffer size
* Decreases when producer adds

### 2. `full`
Counts filled slots
* Initially = 0
* Increases when producer adds

### 3. `mutex` 
Ensures **only one thread accesses buffer**

### How Producer Works

Step-by-step:

```text
wait(empty)   → check space
wait(mutex)   → lock buffer

add item      → put data

signal(mutex) → unlock
signal(full)  → increase filled slots
```

### How Consumer Works

```text
wait(full)    → check data exists
wait(mutex)   → lock buffer

remove item   → take data

signal(mutex) → unlock
signal(empty) → increase empty slots
```
```cpp
#include <iostream>
#include <thread>
#include <semaphore>
#include <vector>
#include <chrono>

using namespace std;

const int BUFFER_SIZE = 5;

vector<int> buffer;
counting_semaphore<BUFFER_SIZE> empty(BUFFER_SIZE); // empty slots
counting_semaphore<BUFFER_SIZE> full(0);            // filled slots
binary_semaphore mtx(1);                            // mutex

// Producer
void producer() {
    int item = 0;

    while (true) {
        this_thread::sleep_for(chrono::milliseconds(500));

        empty.acquire();   // wait(empty)
        mtx.acquire();     // wait(mutex)

        buffer.push_back(item);
        cout << "Produced: " << item << endl;
        item++;

        mtx.release();     // signal(mutex)
        full.release();    // signal(full)
    }
}

// Consumer
void consumer() {
    while (true) {
        full.acquire();    // wait(full)
        mtx.acquire();     // wait(mutex)

        int item = buffer.back();
        buffer.pop_back();
        cout << "Consumed: " << item << endl;

        mtx.release();     // signal(mutex)
        empty.release();   // signal(empty)

        this_thread::sleep_for(chrono::milliseconds(800));
    }
}

int main() {
    thread p(producer);
    thread c(consumer);

    p.join();
    c.join();

    return 0;
}
```

## reader writer 

Two types of processes:
* **Readers** → only read data
* **Writers** → modify data


### Problem

We must follow rules:

#### ✅ Allowed:

* Multiple **readers together** 
* Only **one writer at a time** 

#### ❌ Not allowed:

* Writer + reader together 
* Two writers together 

### Idea of Solution (from your image)

We use:
* `mutex` → protect `readCount`
* `wrt` → control access to shared data
* `readCount` → number of active readers

### Logic

#### Reader

```text
wait(mutex)
readCount++
if first reader → lock writer
signal(mutex)

READ

wait(mutex)
readCount--
if last reader → unlock writer
signal(mutex)
```

#### Writer

```text
wait(wrt)

WRITE

signal(wrt)
```

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <semaphore>
#include <chrono>

using namespace std;

int readCount = 0;

binary_semaphore mutex(1); // protects readCount
binary_semaphore wrt(1);   // controls writer access

// Reader
void reader(int id) {
    while (true) {
        // Entry section
        mutex.acquire();
        readCount++;

        if (readCount == 1) {
            wrt.acquire(); // first reader blocks writers
        }

        mutex.release();

        // Critical Section (Reading)
        cout << "Reader " << id << " is reading\n";
        this_thread::sleep_for(chrono::milliseconds(500));

        // Exit section
        mutex.acquire();
        readCount--;

        if (readCount == 0) {
            wrt.release(); // last reader allows writers
        }

        mutex.release();

        this_thread::sleep_for(chrono::milliseconds(500));
    }
}

// Writer
void writer(int id) {
    while (true) {
        wrt.acquire(); // only one writer at a time

        // Critical Section (Writing)
        cout << "Writer " << id << " is writing\n";
        this_thread::sleep_for(chrono::milliseconds(800));

        wrt.release();

        this_thread::sleep_for(chrono::milliseconds(1000));
    }
}

int main() {
    thread r1(reader, 1);
    thread r2(reader, 2);
    thread r3(reader, 3);

    thread w1(writer, 1);

    r1.join();
    r2.join();
    r3.join();
    w1.join();

    return 0;
}
```

### Key Understanding

| Concept      | Meaning                  |
| ------------ | ------------------------ |
| `readCount`  | number of active readers |
| first reader | blocks writers           |
| last reader  | allows writers           |
| `wrt`        | ensures only one writer  |

#### Output Behavior

```
Reader 1 is reading
Reader 2 is reading   // multiple readers
Reader 3 is reading

Writer 1 is writing   // only after readers finish
```







## The Dining Philosophers problem

There are **5 philosophers** sitting around a table <br>
Each has:
* Food (in center)
* 2 forks (left + right)

### Problem

To eat: <br>
Philosopher needs **both forks**

### Issues

#### 1. Deadlock

All pick **left fork** → wait for right → stuck forever 

#### 2. Starvation

One philosopher may **never get forks** ❌

### Goal

No deadlock
No starvation
Fair access

### Simple Solution Idea

Use **semaphore (or mutex)** to control forks
AND limit number of philosophers eating

### Best Easy Solution (Avoid Deadlock)

Allow only **4 philosophers at a time**

```text
room semaphore = 4
```

### Logic

#### Philosopher:

```text id="n2g0b4"
wait(room)

wait(left fork)
wait(right fork)

EAT

signal(left fork)
signal(right fork)

signal(room)
```

* full code

```cpp id="m3v8rm"
#include <iostream>
#include <thread>
#include <semaphore>
#include <vector>
#include <chrono>

using namespace std;

const int N = 5;

// one semaphore per fork
binary_semaphore forks[5] = {
    binary_semaphore(1),
    binary_semaphore(1),
    binary_semaphore(1),
    binary_semaphore(1),
    binary_semaphore(1)
};

// limit philosophers (avoid deadlock)
counting_semaphore<4> room(4);

void philosopher(int id) {
    while (true) {
        cout << "Philosopher " << id << " is thinking\n";
        this_thread::sleep_for(chrono::milliseconds(500));

        room.acquire(); // enter room

        forks[id].acquire();                 // left fork
        forks[(id + 1) % N].acquire();       // right fork

        cout << "Philosopher " << id << " is eating\n";
        this_thread::sleep_for(chrono::milliseconds(500));

        forks[id].release();
        forks[(id + 1) % N].release();

        room.release(); // leave room
    }
}

int main() {
    vector<thread> philosophers;

    for (int i = 0; i < N; i++) {
        philosophers.push_back(thread(philosopher, i));
    }

    for (auto &t : philosophers) {
        t.join();
    }

    return 0;
}
```
#### Output Behavior

```id="gvdmyn"
Philosopher 1 is thinking
Philosopher 2 is eating
Philosopher 3 is eating
...
```

<img width="431" height="434" alt="image" src="https://github.com/user-attachments/assets/7f76c77a-3085-476b-a8ba-d0e7525125ee" />

* We have 5 philosophers.
* They spend their life just being in **two states:**
    * **a. Thinking**
    * **b. Eating**

* They sit on a circular table surrounded by 5 chairs (1 each), in the center of table is a bowl of noodles, and the table is laid with 5 single forks.
* Thinking state: When a ph. Thinks, he doesn’t interact with others.
* Eating state: When a ph. Gets hungry, he tries to pick up the 2 forks adjacent to him (Left and Right). He can pick one fork at a time.
* One can’t pick up a fork if it is already taken.
* When ph. Has both forks at the same time, he eats without releasing forks.
* Solution can be given using semaphores.
   * a. Each fork is a binary semaphore.
   * b. A ph. Calls wait() operation to acquire a fork.
   * c. Release fork by calling signal().
   * d. Semaphore fork[5]{1};
   
* Although the semaphore solution makes sure that no two neighbors are eating simultaneously but it could still create Deadlock.
* Suppose that all 5 ph. Become hungry at the same time and each picks up their left fork, then All fork semaphores would be 0.
* When each ph. Tries to grab his right fork, he will be waiting for ever (Deadlock)
* We must use some methods to avoid Deadlock and make the solution work
    * a. Allow at most 4 ph. To be sitting simultaneously.
    * b. Allow a ph. To pick up his fork only if both forks are available and to do this, he must pick them up in a critical section (atomically).
    * c. **Odd-even rule** <br> an odd ph. Picks up first his left fork and then his right fork, whereas an even ph. Picks up his right fork then his left fork.

* Hence, only semaphores are not enough to solve this problem. <br>
We must add some enhancement rules to make deadlock free solution.













## Deadlock Part one

* In Multi-programming environment, we have several processes competing for finite number of
resources
* Process requests a resource (R), if R is not available (taken by other process), process enters in a waiting state. Sometimes that waiting process is never able to change its state because the resource, it has requested is busy (forever), called DEADLOCK (DL)
* Two or more processes are waiting on some resource’s availability, which will never be available as it is also busy with some other process. The Processes are said to be in Deadlock.
* DL is a bug present in the process/thread synchronization method.
* In DL, processes never finish executing, and the system resources are tied up, preventing other jobs from starting.
* Example of resources: Memory space, CPU cycles, files, locks, sockets, IO devices etc.
* Single resource can have multiple instances of that. E.g., CPU is a resource, and a system can have 2 CPUs.
* How a process/thread utilize a resource?
    * a. Request: Request the R, if R is free Lock it, else wait till it is available.
    * b. Use
    * c. Release: Release resource instance and make it available for other processes
* **Deadlock Necessary Condition:** 4 Condition should hold simultaneously.
    * **a. Mutual Exclusion**
        * i. Only 1 process at a time can use the resource, if another process requests that resource, the requesting process must wait until the resource has been released.
    * **b. Hold & Wait**
        * i. A process must be holding at least one resource & waiting to acquire additional resources that are currently being held by other processes.
    * **c. No-preemption**
        * i. Resource must be voluntarily released by the process after completion of execution. (No resource preemption)
    * **d. Circular wait**
        * i. A set {P0, P1, ... ,Pn} of waiting processes must exist such that P0 is waiting for a resource held by P1, P1 is waiting for a resource held by P2, and so on.

* **Methods for handling Deadlocks:**
    * a. Use a protocol to prevent or avoid deadlocks, ensuring that the system will never enter a deadlocked state.
    * b. Allow the system to enter a deadlocked state, detect it, and recover.
    * c. Ignore the problem altogether and pretend that deadlocks never occur in system. (Ostrich algorithm) aka, Deadlock ignorance.

* To ensure that deadlocks never occur, the system can use either a deadlock prevention or deadlock avoidance scheme.
* **Deadlock Prevention:** by ensuring at least one of the necessary conditions cannot hold.
    * **a. Mutual exclusion**
        * i. Use locks (mutual exclusion) only for non-sharable resource.
        * ii. Sharable resources like Read-Only files can be accessed by multiple processes/threads.
        * iii. However, we can’t prevent DLs by denying the mutual-exclusion condition, because some resources are intrinsically non-sharable.
    * **b. Hold & Wait**
        * i. To ensure H&W condition never occurs in the system, we must guarantee that, whenever a process requests a resource, it doesn’t hold any other resource.
        * ii. Protocol (A) can be, each process has to request and be allocated all its resources before its execution.
        * iii. Protocol (B) can be, allow a process to request resources only when it has none. It can request any additional resources after it must have released all the resources that it is currently allocated.
    * **c. No preemption**
        * i. If a process is holding some resources and request another resource that cannot be immediately allocated to it, then all the resources the process is currently holding are preempted. The process will restart only when it can regain its old resources, as well as the new one that it is requesting. (Live Lock may occur).
        * ii. If a process requests some resources, we first check whether they are available. If yes, we allocate them. If not, we check whether they are allocated to some other process that is waiting for additional resources. If so, preempt the desired resource from waiting process and allocate them to the requesting process.
    * **d. Circular wait**
        * i. To ensure that this condition never holds is to impose a proper ordering of resource allocation.
        * ii. P1 and P2 both require R1 and R1, locking on these resources should be like, both try to lock R1 then R2. By this way which ever process first locks R1 will get R2.

## Deadlock Part two

* **Deadlock Avoidance:** Idea is, the kernel be given in advance info concerning which resources will use in its lifetime. By this, system can decide for each request whether the process should wait. To decide whether the current request can be satisfied or delayed, the system must consider the resources currently available, resources currently allocated to each process in the system and the future requests and releases of each process.
    * a. Schedule process and its resources allocation in such a way that the DL never occur.
    * b. Safe state: A state is safe if the system can allocate resources to each process (up to its max.) in some order and still avoid DL. A system is in safe state only if there exists a safe sequence.
    * c. In an Unsafe state, the operating system cannot prevent processes from requesting resources in such a way that any deadlock occurs. It is not necessary that all unsafe states are deadlocks; an unsafe state may lead to a deadlock.
    * d. The main key of the deadlock avoidance method is whenever the request is made for resources then the request must only be approved only in the case if the resulting state is a safe state.
    * e. In a case, if the system is unable to fulfill the request of all processes, then the state of the system is called unsafe.
    * f. Scheduling algorithm using which DL can be avoided by finding safe state. (Banker Algorithm)

* **Banker Algorithm**
    * a. When a process requests a set of resources, the system must determine whether allocating these resources will leave the system in a safe state. If yes, then the resources may be allocated to the process. If not, then the process must wait till other processes release enough resources.

* **Deadlock Detection:** Systems haven’t implemented deadlock-prevention or a deadlock avoidance technique, then they may employ DL detection then, recovery technique.
    * a. Single Instance of Each resource type (wait-for graph method)
        * i. A deadlock exists in the system if and only if there is a cycle in the wait-for graph. In order to detect the deadlock, the system needs to maintain the wait-for graph and periodically system invokes an algorithm that searches for the cycle in the wait-for graph.
    * b. Multiple instances for each resource type
        * i. Banker Algorithm

* **Recovery from Deadlock**
    * a. Process termination
        * i. Abort all DL processes
        * ii. Abort one process at a time until DL cycle is eliminated.
    * b. Resource preemption
        * i. To eliminate DL, we successively preempt some resources from processes and give these resources to other processes until DL cycle is broken.








## Memory Management Techniques Contiguous Memory Allocation

In Multi-programming environment, we have multiple processes in the main memory (Ready Queue) to keep the CPU utilization high and to make computer responsive to the users. <br>
To realize this increase in performance, however, we must keep several processes in the memory; that is, we must share the main memory. As a result, we must manage main memory for all the different processes. 

#### **Logical versus Physical Address Space** 
* a. Logical Address
    * i. An address generated by the CPU.
    * ii. The logical address is basically the address of an instruction or data used by a process.
    * iii. User can access logical address of the process.
    * iv. User has indirect access to the physical address through logical address.
    * v. Logical address does not exist physically. Hence, aka, Virtual address.
    * vi. The set of all logical addresses that are generated by any program is referred to as Logical Address Space.vii. Range: 0 to max.
* b. Physical Address
    * i. An address loaded into the memory-address register of the physical memory.
    * ii. User can never access the physical address of the Program.
    * iii. The physical address is in the memory unit. It’s a location in the main memory physically.
    * iv. A physical address can be accessed by a user indirectly but not directly.
    * v. The set of all physical addresses corresponding to the Logical addresses is commonly known as Physical Address Space.
    * vi. It is computed by the Memory Management Unit (MMU).
    * vii. Range: (R + 0) to (R + max), for a base value R.
* c. The runtime mapping from virtual to physical address is done by a hardware device called the memory-management unit (MMU).
* d. The user's program mainly generates the logical address, and the user thinks that the program isrunning in this logical address, but the program mainly needs physical memory in order to complete its execution.

<img width="505" height="360" alt="image" src="https://github.com/user-attachments/assets/57e923ac-0031-4c2a-aa5a-933a22d8be1a" />  
<br>

How OS manages the isolation and protect? **(Memory Mapping and Protection)**
* a. OS provides this Virtual Address Space (VAS) concept.
* b. To separate memory space, we need the ability to determine the range of legal addresses that the process may access and to ensure that the process can access only these legal addresses.
* c. The relocation register contains value of smallest physical address (Base address [R]); the limit register contains the range of logical addresses (e.g., relocation = 100040 & limit = 74600).
* d. Each logical address must be less than the limit register.
* e. MMU maps the logical address dynamically by adding the value in the relocation register.
* f. When CPU scheduler selects a process for execution, the dispatcher loads the relocation and limit registers with the correct values as part of the context switch. Since every address generated by the CPU (Logical address) is checked against these registers, we can protect both OS and other users’ and data from being modified by running process.
* g. Any attempt by a program executing in user mode to access the OS memory or other uses’ memory results in a trap in the OS, which treat the attempt as a fatal error.
* h. Address Translation

<img width="690" height="309" alt="image" src="https://github.com/user-attachments/assets/d2c51cc9-a0d4-41e1-a8cf-6fb04d1bcb4e" />

#### **Allocation Method on Physical Memory**
* a. Contiguous Allocation
* b. Non-contiguous Allocation

#### Contiguous Memory Allocation
* a. In this scheme, each process is contained in a single contiguous block of memory.
* b. **Fixed Partitioning**
    * i. The main memory is divided into partitions of equal or different sizes.
      <img width="565" height="350" alt="image" src="https://github.com/user-attachments/assets/2e281e5a-6079-4a3b-bd6e-b301498f60a7" />

 
    * ii. Limitations:
        * 1. Internal Fragmentation: if the size of the process is lesser then the total size of the partition then some size of the partition gets wasted and remain unused.This is wastage of the memory and called internal fragmentation.
        * 2. External Fragmentation: The total unused space of various partitions cannot be used to load the processes even though there is space available but not in the contiguous form.
        * 3. Limitation on process size: If the process size is larger than the size of maximum sized partition then that process cannot be loaded into the memory. Therefore, a limitation can be imposed on the process size that is it cannot be larger than the size of the largest partition.
        * 4. Low degree of multi-programming: In fixed partitioning, the degree of multiprogramming is fixed and very less because the size of the partition cannot be varied according to the size of processes.


* c. **Dynamic Partitioning**
    * i. In this technique, the partition size is not declared initially. It is declared at the time of process loading.
    <img width="527" height="323" alt="image" src="https://github.com/user-attachments/assets/7991fc8a-4206-4ba5-ab55-da93c0f396bf" />
    
    <br>
    * ii. Advantages over fixed partitioning
        * 1. No internal fragmentation
        * 2. No limit on size of process
        * 3. Better degree of multi-programming
    * iv. Limitation
        * 1. External fragmentation
    <br>
        

  <img width="660" height="449" alt="image" src="https://github.com/user-attachments/assets/77ac6a6f-cafc-49d5-9759-034e3c13e8ee" />



## Free Space Management

#### 1. Defragmentation/Compaction
* a. Dynamic partitioning suffers from external fragmentation.
* b. Compaction to minimize the probability of external fragmentation.
* c. All the free partitions are made contiguous, and all the loaded partitions are brought together.
* d. By applying this technique, we can store the bigger processes in the memory. The free partitions are merged which can now be allocated according to the needs of new processes. This technique is
also called defragmentation.
* e. The efficiency of the system is decreased in the case of compaction since all the free spaces will be transferred from several places to a single place.

#### 2. How free space is stored/represented in OS?
* a. Free holes in the memory are represented by a free list (Linked-List data structure).

#### 3. How to satisfy a request of a of n size from a list of free holes?

* a. Various algorithms which are implemented by the Operating System in order to find out the holes in the linked list and allocate them to the processes.
* b. **First Fit**
    * i. Allocate the first hole that is big enough.
    * ii. Simple and easy to implement.
    * iii. Fast/Less time complexity
* c. **Next Fit**
    * i. Enhancement on First fit but starts search always from last allocated hole.
    * ii. Same advantages of First Fit.
* d. **Best Fit**
    * i. Allocate smallest hole that is big enough.
    * ii. Lesser internal fragmentation.
    * iii. May create many small holes and cause major external fragmentation.
    * iv. Slow, as required to iterate whole free holes list.
* e. **Worst Fit**
    * i. Allocate the largest hole that is big enough.
    * ii. Slow, as required to iterate whole free holes list.
    * iii. Leaves larger holes that may accommodate other processes.


## Paging Non Contiguous Memory Allocation

* The main disadvantage of Dynamic partitioning is External Fragmentation. <br>
    a. Can be removed by Compaction, but with overhead.
    b. We need more dynamic/flexible/optimal mechanism, to load processes in the partitions.*
* **Idea behind Paging**
    a. If we have only two small non-contiguous free holes in the memory, say 1KB each.
    b. If OS wants to allocate RAM to a process of 2KB, in contiguous allocation, it is not possible, as we must have contiguous memory space available of 2KB. (External Fragmentation)
    c. What if we divide the process into 1KB-1KB blocks?
* **Paging**
    a. Paging is a memory-management scheme that permits the physical address space of a process to be non-contiguous.
    b. It avoids external fragmentation and the need of compaction.
    c. Idea is to divide the physical memory into fixed-sized blocks called Frames, along with divide logical memory into blocks of same size called Pages. (# Page size = Frame size)
    d. Page size is usually determined by the processor architecture. Traditionally, pages in a system had uniform size, such as 4,096 bytes. However, processor designs often allow two or more, sometimes simultaneous, page sizes due to its benefits.
    e. Page Table
        i. A Data structure stores which page is mapped to which frame.
        ii. The page table contains the base address of each page in the physical memory.
    f. Every address generated by CPU (logical address) is divided into two parts: a page number (p) and a page offset (d). The p is used as an index into a page table to get base address the corresponding frame in physical memory.
  <img width="949" height="447" alt="image" src="https://github.com/user-attachments/assets/5a4fa7e7-b3c8-42b0-94d7-4138ebcc4870" />

    g. Page table is stored in main memory at the time of process creation and its base address is stored in process control block (PCB).
    h. A page table base register (PTBR) is present in the system that points to the current page table. Changing page tables requires only this one register, at the time of context-switching.

* How Paging avoids external fragmentation?
    a. Non-contiguous allocation of the pages of the process is allowed in the random free frames of the physical memory.

* Why paging is slow and how do we make it fast?
    a. There are too many memory references to access the desired location in physical memory.

* Translation Look-aside buffer (TLB)
    a. A Hardware support to speed-up paging process.
    b. It’s a hardware cache, high speed memory.
    c. TBL has key and value.
    d. Page table is stores in main memory & because of this when the memory references is made the translation is slow.
    e. When we are retrieving physical address using page table, after getting frame address corresponding to the page number, we put an entry of the into the TLB. So that next time, we can get the values from TLB directly without referencing actual page table. Hence, make paging process faster.
  <img width="934" height="696" alt="image" src="https://github.com/user-attachments/assets/ecef2e4f-f2ac-4e4b-ab11-7997ec0f1f08" />

    f. TLB hit, TLB contains the mapping for the requested logical address.
    g. Address space identifier (ASIDs) is stored in each entry of TLB. ASID uniquely identifies each process and is used to provide address space protection and allow to TLB to contain entries for several different processes. When TLB attempts to resolve virtual page numbers, it ensures that the ASID for the currently executing process matches the ASID associated with virtual page. If it doesn’t match, the attempt is treated as TLB miss.





## Segmentation Non-Contiguous Memory Allocation

* An important aspect of memory management that become unavoidable with paging is separation of user’s
view of memory from the actual physical memory.
* Segmentation is memory management technique that supports the user view of memory.
* A logical address space is a collection of segments, these segments are based on user view of logical
memory.
* Each segment has segment number and offset, defining a segment.
<segment-number, offset> {s,d}
* Process is divided into variable segments based on user view.
* Paging is closer to the Operating system rather than the User. It divides all the processes into the form of pages although a process can have some relative parts of functions which need to be loaded in the same page.
* Operating system doesn't care about the User's view of the process. It may divide the same function into different pages and those pages may or may not be loaded at the same time into the memory. It decreases the efficiency of the system.
* It is better to have segmentation which divides the process into the segments. Each segment contains the same type of functions such as the main function can be included in one segment and the library functions can be included in the other segment.
<img width="947" height="500" alt="image" src="https://github.com/user-attachments/assets/5bb2b0e4-f6a3-4e8b-a3af-5214e9400722" />

* **Advantages:**
    * No internal fragmentation.
    * One segment has a contiguous allocation, hence efficient working within segment.
    * The size of segment table is generally less than the size of page table.
    * It results in a more efficient system because the compiler keeps the same type of functions in one segment.
  
* **Disadvantages:**
    * External fragmentation.
    * The different size of segment is not good that the time of swapping.
    * Modern System architecture provides both segmentation and paging implemented in some hybrid approach.



## What is Virtual Memory Demand Paging Page Faults

Virtual memory is a technique that allows the execution of processes that are not completely in the memory. It provides user an illusion of having a very big main memory. This is done by treating a part of secondary memory as the main memory. (Swap-space)

* **Advantage** of this is, programs can be larger than physical memory. <br>
It is required that instructions must be in physical memory to be executed. But it limits the size of a program to the size of physical memory. In fact, in many cases, the entire program is not needed at the same time. So, we want an ability to execute a program that is only partially in memory would give many benefits:
    * a. A program would no longer be constrained by the amount of physical memory that is available.
    * b. Because each user program could take less physical memory, more programs could be run at the same time, with a corresponding increase in CPU utilization and throughput.
    * c. Running a program that is not entirely in memory would benefit both the system and the user.

* Programmer is provided very large virtual memory when only a smaller physical memory is available.
* Demand Paging is a popular method of virtual memory management.
* In demand paging, the pages of a process which are least used, get stored in the secondary memory.
* A page is copied to the main memory when its demand is made, or page fault occurs. There are various page replacement algorithms which are used to determine the pages which will be replaced.
* Rather than swapping the entire process into memory, we use Lazy Swapper. A lazy swapper never swaps a page into memory unless that page will be needed.
*  We are viewing a process as a sequence of pages, rather than one large contiguous address space, using the term Swapper is technically incorrect. A swapper manipulates entire processes, whereas a Pager is concerned with individual pages of a process.

* How Demand Paging works?
    * a. When a process is to be swapped-in, the pager guesses which pages will be used.
    * b. Instead of swapping in a whole process, the pager brings only those pages into memory. This, it avoids reading into memory pages that will not be used anyway.
    * c. Above way, OS decreases the swap time and the amount of physical memory needed.
    * d. The valid-invalid bit scheme in the page table is used to distinguish between pages that are in memory and that are on the disk.
        * i. Valid-invalid bit 1 means, the associated page is both legal and in memory.
        * ii. Valid-invalid bit 0 means, the page either is not valid (not in the LAS of the process) or is valid but is currently on the disk.

<img width="862" height="514" alt="image" src="https://github.com/user-attachments/assets/32133772-d0c4-43e2-8729-5a6658d30369" />

    * f. If a process never attempts to access some invalid bit page, the process will be executed successfully without even the need pages present in the swap space.
    * g. What happens if the process tries to access a page that was not brought into memory, access to a page marked invalid causes page fault. Paging hardware noticing invalid bit for a demanded page will cause a trap to the OS.
    * h. The procedure to handle the page fault:
        * i. Check an internal table (in PCB of the process) to determine whether the reference was valid or an invalid memory access.
        * ii. If ref. was invalid process throws exception. If ref. is valid, pager will swap-in the page.
        * iii. We find a free frame (from free-frame list)
        * iv. Schedule a disk operation to read the desired page into the newly allocated frame.
        * v. When disk read is complete, we modify the page table that, the page is now in memory.
        * vi. Restart the instruction that was interrupted by the trap. The process can now access the page as through it had always been in memory.

<img width="930" height="625" alt="image" src="https://github.com/user-attachments/assets/7900761b-6e28-4c28-adbb-80093c5c24f5" />

    * **j. Pure Demand Paging**
        * i. In extreme case, we can start executing a process with no pages in memory. When OS sets the instruction pointer to the first instruction of the process, which is not in the memory. The process immediately faults for the page and page is brought in the memory.
        * ii. Never bring a page into memory until it is required.
    * k. We use locality of reference to bring out reasonable performance from demand paging.

* **Advantages of Virtual memory**
a. The degree of multi-programming will be increased.
b. User can run large apps with less real physical memory.

* **Disadvantages of Virtual Memory**
a. The system can become slower as swapping takes time.
b. Thrashing may occur.

## Page Replacement Algorithms

* Whenever Page Fault occurs, that is, a process tries to access a page which is not currently present in a frame and OS must bring the page from swap-space to a frame.
* OS must do page replacement to accommodate new page into a free frame, but there might be a possibility the system is working in high utilization and all the frames are busy, in that case OS must replace one of the pages allocated into some frame with the new page.
* The page replacement algorithm decides which memory page is to be replaced. Some allocated page is
swapped out from the frame and new page is swapped into the freed frame.

#### Types of Page Replacement Algorithm: (AIM is to have minimum page faults)
* **a. FIFO**
    * i. Allocate frame to the page as it comes into the memory by replacing the oldest page.
    * ii. Easy to implement.
    * iii. Performance is not always good
        * 1. The page replaced may be an initialization module that was used long time ago (Good replacement candidate)
          2. The page may contain a heavily used variable that was initialized early and is in content use. (Will again cause page fault)
    * iv. Belady’s anomaly is present.
        * 1. In the case of LRU and optimal page replacement algorithms, it is seen that the number of page faults will be reduced if we increase the number of frames. However, Balady found that, In FIFO page replacement algorithm, the number of page faults will get increased with the increment in number of frames.
        * 2. This is the strange behavior shown by FIFO algorithm in some of the cases.
* **b Optimal page replacement**
    * i. Find if a page that is never referenced in future. If such a page exists, replace this page with new page. If no such page exists, find a page that is referenced farthest in future. Replace this page with new page.
    * ii. Lowest page fault rate among any algorithm.
    * iii. Difficult to implement as OS requires future knowledge of reference string which is kind of impossible. (Similar to SJF scheduling)
* **c. Least-recently used (LRU)**
    * i. We can use recent past as an approximation of the near future then we can replace the page that has not been used for the longest period.
    * ii. Can be implemented by two ways
        * 1. Counters
            * a. Associate time field with each page table entry.
            * b. Replace the page with smallest time value.
        * 2. Stack
            * a. Keep a stack of page number.
            * b. Whenever page is referenced, it is removed from the stack & put on the top.
            * c. By this, most recently used is always on the top, & least recently used is always on the bottom.
            * d. As entries might be removed from the middle of the stack, so Doubly linked list can be used.
* **d. Counting-based page replacement** – Keep a counter of the number of references that have been made to each page. (Reference counting)
    * i. Least frequently used (LFU)
        * 1. Actively used pages should have a large reference count.
        * 2. Replace page with the smallest count.
    * ii. Most frequently used (MFU)
        * 1. Based on the argument that the page with the smallest count was probably just brought in and has yet to be used.
    * iii. Neither MFU nor LFU replacement is common.


## Thrashing

**Thrashing**
* a. If the process doesn’t have the number of frames it needs to support pages in active use, it will quickly page-fault. At this point, it must replace some page. However, since all its pages are in active use, it must replace a page that will be needed again right away. Consequently, it quickly faults again, and again, and again, replacing pages that it must bring back in immediately.
* b. This high paging activity is called Thrashing.
* c. A system is Thrashing when it spends more time servicing the page faults than executing
processes.
<img width="717" height="442" alt="image" src="https://github.com/user-attachments/assets/266a404c-6b5c-4a2a-b21f-8c48f3dcfb7c" />

* d. Technique to Handle Thrashing
    * i. Working set model
        * 1. This model is based on the concept of the Locality Model.
        * 2. The basic principle states that if we allocate enough frames to a process to accommodate its current locality, it will only fault whenever it moves to some new locality. But if the allocated frames are lesser than the size of the current locality, the process is bound to thrash.
    * ii. Page Fault frequency
        * 1. Thrashing has a high page-fault rate.
        * 2. We want to control the page-fault rate.
        * 3. When it is too high, the process needs more frames. Conversely, if the page fault rate is too low, then the process may have too many frames.
        * 4. We establish upper and lower bounds on the desired page fault rate.
        * 5. If pf-rate exceeds the upper limit, allocate the process another frame, if pf rate fails falls below the lower limit, remove a frame from the process.
        * 6. By controlling pf-rate, thrashing can be prevented.








###### DBMS
# 🎗 DBMS 
- [introduction to database](#Introduction-to-DBMS)
- [DBMS Architecture](#DBMS-Architecture)
- [ER Model](#ER-Model)
- [Extended ER](#Extended-ER)
- [Steps to Make ER Diagram](#Steps-to-Make-ER-Diagram)
- [Relational Model](#Relational-Model)
- [ER to Relational Mapping](#ER-to-Relational-Mapping)
- [Normalisation](#Normalisation)
- [Transaction](#Transaction)
- [How to implement Atomicity and Durability in Transactions](#How-to-implement-Atomicity-and-Durability-in-Transactions)
- [Indexing in DBMS](#Indexing-in-DBMS)
- [NoSQL](#NoSQL)
- [Types of Databases](#Types-of-Databases)
- [Clustering in DBMS](#Clustering-in-DBMS)
- [Partitioning & Sharding in DBMS (DB Optimisation)](#Partitioning--Sharding-in-DBMS-DB-Optimisation)
- [CAP Theorem](#CAP-Theorem)
- [master slave architecture](#master-slave-architecture)

---
```
ACID properties

Indexing &
Query Optimization

Normalization Forms
1NF, 2NF, 3NF, BCNF

ER Diagrams basics
```


## Introduction to DBMS

### 🎍 Data
* Raw, unorganized facts
* No meaning without processing
* Measured in bits & bytes

### 🎍 Types
* Quantitative → numerical (weight, cost)
* Qualitative → descriptive (name, gender)

### 🎍 Information
* Processed & meaningful data
* Used for decision-making

### 🎍 Data vs Information

| Basis           | Data                                 | Information                 |
| --------------- | ------------------------------------ | --------------------------- |
| Definition      | Collection of raw facts              | Processed data with meaning |
| Nature          | Raw and unorganized                  | Organized and structured    |
| Relationship    | Individual and sometimes unrelated   | Provides big-picture view   |
| Meaning         | Meaningless on its own               | Meaningful after processing |
| Dependency      | Does not depend on information       | Depends on data             |
| Form            | Numbers, graphs, figures, statistics | Words, language, ideas      |
| Decision Making | Not sufficient for decisions         | Used for decision-making    |

### 🎍 Database
* Organized electronic storage of data
* Easily accessed, updated, managed

### 🎍 DBMS
* interrelated data and set of program to access those data 
* Software to store & manage databases
* Supports insert, delete, update, retrieve

### 🎍 DBMS vs File System (Why DBMS?)
* No redundancy and data inconsistency (avoids same data at two different places and change in one of them)
* Easy data access (by query)
* Better security (protect data from unauthorized user)
* Handles concurrency (Multiple users can access)
* Maintains integrity (data remains accurate, valid, and consistent)
* maintains atomicity (transaction is completed fully or not executed at all)
* concurent-access anomalies (Avoids lost updates, dirty reads, and inconsistent data when multiple transactions occur simultaneously)

---

## DBMS Architecture

### 🎍 view of data(3-Schema Architecture)
system hides certain details of how the data is stored and maintained, through several levels of abstraction.
1. **Physical Level / Internal level**
   * How data is stored
2. **Logical Level / Conceptual level**
   * What data is stored
   * Relationships
3. **View Level / External level**
   * User-specific views
   * Security
     
<img width="559" height="387" alt="image" src="https://github.com/user-attachments/assets/ad52331c-ebcb-4d26-8026-dc9243b2f346" />

### 🎍 Instance / Schema

* **Instance** → DB data at a time (dynamic)
* **Schema** → DB structure (static)

Schema doesn’t change frequently. Data may change frequently. <br> 
We have 3 types of Schemas: Physical, Logical, several view schemas called subschemas. <br> <br>

DB Schema (logical Schema)
1. attributes of table
2. consistency constraints

### 🎍 Data Models
* descibes design at logical level 
* a collection of conceptual tools for describing data , data relationship , data semantic & consistency
* eg : ER Model, Relational Model, Object-Oriented Model

### 🎍 DB Languages

* **DDL (Data Definition Language)** defines and manages the database structure (tables, views, indexes, etc.).
* **DML (Data Manipulation Language)** is used to retrieve, insert, update, and delete data from tables.
* **DCL (Data Control Language)** controls user permissions and access to database objects.
* **TCL (Transaction Control Language)** manages transactions and ensures data consistency using **COMMIT**, **ROLLBACK**, and **SAVEPOINT**.

### 🎍 How is Database accesssed from application program 
apps (written in host languages C,C++,Java) interacts with DB.
<br>API is provided to send DML / DDL Statements to DB and retrieve the result.
<br>     (i)  open database connectivity (ODBC), Microsoft "C" .
<br>     (ii) JAVA database connectivity (JDBC),java

### 🎍 DBA
* A person who has central control of both the data and the programs that access those data.
* Functions of DBA
    * Schema Definition
    * Storage structure and access methods.
    * Schema and physical organization modifications.
    * Authorization control.
    * Routine maintenance
        * Periodic backups.
        * Security patches.
        * Any upgrades.

### 🎍 DBMS Architectures

* **1-Tier** → Single machine, The client, server & DB all present on the same machine.
* **2-Tier** →
    * App is partitioned into 2-components.
    * Client machine, which invokes DB system functionality at server end through query language statements.
    * API standards like ODBC & JDBC are used to interact between client and server.
* **3-Tier** → Client + App server + DB (best)
    * App is partitioned into 3 logical components.
    * Client machine is just a frontend and doesn't contain any direct DB calls.
    * Client machine communicates with App server, and App server communicated with DB system to access data.
    * Business logic, what action to take at that condition is in App server itself.
    * T3 architecture are best for WWW Applications.
    * Advantages:
        * Scalability due to distributed application servers.
        * Data integrity, App server acts as a middle layer between client and DB, which minimize the chances of data corruption.
        * Security, client can't directly access DB, hence it is more secure.


<img width="582" height="306" alt="image" src="https://github.com/user-attachments/assets/4e8bb4e6-7023-4844-8892-8b9d38f741fd" />


---

## ER Model

**Data Model**: Collection of conceptual tools for describing data, data relationships, data semantics, and consistency
constraints. <br>
**ER Model** : It is a high level data model based on a perception of a real world that consists of a collection of basic objects, called entities and of relationships among these objects. <br>
Graphical representation of ER Model is ER diagram, which acts as a blueprint of DB.

### 🎍 Entity

* Real-world object
* Identified by **Primary Key**
* eg -> Student

**Types**

* Strong Entity → independent
* Weak Entity → depends on strong entity

<img width="691" height="247" alt="image" src="https://github.com/user-attachments/assets/d9e3f9b4-827a-4ce9-8e48-fed464bc794e" />


### 🎍 Attributes
An attribute represents a characteristic or feature of an entity.
A property of an entity
eg -> Roll_No, Name, Age

#### Types of Attributes

| **Attribute Type**            | **Description**                                        | **Example**                           | **ER Diagram Representation**   |
| ----------------------------- | ------------------------------------------------------ | ------------------------------------- | ------------------------------- |
| **Single-Valued Attribute**   | Stores only one value for an entity.                   | Age, Gender                           | Single Oval (Ellipse)           |
| **Multi-Valued Attribute**    | Stores multiple values for an entity.                  | Phone No, Skills                      | Double Oval (Double Ellipse)    |
| **Simple (Atomic) Attribute** | Cannot be divided into smaller parts.                  | First Name, Salary                    | Single Oval                     |
| **Composite Attribute**       | Can be divided into sub-attributes.                    | Name (First Name, Last Name), Address | Oval connected to Sub-Ovals     |
| **Key Attribute**             | Uniquely identifies each entity.                       | Roll No, Employee_ID                  | Underlined Oval                 |
| **Non-Key Attribute**         | Describes an entity but does not uniquely identify it. | Name, Address                         | Single Oval                     |
| **Derived Attribute**         | Calculated from another attribute.                     | Age (from Date_of_Birth)              | Dashed Oval                     |
| **Stored Attribute**          | Directly stored in the database.                       | Date_of_Birth                         | Single Oval                     |
| **Required Attribute**        | Must contain a value for every entity.                 | Employee_ID                           | Single Oval                     |
| **Optional Attribute**        | May or may not contain a value.                        | Middle_Name                           | Single Oval (No special symbol) |


<img width="828" height="432" alt="image" src="https://github.com/user-attachments/assets/a307959f-3a27-4a3d-ab60-34dab937a460" />

### 🎍 Relationships

* Association between entities

* **Cardinality**
* one to one
* one to many
* many to one
* many to many

* **Degree**
* Unary, Binary, Ternary

### 🎍 Participation
aka minimium cardinality constraints.
* Partial -> not all  entity envolved
* Total (mandatory) -> all entitty envolved
* **weak entity** has total participation constraints.


<img width="872" height="474" alt="image" src="https://github.com/user-attachments/assets/65ae1467-af6b-48e1-a77f-f81f22ae4d7b" />

---
## Extended ER

* 🎍 **Specialisation** → Top-down <br>
Specialisation is splitting up the entity set into further sub entity sets on the basis of their functionalities,
specialities and features. <br>
It is a Top-Down approach.
  
* 🎍 **Generalisation** → Bottom-up <br>
 properties of two entities are overlapping .

* 🎍 **Inheritance** → attributes passed <br>
Attribute Inheritance <br>
Both Specialisation and Generalisation, has attribute inheritance. <br>
he attributes of higher level entity sets are inherited by lower level entity sets. <br>
E.g., Customer & Employee inherit the attributes of Person

* 🎍 **Aggregation** → relationship as entity
relationships among relationships <br>
Avoid redundancy 

---
# Steps to Make ER Diagram

* **1) Identify Entity Sets**
* **2) Identify attributes and their types**
* **3) Identify relational and constraints**


### 🎍 Example: ER Model of Banking System

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

#### 🎍 **1) Entity Set**

1. Branch 2. Customer 3. Employee 4. Saving Account <br>
5. Current Account 6. Loan 7. Payment (weak entity – loan)

#### 🎍 **2) Attributes & Their Types**

1. branch -> name, city, assest, liabilities
2. customer -> cust-id, name, address(composite), contact no(multivalued), DOB , age                              
3. employee -> name contact no. , dependent name(multivalued), years of service(years of services), start-date(single-value) 
4. Saving Account -> acc_number, balance, interest_rate, daily_withdrawal_limit
5. Current Account -> acc_no, balance, per_transaction_charges, overdraft_amount
6. Generalized Entity "Account" -> acc_number, balance
7. Loan -> loan_number, amount
8. Weak Entity "Payment" -> payment_no, date, amount

#### 🎍 **3) Relationship & Constraints**
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

### 🎍 Basic Terms

* **Table** → Relation, A single row / unique record.
* **Row** → Tuple, relationship among a set of values.
* **Column** → Attribute, attributes of the relation.
* **Degree** → No. of columns / attribute.
* **Cardinality** → No. of rows / tuples
* **Relational Key** → Set of attributes which can uniquely identify an each tuple.

### 🎍 properties 

* unique key
* atomic values
* tuple unique
* sequence any
* integrity constraints

### 🎍 Keys

* **Super Key (SK) :** combine unique key, can be null  
* **Candidate Key (CK) :** minimum subset of super keys, cannot be null
* **Primary Key (PK) :** selected out of CK set, has least no. of attributes 
* **Alternate Key (AK) :** [CK] - PK 
* **Foreign Key (FK) :** relational key
* **Composite Key :** PK formed using at least 2 attributes.
* **Compound Key :**  PK which is formed using 2 FK.
* **Surrogate Key :** Synthetic PK, Generated automatically by DB, usually an integer value, May be used as PK. 

### 🎍 Integrity Constraints

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

* 🎍 Strong entity → becomes an individual table with entity name, attrbute becomes column <br>
  **PK is used as relation's PK**
* 🎍 Weak entity → table formed with all entity attribute <br>
  **FK + composite PK** PK of corresponding strong entity will be added as FK. 
* 🎍 single valued attribute → column directly in tables 
* 🎍 Composite attribute → handled by attribute itself in original relation. **split**
* 🎍 Multivalued attribute → new table(named as original attribute name) are created for each multivalued attribute <br>
  PK as FK
  PK = FK + multivalued name 
* 🎍 Derived attribute → not consider in tables 
* 🎍 Generalisation → M1 create a table for the higher level entity <br>
                   M2 if generalisation is disjoint and complete , table <br>
                   drawback of M2 - stored twice                   
* 🎍 Aggregation → relationship table 

---

## Normalisation

Normalisation is a step towards DB optimisation. <br>
1. Normalisation is used to minimise the redundancy from a relations. It is also used to eliminate undesirable
characteristics like Insertion, Update, and Deletion Anomalies.
2. Normalisation divides the composite attributes into individual attributes OR larger table into smaller and links them
using relationships.
3. The normal form is used to reduce redundancy from the database table.

#### 🎍 Functional Dependency (FD)
PK to other attribute / relation , getting other entity with one or more entity <br>
X -> Y <br>
the left side of FD - Determinant <br>
the right side of the production - Dependent. <br>
    
#### 🎍 Types of FD
* Trivial FD : **A → B is trivial if B ⊆ A** A → B has trivial functional dependency if B is a subset of A. A->A, B->B are also Trivial FD.
* Non-trivial FD : **A → B is non-trivial if B ⊄ A, A ∩ B = Ø (NULL)** A → B has a non-trivial functional dependency if B is not a subset of A. [A intersection B is NULL].
    
  #### 🎍 Rules of FD (Armstrong’s axioms)
* Reflexive : If ‘A’ is a set of attributes and ‘B’ is a subset of ‘A’. Then, A→ B holds. <br>
                  If A ⊇ B then A → B. <br>
* Augmentation : If B can be determined from A, then adding an attribute to this functional dependency won’t change anything. <br>
                     If A→ B holds, then AX→ BX holds too. ‘X’ being a set of attributes. <br>
* Transitivity : If A determines B and B determines C, we can say that A determines C. <br>
                     If A→ B and B→ C then A→ C. <br>

* Why Normalisation? -> To avoid redundancy in the DB, not to store redundant data. 
* redundant data? -> Insertion, deletion and updation anomalies arises.
 
#### 🎍 Anomalies** abnormalities, there are three types of anomalies introduced by data redundancy.
* Insertion anomaly : can not be inserted, without the presence of other data.
* Deletion anomaly : unintended loss of some other important data.
* Updation anomaly (or modification anomaly) : The update anomaly is when an update of a single data value requires multiple rows of data to be updated. <br>
    time taken , data inconsistency

#### 🎍 Types of Normal forms
* **1NF**
    1. Every relation cell must have atomic value.
    2. Relation must not have multi-valued attributes.
* **2NF**
    1. Relation must be in 1NF.
    2. There should not be any partial dependency.
        * All non-prime attributes must be fully dependent on PK.
        * Non prime attribute can not depend on the part of the PK.
* **3NF**
    1. Relation must be in 2NF.
    2. No transitivity dependency exists.
        * Non-prime attribute should not find a non-prime attribute.
* **BCNF (Boyce-Codd normal form)**
     1. Relation must be in 3NF.
     2. FD: A -> B, A must be a super key.
         * We must not derive prime attribute from any prime or non-prime attribute

#### Advantages of Normalisation
1. Normalisation helps to minimise data redundancy.
2. Greater overall database organisation.
3. Data consistency is maintained in DB.

---

## Transaction
#### 🎍 Transaction
* A unit of work done against the DB in a logical sequence.
* Sequence is very important in transaction.
* It is a logical unit of work that contains one or more SQL statements. The result of all these statements in a
transaction either gets completed successfully (all the changes made to the database are permanent) or if at any
point any failure happens it gets rollbacked (all the changes being done are undone.) 

#### 🎍 ACID Properties
* To ensure integrity of the data.
* **Atomicity** : Either all operations of transaction are reflected properly in the DB, or none are.
* **Consistency** : Integrity constraints must be maintained before and after transaction.
* **Isolation** : multiple transactions may execute concurrently, unaware of other transactions executinh, without interfering each other.
* **Durability** : After transaction completes successfully, the changes it has made to the database persist, even if there are system failures.

#### 🎍 Transaction states

<img width="795" height="438" alt="image" src="https://github.com/user-attachments/assets/2fc4883f-938c-4b9a-9579-ccbfa9cfcb45" />

1. **Active state :** read and write operation -> partial commit state <br>
 &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;-> error - failed state

   
3. **Partially committed state :** transaction executed -> changes saved -> in buffer in main memory. <br>
If the changes are permanent DB -> committed state <br>
&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;-> error - Failed state. <br>

3. **Committed state :** updates permanent on DB, T in committed state. <br>
Rollback can’t be done. <br>
New consistent state is achieved at this stage.

5. **Failed state :** failure occurs, impossible execution 

6. **Aborted state :** T reaches the failed state <br>
all the changes made in the buffer are reversed. <br>
rollback <br>
prior DB’s state

7. **Terminated state :** A transaction is said to have terminated if has either committed or aborted.

## How to implement Atomicity and Durability in Transactions

### Recovery Mechanism Component of DBMS supports atomicity and durability.

### 🎍 Shadow-copy scheme
1. Based on making copies of DB (aka, **shadow copies**).
2. Assumption only one Transaction (T) is active at a time.
3. A pointer called **db-pointer** is maintained on the disk; which at any instant points to current copy of DB.
4. T, that wants to update DB first creates a complete copy of DB.
5. All further updates are done on new DB copy leaving the original copy (shadow copy) untouched.
6. If at any point the **T has to be aborted** the system deletes the new copy. And the old copy is not affected.
7. If **T success**, it is **committed** as,
    1. OS makes sure all the pages of the new copy of DB written on the disk.
    2. DB system updates the db-pointer to point to the new copy of DB.
    3. New copy is now the current copy of DB.
    4. The old copy is deleted.
    5. The T is said to have been COMMITTED at the point where updated db-pointer is written to disk.

#### **Atomicity**
1. If T fails at any time before db-pointer is updated, the old content of DB are not affected.
2. T abort can be done by just deleting the new copy of DB.
3. Hence, either all updates are reflected or none.

#### **Durability**
1. Suppose, system fails are any time before the updated db-pointer is written to disk.
2. When the system restarts, it will read db-pointer & will thus, see the original content of DB and none of the effects of T will
be visible.
3. T is assumed to be successful only when db-pointer is updated.
4. If **system fails after** db-pointer has been updated. Before that all the pages of the new copy were written to disk. Hence,
when system restarts, it will read new DB copy.

* The implementation is dependent on write to the db-pointer being atomic. Luckily, disk system provide atomic updates to entire
block or at least a disk sector. So, we make sure db-pointer lies entirely in a single sector. By storing db-pointer at the beginning
of a block.
* **Inefficient**, as entire DB is copied for every Transaction.

### 🎍 Log-based recovery methods
1. The log is a sequence of records. Log of each transaction is maintained in some stable storage so that if any failure occurs, then
it can be recovered from there.
2. If any operation is performed on the database, then it will be recorded in the log.
3. But the process of storing the logs should be done before the actual transaction is applied in the database.
4. Stable storage is a classification of computer data storage technology that guarantees atomicity for any given write operation
and allows software to be written that is robust against some hardware and power failures.

#### **Deferred DB Modifications**
1. Ensuring atomicity by recording all the DB modifications in the log but deferring the execution of all the write operations
until the final action of the T has been executed.
2. Log information is used to execute deferred writes when T is completed.
3. If system crashed before the T completes, or if T is aborted, the information in the logs are ignored.
4. If T completes, the records associated to it in the log file are used in executing the deferred writes.
5. If failure occur while this updating is taking place, we preform redo.

#### **Immediate DB Modifications**
1. DB modifications to be output to the DB while the T is still in active state.
2. DB modifications written by active T are called uncommitted modifications.
3. In the event of crash or T failure, system uses old value field of the log records to restore modified values.
4. Update takes place only after log records in a stable storage.
5. Failure handling
   1. System failure before T completes, or if T aborted, then old value field is used to undo the T.
   2. If T completes and system crashes, then new value field is used to redo T having commit logs in the logs.
CodeHelp.

## Indexing in DBMS

**Indexing** is used to **optimise the performance** of a database by minimising the number of disk accesses required when a query is
processed. <br>
The index is a type of **data structure.** <br>
**Speeds up operation** with read operations like SELECT queries, WHERE clause etc. <br>

**Search Key :** Contains copy of primary key or candidate key
of the table or something else. <br>
**Data Reference :** Pointer holding the address of disk block
where the value of the corresponding key is stored. <br>
Indexing is optional, but increases access speed. It is not the
primary mean to access the tuple, it is the secondary mean. <br>
Index file is always sorted. <br>

#### 🎍 **Indexing Methods**
* **Primary Index (Clustering Index)**
A file may have several indices, on different search keys. If the data file containing the records is sequentially ordered, a
Primary index is an index whose search key also defines the sequential order of the file. <br>
**NOTE :** The term primary index is sometimes used to mean an index on a primary key. However, such usage is **nonstandard** and **should be avoided.** <br>
All files are ordered sequentially on some search key. It could be Primary Key or non-primary key. <br>
**Dense And Sparse Indices** <br>
* **Dense Index** <br>
        1. The dense index contains an index record for every search key value in the data file. <br>
        2. The index record contains the search-key value and a pointer to the first data record with that search-key value.
The rest of the records with the same search-key value would be stored sequentially after the first record. <br>
        3. It needs more space to store index record itself. The index records have the search key and a pointer to the actual
record on the disk. <br>
* **Sparse Index** <br>
    1. An index record appears for only some of the search-key values. <br>
    2. Sparse Index helps you to resolve the issues of dense Indexing in DBMS. In this method of indexing technique, a range of index columns stores the same data block address, and when data needs to be retrieved, the block address will be fetched. <br>
* Primary Indexing can be based on Data file is sorted w.r.t Primary Key attribute or non-key attributes.
* **Based on Key attribute**
1. Data file is sorted w.r.t primary key attribute.
2. PK will be used as search-key in Index.
3. Sparse Index will be formed i.e., no. of entries in the index file = no. of blocks in datafile.
* **Based on Non-Key attribute**
1. Data file is sorted w.r.t non-key attribute.
2. No. Of entries in the index = unique non-key attribute value in the data file.
3. This is dense index as, all the unique values have an entry in the
index file.
4. E.g., Let’s assume that a company recruited many employees in
various departments. In this case, clustering indexing in DBMS
should be created for all employees who belong to the same
dept.
* **Multi-level Index**
1. Index with two or more levels.
2. If the single level index become enough large that the binary
search it self would take much time, we can break down
indexing into multiple levels.

#### 🎍 **Secondary Index (Non-Clustering Index)** 
1. Datafile is unsorted. Hence, Primary Indexing is not possible.
2. Can be done on key or non-key attribute.
3. Called secondary indexing because normally one indexing is already
applied.
4. No. Of entries in the index file = no. of records in the data file.
5. It's an example of Dense index.
CodeHelp

* **Advantages of Indexing**
1. Faster access and retrieval of data.
2. IO is less.

* **Limitations of Indexing**
1. Additional space to store index table
2. Indexing Decrease performance in INSERT, DELETE, and UPDATE query.

## NoSQL 

**NoSQL Overview**
* Non-relational, non-tabular databases
* Schema-free, flexible data models
* Handles big data & high traffic
* Supports horizontal scaling
* Mostly open-source

**Why NoSQL Emerged**
* Rise of unstructured data
* Need for faster development & flexibility
* Cheap storage, cloud computing
* Easy scaling across servers
* caching mechanism

**Advantages**
* Flexible schema
* Horizontal scaling (Sharding, Replication)
* High availability & fault tolerance
* Fast read/insert operations
* Good for cloud & distributed apps

**When to Use NoSQL**
* Agile development
* Huge / semi-structured data
* Scale-out systems
* Microservices & real-time apps

**Misconceptions**
* ❌ No relationships → ✅ Stored differently (nested)
* ❌ No ACID → ✅ Some DBs (MongoDB) support ACID

**Types of NoSQL**

1. **Key-Value** – Fast access via keys
   * Use: caching, sessions
   * Ex: Redis, DynamoDB
    
2. **Column-Oriented** – Column-wise storage
   * Use: analytics
   * Ex: Cassandra, RedShift
     
3. **Document-Based** – JSON-like documents
   * Use: e-commerce, apps
   * Ex: MongoDB, CouchDB
     
4. **Graph-Based** – Relationship focused
   * Use: social networks, fraud detection
   * Ex: Neo4j

**Disadvantages**
* Data redundancy
* Costly update/delete
* One model doesn’t fit all use cases
* Limited consistency & ACID (in general)

<img width="617" height="638" alt="image" src="https://github.com/user-attachments/assets/4915b60b-5298-4f6c-ba9c-41ed5f0ee6c1" />

# Types of Databases

## 🎍 Relational Databases

* Based on the **Relational Model**
* Designed in the **1970s**, still widely used
* Also called **RDBMS**
* Use **SQL** for CRUD operations
* Data stored in **tables**
* Tables are connected using **foreign keys (JOINs)**
* Example:

  * `User` table
  * `Purchases` table joined via user ID
* Examples: **MySQL, MS SQL Server, Oracle**
* Highly optimised for **structured data**
* Strong **data normalisation**
* Uses a well-known query language (**SQL**)
* **Scalability issues** (horizontal scaling is difficult)
* As data grows, system becomes **complex**

## 🎍 Object Oriented Databases

* Based on **Object-Oriented Programming concepts**

  * Inheritance
  * Encapsulation
  * Object identity
* Data is stored as **objects**, not tables
* Supports **complex data types**
* Useful when databases become very complex
* Relationships can be difficult to maintain

### Characteristics

* Data treated as **objects**
* All related data stored in **one object**
* No need for multiple tables

### Advantages

* Easy and fast **data storage & retrieval**
* Handles **complex relationships**
* Good for modelling **real-world problems**
* Works naturally with **OOP languages**

### Disadvantages

* High complexity → slower **read/write/update/delete**
* Limited community support
* No **views** like relational databases

### Examples

* **ObjectDB**
* **GemStone**

---

## 🎍 NoSQL Databases

* **Non-relational**, non-tabular databases
* Schema-free
* Flexible data structures
* Handles **big data**
* Supports **horizontal scaling**
* Mostly **open source**
* Stores data in formats other than tables
* Types include:

  * Document
  * Key-Value
  * Wide-Column
  * Graph
* Refer **LEC-15 NoSQL notes**

## 🎍 Hierarchical Databases

* Based on **tree-like structure**
* Best for **one-to-many relationships**
* Example: employees → departments

### Structure

* One **root (parent)** node
* Multiple **child** nodes
* Each child has **only one parent**
* Data stored as **records & fields**
* Data retrieval starts from the **root**

### Advantages

* Easy to use
* Fast traversal
* Simple structure
* Suitable for:

  * File systems
  * Folder structures
  * Drop-down menus
* Adding/deleting data does not affect whole DB
* Supported by many programming languages

### Disadvantages

* Very **inflexible**
* Cannot handle **many-to-many** relationships
* Sequential searching is time-consuming
* Data redundancy possible

### Example

* **IBM IMS**

## 🎍 Network Databases

* Extension of **Hierarchical databases**
* Child records can have **multiple parents**
* Organised as a **graph**
* Supports **many-to-many relationships**

### Advantages

* Handles **complex relationships**

### Disadvantages

* Difficult to maintain
* M:N links can slow retrieval
* Limited web/community support

### Examples

* **IDS**
* **IDMS**
* **Raima Database Manager**
* **TurboIMAGE**

---

## Clustering in DBMS

## 🎍 Database Clustering (Replica-Sets)

* Process of combining **multiple servers/instances** connected to a single database
* Used when one server is **not sufficient** to handle:

  * Large data volume
  * High number of requests
* Often associated with **SQL databases**
* SQL is used to manage clustered database information
* Same dataset is **replicated across multiple servers**

## 🎍 Advantages of Database Clustering

### Data Redundancy

* Same data stored on **multiple servers**
* Redundancy is **intentional and synchronised**
* Prevents data loss during server failure
* If one server fails, data is still available on others

### Load Balancing

* Workload is **distributed across servers**
* Prevents a single machine from getting overloaded
* Supports:

  * More users
  * Traffic spikes
* Improves scalability and performance
* Directly contributes to **high availability**

### High Availability

* Refers to how often the database is **accessible**
* Depends on:

  * Number of transactions
  * Frequency of analytics
* Clustering ensures database remains available even if:

  * One or more servers go down
* Achieves very high uptime using:

  * Load balancing
  * Multiple backup machines

## 🎍 How Database Clustering Works

* Requests are **split among multiple computers**
* Each user request can be handled by **any node**
* Load balancing distributes traffic
* If one node fails:

  * Another node handles the request
* Results in:

  * Minimal downtime
  * No single point of failure

---

## Partitioning & Sharding in DBMS DB Optimisation

## 🎍 Partitioning

* A big problem can be solved easily when it is chopped into several smaller sub-problems.

* That is what the **partitioning technique** does.

* It divides a big database containing data metrics and indexes into **smaller and handy slices of data called partitions**.

* The partitioned tables are directly used by **SQL queries without any alteration**.

* Once the database is partitioned, the **data definition language** can easily work on the smaller partitioned slices, instead of handling the giant database altogether.

* This is how partitioning cuts down the problems in managing large database tables.

* Partitioning is the technique used to divide stored database objects into **separate servers**.

* Due to this, there is an increase in:

  * Performance
  * Controllability of the data

* We can manage huge chunks of data optimally.

* When we horizontally scale our machines/servers, dealing with relational databases becomes challenging because it is tough to maintain relations.

* If we apply partitioning to a database that is already scaled out (equipped with multiple servers), we can partition the database among those servers and handle big data easily.

## 🎍 Vertical Partitioning

* Slicing relation **vertically / column-wise**
* Need to access **different servers** to get complete tuples

## 🎍 Horizontal Partitioning

* Slicing relation **horizontally / row-wise**
* Independent chunks of data tuples are stored in **different servers**

## 🎍 When Partitioning is Applied

* Dataset becomes so huge that managing and dealing with it becomes a tedious task
* Number of requests becomes very large
* Single DB server access takes huge time
* System response time becomes high

## 🎍 Advantages of Partitioning

* Parallelism
* Availability
* Performance
* Manageability
* Reduced cost, as scaling-up or vertical scaling can be costly

## 🎍 Distributed Database

* A single logical database spread across **multiple locations (servers)** and logically interconnected by a network
* Product of applying DB optimisation techniques such as:

  * Clustering
  * Partitioning
  * Sharding
* Why this is needed: **Refer “When Partitioning is Applied”**

## 🎍 Sharding

* Technique to implement **Horizontal Partitioning**
* Fundamental idea of sharding:

  * Instead of storing all data on one DB instance
  * Data is split across multiple DB instances
  * A **routing layer** forwards the request to the correct instance containing the data

### Pros

* Scalability
* Availability

### Cons

* High complexity
* Partition mapping required
* Routing layer must be implemented
* Non-uniform data distribution
* Necessity of **Re-Sharding**
* Not suitable for analytical queries
* Data is spread across DB instances (Scatter–Gather problem)


## CAP Theorem

### Overview

* One of the **most important concepts in Distributed Databases**
* Useful to design **efficient distributed systems** based on business logic

### Consistency (C)

* In a consistent system, **all nodes see the same data simultaneously**
* A read operation returns the value of the **most recent write**
* Read should cause all nodes to return the same data
* All users see the same data at the same time, regardless of the node they connect to
* Data is written to a **single node first**, then replicated to other nodes

### Availability (A)

* System remains **operational all the time**
* Every request receives a response, regardless of node failures
* System continues working even if **multiple nodes are down**
* No guarantee that the response contains the **most recent write**

### Partition Tolerance (P)

* Occurs when there is a **break in communication between nodes**
* Messages may be **dropped or delayed**
* Partition-tolerant systems continue to function even during network failures
* Requires **data replication across multiple nodes and networks**

## 🎍 What the CAP Theorem Says

* A distributed system can provide **only two out of three** properties at the same time:

  * Consistency
  * Availability
  * Partition Tolerance
* CAP theorem formalises the **trade-off between consistency and availability** when a partition occurs

## 🎍 CAP Theorem in NoSQL Databases

* NoSQL databases are ideal for **distributed networks**
* Support **horizontal scaling**
* Can scale quickly across multiple nodes
* CAP theorem must be considered while choosing a NoSQL database

## 🎍 CA Databases

* Provide **Consistency + Availability**
* Do **not support Partition Tolerance**
* Not practical in real distributed systems because partitions are unavoidable
* Still useful in limited cases
* Some relational databases like:

  * MySQL
  * PostgreSQL
* Can provide consistency and availability using **replication**


## 🎍 CP Databases

* Provide **Consistency + Partition Tolerance**
* Do **not provide Availability**
* During a partition:

  * Inconsistent nodes are turned off
  * System waits until partition is fixed
* **MongoDB** is an example of a CP database
* MongoDB:

  * Is a NoSQL DBMS
  * Uses **document-based storage**
  * Is **schema-less**
  * Commonly used in big data and distributed applications
* CP systems have:

  * **One primary node** that handles all write requests in a replica set
  * Secondary nodes replicate data from the primary
* If the primary fails:

  * A secondary node takes over
* In banking systems:

  * **Consistency is more important than availability**
  * Hence CP databases are preferred

## 🎍 AP Databases

* Provide **Availability + Partition Tolerance**
* Do **not provide Consistency**
* During a partition:

  * All nodes remain available
  * Data may not be the most recent
* Example scenario:

  * User accesses data from a bad node
  * Receives outdated data
* After partition is resolved:

  * Nodes synchronise data
  * **Eventual consistency** is achieved
* **Apache Cassandra** is an example of an AP database
* Cassandra:

  * Has **no primary node**
  * All nodes remain available
* Eventual consistency is achieved by:

  * Re-syncing data after partition resolution
* For applications like **Facebook**:

  * Availability is more important than consistency
  * AP databases like **Cassandra** or **Amazon DynamoDB** are preferred

<img width="354" height="301" alt="image" src="https://github.com/user-attachments/assets/2835a660-5d59-458d-80be-f38b3d05b4c3" />

---

## master slave architecture 

<img width="882" height="501" alt="image" src="https://github.com/user-attachments/assets/ad34aa68-c9c6-4ac9-a443-d0bd9b999cd1" />

## 🎍 Master–Slave Architecture (Database Replication)

* Master–Slave is a general way to **optimise I/O** in a system where the number of requests becomes so high that a **single DB server cannot handle it efficiently**
* It is a pattern discussed in **LEC-19 (Database Scaling Pattern)**

  * **Command Query Responsibility Segregation (CQRS)**

## 🎍 Working of Master–Slave

* The **true or latest data** is always kept in the **Master database**
* **Write operations** are directed only to the **Master**
* **Read operations** are performed only from the **Slave databases**
* This architecture helps in:

  * Safeguarding site **reliability**
  * Improving **availability**
  * Reducing **latency**
* If the site receives a lot of traffic and only one database is available:

  * The database becomes overloaded with read and write requests
  * The system becomes slow for all users

## 🎍 DB Replication

* DB replication distributes data from the **Master machine to Slave machines**
* Replication can be:

  * **Synchronous**
  * **Asynchronous**
* Type of replication depends on the **system’s requirement**

---




















# CN 

* [Basics](#Basics)
* [Network Topology](#Network-Topology)
* [Network Types](#Network-Types)
* [OSI Model](#Osi-Model)
* [Networking Commands](#Networking-Commands)
* [Web Concepts](#Web-Concepts)
* [Networking Protocols](#Networking-Protocols)
* [System Design Concepts](#System-Design-Concepts)
* [Modern Infrastructure](#Modern-Infrastructure)
* [Wireless Communication](#Wireless-Communication)
* [Security](#Security)
* [Real World Systems](Real-World-Systems)

##  Basics

* [What is Computer Networking](#What-is-Computer-Networking)
* [Basic Terms](#Basic-Terms)
* [Web vs Internet](#Web-vs-Internet)
* [Transmission Media](#Transmission-Media)
* [Network Devices](#Metwork-Devices)
* [Unicast, Broadcast, Multicast](#Unicast-Broadcast-and-Multicast)


```
TCP vs UDP
HTTP vs HTTPS
OSI & TCP/IP Layers
DNS & CDN Basics

Real-world questions
What happens when you type google.com
Difference between 2G / 3G / 4G
```

### What is Computer Networking

* A **computer network** is a collection of interconnected devices that can communicate and share resources.
* Devices include: computers, servers, routers, switches, mobiles.
* Communication happens using **protocols** (rules).
* **Goals**
    * Resource sharing (files, printers)
    * Communication (email, chat)
    * Scalability
    * Reliability
* **Types**
    * Wired (Ethernet)
    * Wireless (Wi-Fi, Bluetooth)

## Basic Terms

* **Node** → Any device in a network
* **Link** → Connection between nodes
* **Bandwidth** → Data transfer capacity (bps)
* **Latency** → Delay in data transfer
* **Throughput** → Actual data transferred
* **IP Address** → Unique identifier of a device
* **MAC Address** → Hardware address (unique, physical)
* **Protocol** → Rules of communication (HTTP, TCP, etc.)

**Important**

* Bandwidth ≠ Throughput
* Latency low = faster response

## Web vs Internet

| Feature    | Internet            | Web                 |
| ---------- | ------------------- | ------------------- |
| Definition | Network of networks | Service on internet |
| Works on   | IP, TCP/UDP         | HTTP/HTTPS          |
| Includes   | Email, FTP, Web     | Only websites       |
<br><br>
**Simple**

* Internet = Infrastructure
* Web = Service on top
<br><br>
**Example**

* Internet = Roads
* Web = Cars running on roads

## Transmission Media

Means how data travels

### 1. Guided (Wired)

* Twisted Pair Cable
* Coaxial Cable
* Optical Fiber (🔥 fastest)

### 2. Unguided (Wireless)

* Radio waves
* Microwaves
* Infrared
<br><br>
**Important**

* Fiber → High speed, low loss
* Wireless → Flexible but less secure

## Network Devices

* **Router** → Connects different networks
* **Switch** → Connects devices in LAN
* **Hub** → Broadcasts data (old, inefficient)
* **Modem** → Converts digital ↔ analog
* **Access Point** → Provides Wi-Fi
* **Firewall** → Security filter

💡 **Important Differences**

* Hub vs Switch → Switch is smarter
* Router works at **Network Layer**

## Unicast Broadcast Multicast

### 1. Unicast

* One-to-One communication
* Example: Sending message to a friend

### 2. Broadcast

* One-to-All
* Example: ARP request

### 3. Multicast

* One-to-Many (selected group)
* Example: Live streaming
<br><br>
**Important**

* Broadcast = heavy traffic
* Multicast = optimized communication


## Network Topology

* [Mesh](#Mesh-Topology)
* [Star](#Star-Topology)
* [Bus](#Bus-Topology)
* [Ring](#Ring-Topology)
* [Tree](#Tree-Topology)

**Definition :**<br>
Network topology is the **physical or logical arrangement of devices (nodes) and connections (links)** in a network.<br><br>

Two types:<br><br>

* **Physical Topology** → Actual layout (cables, devices)
* **Logical Topology** → How data flows

### Mesh Topology

#### Structure

* Every node is connected to **every other node**

#### Formula

* Total links = **n(n-1)/2**

#### Advantages

* High reliability (no single point of failure)
* Fault tolerant
* High security (dedicated links)

#### Disadvantages

* Very expensive (lots of cables)
* Complex setup
* Poor scalability

#### Use Case

* Military systems, critical networks


### Star Topology

#### Structure

* All devices connected to a **central hub/switch**

#### Advantages

* Easy to install & manage
* Easy fault detection
* Scalable

#### Disadvantages

* Central device failure → whole network down
* More cable than bus

#### Use Case

* Most modern LANs (🔥 very important)

## Bus Topology

#### Structure

* All devices connected to a **single backbone cable**

#### Advantages

* Low cost
* Simple to implement

#### Disadvantages

* Backbone failure → entire network down
* Difficult fault detection
* Collision issues

#### Use Case

* Old Ethernet networks (rare today)

## Ring Topology

#### Structure

* Devices connected in a **circular loop**

#### Working

* Data travels in **one direction** (token passing)

#### Advantages

* No collisions
* Predictable performance

#### Disadvantages

* Failure of one node → affects entire network
* Hard to troubleshoot

#### Use Case

* Token Ring (obsolete now)

## Tree Topology

#### Structure

* Combination of **star + bus**
* Hierarchical (parent-child structure)

#### Advantages

* Scalable
* Easy management of large networks

#### Disadvantages

* Backbone dependency
* Complex setup

#### Use Case

* Large organizations, enterprise networks

### Placement Important Comparison

| Topology | Cost        | Reliability | Scalability | Failure Impact       |
| -------- | ----------- | ----------- | ----------- | -------------------- |
| Mesh     | High        | Very High   | Poor        | Minimal              |
| Star     | Medium      | Medium      | High        | Central node failure |
| Bus      | Low         | Low         | Poor        | Full network down    |
| Ring     | Medium      | Medium      | Low         | One node affects all |
| Tree     | Medium-High | Medium      | High        | Backbone failure     |




## Network Types

* [LAN](#LAN)
* [MAN](#MAN)
* [WAN](#WAN)
* [PAN](#PAN)
* [CAN](#CAN)
* [SAN](#SAN)
 

### LAN

* **LAN (Local Area Network)**
* **Area Covered:** Small area (office, home, building)
* **Speed:** High (100 Mbps – 10 Gbps)
* **Topology:** Star, Ring, Bus
* **Devices:** Switch, Router, Hub
* **Example:** Home Wi-Fi, Office network

### MAN

* **MAN (Metropolitan Area Network)**
* **Area Covered:** City or town
* **Speed:** Medium
* **Topology:** Ring or Fiber-optic
* **Devices:** Routers, Switches
* **Example:** City-wide cable TV or internet network

### WAN

* **WAN (Wide Area Network)**
* **Area Covered:** Countries or continents
* **Speed:** Lower than LAN/MAN
* **Topology:** Mesh, Hybrid
* **Devices:** Routers, Modems
* **Example:** Internet

### PAN

* **PAN (Personal Area Network)**
* **Area Covered:** Very small, personal use
* **Speed:** Low to medium
* **Devices:** Smartphone, Laptop, Bluetooth devices
* **Example:** Bluetooth headphones, USB tethering

### CAN

* **CAN (Campus Area Network)**
* **Area Covered:** Multiple LANs in a campus or company
* **Devices:** Switches, Routers
* **Example:** University network connecting different departments

### SAN

* **SAN (Storage Area Network)**
* **Purpose:** High-speed network for storage devices
* **Devices:** Storage controllers, Fibre Channel switches
* **Example:** Data centers





## OSI Model

* [What is OSI Model](#What-is-OSI-Model)
* [OSI Layers](#OSI-Layers)
* [How a Packet Travels](#How-a-Packet-Travels)

### What is OSI Model

* **Full form:** Open Systems Interconnection Model
* **Purpose:** Standard framework for **network communication** between devices.
* **Layers:** 7 layers, each with a specific function.
* Helps in **troubleshooting**, designing, and understanding networks.

### OSI Layers

| Layer               | Function                                  | Data Unit | Devices/Protocols      |
| ------------------- | ----------------------------------------- | --------- | ---------------------- |
| **7. Application**  | Interface between user & network          | Data      | HTTP, FTP, SMTP        |
| **6. Presentation** | Data translation, encryption, compression | Data      | JPEG, MPEG, SSL/TLS    |
| **5. Session**      | Establish, manage, terminate sessions     | Data      | APIs, Sockets          |
| **4. Transport**    | End-to-end communication, error control   | Segment   | TCP, UDP               |
| **3. Network**      | Routing, addressing                       | Packet    | IP, Routers            |
| **2. Data Link**    | Error detection/correction, framing       | Frame     | Switch, MAC, Ethernet  |
| **1. Physical**     | Transmission of bits over media           | Bits      | Cables, Hub, Repeaters |

**Mnemonic to remember layers (top to bottom):**
**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

### How a Packet Travels

1. **Application Layer:** User sends a request (e.g., HTTP request).
2. **Presentation Layer:** Data is encrypted/compressed.
3. **Session Layer:** Connection/session established between devices.
4. **Transport Layer:** Data is split into **segments**, sequence added.
5. **Network Layer:** Segments → **Packets**, IP addresses added, routed.
6. **Data Link Layer:** Packets → **Frames**, MAC addresses added.
7. **Physical Layer:** Frames → **Bits**, transmitted over cables/wireless.

**Reverse process** happens at the receiver: bits → frames → packets → segments → data → presented to user.


## Networking Commands

## **Networking Commands**

* [Web Concepts](#web-concepts)
* [HTTP vs HTTPS](#http-vs-https)
* [API Gateway](#api-gateway)
* [SSL / TLS](#ssl--tls)
* [Reverse Proxy](#reverse-proxy)
* [Load Balancer](#load-balancer)

## **Web Concepts**

* Web works on **client-server model**
* Client → sends request (browser)
* Server → sends response (web server)
* Uses **HTTP/HTTPS protocols**
* Example: Opening a website in Chrome

## **HTTP vs HTTPS**

### **HTTP (HyperText Transfer Protocol)**

* Not secure
* Data sent in **plain text**
* Default port: **80**

### **HTTPS (Secure HTTP)**

* Secure version of HTTP
* Uses **encryption (SSL/TLS)**
* Default port: **443**
* Protects data from hackers

## **API Gateway**

* Acts as an **entry point** for all client requests
* Routes requests to appropriate services
* Handles:

  * Authentication
  * Rate limiting
  * Load balancing
* Used in **microservices architecture**

## **SSL / TLS**

* **SSL (Secure Sockets Layer)** and **TLS (Transport Layer Security)**
* Provide **encryption** for secure communication
* Used in HTTPS
* TLS is the **modern and more secure version of SSL**

## **Reverse Proxy**

* Sits between **client and server**
* Forwards client requests to backend servers
* Hides server identity
* Improves:

  * Security
  * Performance (caching)

## **Load Balancer**

* Distributes incoming traffic across multiple servers
* Prevents server overload
* Improves:

  * Performance
  * Availability
* Types:

  * Round Robin
  * Least Connections


## Networking Protocols

* [ARP](#arp)
* [Multiplexing](#multiplexing)
* [Public vs Private IP](#public-vs-private-ip)
* [NIC and MAC Address](#nic-and-mac-address)
* [Gateway vs Router](#gateway-vs-router)
* [Modem vs Router](#modem-vs-router)

Here are your clean and structured notes:

---

## **Networking Protocols**

* [ARP](#arp)
* [Multiplexing](#multiplexing)
* [Public vs Private IP](#public-vs-private-ip)
* [NIC and MAC Address](#nic-and-mac-address)
* [Gateway vs Router](#gateway-vs-router)
* [Modem vs Router](#modem-vs-router)

## **ARP**

* **Full form:** Address Resolution Protocol
* Maps **IP address → MAC address**
* Used in local network communication
* Example: Finding device MAC using its IP

## **Multiplexing**

* Technique to **combine multiple signals into one channel**
* Improves bandwidth usage
* Types:

  * FDM (Frequency Division)
  * TDM (Time Division)

## **Public vs Private IP**

### **Public IP**

* Unique across the internet
* Assigned by ISP
* Used for external communication

### **Private IP**

* Used inside local networks
* Not accessible from internet directly
* Example ranges:

  * 192.168.x.x
  * 10.x.x.x

## **NIC and MAC Address**

### **NIC (Network Interface Card)**

* Hardware that connects device to network
* Example: Ethernet card, Wi-Fi adapter

### **MAC Address**

* Unique **physical address** of NIC
* Assigned by manufacturer
* Format: 00:1A:2B:3C:4D:5E

## **Gateway vs Router**

### **Gateway**

* Connects **different networks**
* Acts as entry/exit point

### **Router**

* Routes data between networks
* Uses IP addresses

## **Modem vs Router**

### **Modem**

* Converts **digital ↔ analog signals**
* Connects to ISP

### **Router**

* Distributes internet to multiple devices
* Creates local network (Wi-Fi/LAN)








## **System Design Concepts**

* [Horizontal vs Vertical Scaling](#horizontal-vs-vertical-scaling)
* [Caching](#caching)
* [Performance vs Scalability](#performance-vs-scalability)
* [Latency vs Throughput](#latency-vs-throughput)
* [VIP in Networks](#vip-in-networks)


## **Horizontal vs Vertical Scaling**

### **Horizontal Scaling**

* Adding **more machines/servers**
* Also called **scaling out**
* Improves reliability and availability
* Example: Adding more servers to handle traffic

### **Vertical Scaling**

* Increasing **power of a single machine** (CPU, RAM)
* Also called **scaling up**
* Limited by hardware capacity
* Example: Upgrading server RAM

## **Caching**

* Storing frequently accessed data in **temporary storage**
* Reduces **latency** and server load
* Improves performance

**Types:**

* Browser cache
* Server cache
* CDN cache

## **Performance vs Scalability**

### **Performance**

* How fast a system responds
* Measured by **response time & latency**

### **Scalability**

* Ability to handle **increasing load**
* Measured by how system grows without failure

## **Latency vs Throughput**

### **Latency**

* Time taken for a request → response
* Lower latency = faster response

### **Throughput**

* Number of requests processed per second
* Higher throughput = better capacity

## **VIP in Networks**

* **VIP = Virtual IP Address**
* Not tied to a single device
* Used by:

  * Load balancers
  * High availability systems
* Helps in **failover** and traffic distribution








## **Modern Infrastructure**

* [REST API vs HTTP API](#rest-api-vs-http-api)
* [Containers](#containers)
* [Containerization vs Virtualization](#containerization-vs-virtualization)

## **REST API vs HTTP API**

### **REST API**

* Follows **REST principles** (stateless, client-server, cacheable)
* Uses standard HTTP methods: **GET, POST, PUT, DELETE**
* Structured and widely used

### **HTTP API**

* General term for any API using HTTP
* Not necessarily RESTful
* More flexible but less standardized

## **Containers**

* Lightweight units that package:

  * Application
  * Dependencies
* Run consistently across environments

**Features:**

* Fast startup
* Portable
* Efficient resource usage

## **Containerization vs Virtualization**

### **Containerization**

* Uses **containers**
* Shares host OS
* Lightweight and fast
* Example: Docker

### **Virtualization**

* Uses **virtual machines (VMs)**
* Each VM has its own OS
* Heavy and slower than containers
* Example: VMware









## **Wireless Communication**

* [Bluetooth](#bluetooth)
* [Hotspot](#hotspot)
* [2G vs 3G vs 4G vs 5G](#2g-vs-3g-vs-4g-vs-5g)

## **Bluetooth**

* Short-range wireless communication technology
* Used to connect devices like:

  * Headphones
  * Speakers
  * Smartwatches
* Range: ~10 meters
* Low power consumption

## **Hotspot**

* Turns a device (phone/laptop) into a **Wi-Fi source**
* Shares mobile data with other devices
* Types:

  * Mobile hotspot
  * Wi-Fi hotspot

## **2G vs 3G vs 4G vs 5G**

### **2G**

* Supports calls and SMS
* Very slow data (kbps)

### **3G**

* Introduced mobile internet
* Moderate speed (Mbps)

### **4G**

* High-speed internet
* Supports streaming, gaming
* Speed: up to ~100 Mbps

### **5G**

* Very high speed and low latency
* Supports IoT, smart devices
* Speed: up to Gbps








## **Security**

* [VPN](#vpn)

## **VPN**

* **Full form:** Virtual Private Network
* Creates a **secure, encrypted connection** over the internet
* Hides user’s **IP address**
* Protects data from hackers and tracking

**Uses:**

* Secure browsing on public Wi-Fi
* Access restricted websites
* Maintain privacy and anonymity







## **Real World Systems**

* [How Email Works](#how-email-works)
* [How File Transfer Works](#how-file-transfer-works)
* [How ATM Works](#how-atm-works)

## **How Email Works**

* User composes email in **email client**
* Sent using **SMTP (Simple Mail Transfer Protocol)**
* Email server processes and sends to recipient server
* Receiver fetches email using:

  * **POP3** or
  * **IMAP**
* Email is displayed in receiver’s inbox

## **How File Transfer Works**

* Uses protocols like:

  * **FTP (File Transfer Protocol)**
  * **SFTP (Secure FTP)**
* Steps:

  * Client requests file
  * Server authenticates user
  * File is transferred in packets
  * Reassembled at receiver side

## **How ATM Works**

* User inserts card → ATM reads card details
* User enters PIN → verified by bank server
* Request sent to bank system
* Bank checks:

  * Balance
  * Authentication
* If valid:

  * Cash is dispensed
  * Transaction recorded
* Receipt generated

















## mechanism of the computer
