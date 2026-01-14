# THEORY

### OOPS THEORY
[OOPS](#Oops)
<BR>
[THEORY NOTES- oops theory part 1 ](https://drive.google.com/file/d/1h-4RdVIQCNu_loshweVu5TvqvYxHTY2d/view)
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
- [shallow and deep copy](#shallow-and-deep-copy)
- [this](#this)
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

# setter and getter
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

### What is Padding?

**Padding** is the extra unused memory added by the compiler **between class/struct data members** to satisfy **alignment rules** and make memory access faster.

### Why padding is needed?

* CPU accesses memory faster when data is **properly aligned**
* Avoids **multiple memory fetches**
* Improves **performance**

---

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

---

## 🔹 Alignment

### What is Alignment?

**Alignment** means placing data in memory addresses that are multiples of their size.

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

---

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

---

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

## 🔑 Key Differences (Exam Table)

| Concept            | Padding            | Greedy Alignment         |
| ------------------ | ------------------ | ------------------------ |
| Meaning            | Extra unused bytes | Placement strategy       |
| Purpose            | Speed              | Correct alignment        |
| Controlled by      | Compiler           | Compiler                 |
| Programmer control | ❌                  | Partially (member order) |

---

## 🔹 How to Reduce Padding? (Very Important)

✔ Arrange members **largest → smallest**
✔ Use `#pragma pack(1)` (⚠️ performance cost)

```cpp
#pragma pack(1)
class P {
    char c;
    int i;
};
```



## 🔹 One-Line Definitions (Homework Ready)

* **Padding**: Extra bytes added to satisfy alignment.
* **Alignment**: Positioning data at suitable memory addresses.
* **Greedy alignment**: Compiler places each member at the earliest aligned address, even if padding increases.

---

### static and dynamic
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
};

int main() {
    //static memory allocation
    Teacher t1 ;

    //dynamic memory allocation
    Teacher *t2 = new Teacher; // for calling writ (*t2.propertie)
    
    return 0;
}
```

##### encapsulation 
combine data and other function

```cpp
#include <iostream>
using namespace std;
class Teacher {
    double salary;
    public:
    string name;
    string dept;
    string subject;
    
//setter
void setSalary (double s) {
    salary = s;
}

double getSalary() {
return salary;
}
```

##### constructor
* when a function is created a function (constructor gets build) like name t1.Teacher()
* object creation used for initialisation

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
//shallow copy
Student(Student &obj) {
    this->name = obj.name;
    this->cgpaPtr = obj.cgpaPtr;
}

//deep copy
Student(Student &obj){
    this->name = obj.name;
    cgpaPtr = new double;
    cgpaPtr = *obj.cgpaPtr;
}
```

```cpp
int main() {
    Student s1("rahul kumar", 8.9);
    Student s2(s1); //"neha kumar"

    s1.getInfo();
    *(s2.cgpaPtr) = 9.2;
    s1.getInfo();

    s2.name = "neha";
    s2.getInfo();
    return 0;
}
```
### destructor

```cpp
//destructor
~Student() {
    cout << "Hi, I delete everything\n";
}
```

### static keywords
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

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/474ed3eb-12e2-46c8-8efb-3352473bacfc" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/54f3ad88-1fe4-4fd5-81f6-0b23e7b08e9c" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6fc25f50-66dc-49d0-889c-116d901363e9" />

# CN 

# OS
