# INTRODUCTION TO SYSTEM DESIGN

## What is Low Level Design (LLD)?
- **Scalability:** System works well even if users or data increase a lot.
- **Maintainability:** Easy to fix bugs or add features without breaking old code.
- **Reusability:** Code can be reused in different parts of the app without rewriting.

---

## HLD vs LLD vs DSA
- **HLD (High Level Design):** Focuses on system architecture, technology stack, database choices, server scaling, and cost optimization.
- **LLD (Low Level Design):** Focuses on code structure, class diagrams, and implementation details.
- **DSA (Data Structures & Algorithms):** Used to solve problems in LLD; DSA is the brain, LLD is the skeleton.

---

## Rider Mapping Algorithm
Rider mapping algorithms efficiently match riders with drivers in ride-sharing platforms. Goals:
- Minimize wait times
- Optimize routes
- Maximize resource utilization

---

## Summary
- **HLD:** System architecture
- **LLD:** Code structure
- **DSA:** Problem solving in LLD

---

# HISTORY OF PROGRAMMING

## 1. Machine Language (0/1)
- Direct interaction with CPU
- Prone to errors
- Not scalable

## 2. Assembly Language
- Example: `MOV A, 61H`
- Prone to errors
- Not scalable (direct interaction with hardware)
- Tedious to write and maintain

## 3. Procedural Programming
- Uses functions
- Control structures: if-else, switch
- Loops
- Code is a set of instructions

### Example (Procedural Approach)
```cpp
std::string engine;
std::string model;
std::string brand;
int wheels;
bool isEngineOn;

void start() {}
void gearShift() {}
void accelerate() {}
void stop() {}

void drive() {
    start();
    gearShift();
    accelerate();
}

int main_proc() {
    // Set up car details if needed
    drive();
    return 0;
}
```

## 4. Object-Oriented Programming (OOP)
- Real-world modeling
- Data security
- Highly scalable and reusable
- Objects interact with each other and have characteristics (attributes) and behaviors (methods)
- All these characteristics and behaviors are grouped into a class, making the code more organized, reusable, and easier to maintain.

### Example (OOP Approach)
```cpp
class Car {
public:
    // characteristics
    std::string engine;
    std::string model;
    std::string brand;
    int wheels;
    bool isEngineOn;

    // behaviors
    void start() {}
    void gearShift() {}
    void accelerate() {}
    void stop() {}
};

class Owner {
public:
    Car car;
    std::string name;
    void drive() {
        car.start();
        car.gearShift();
        car.accelerate();
    }
};

int main() {
    Owner owner;
    owner.drive();
    return 0;
}
```

# OOPS PILLARS

## Pillars of OOPs
- Abstraction
- Encapsulation
- Inheritance
- Polymorphism

### Abstraction
Abstraction means showing only the important things and hiding the unnecessary details from the user.

- Only the required features are shown to the user.
- The user does not need to know how things work inside, just how to use them.
- Makes using complex systems simple and easy.

**Example:**
When an owner uses a car, they just use start, stop, and accelerate. They do not need to know how the engine works inside.

```cpp
class Car {
public:
    void start() {
        // Complex logic hidden from user
    }
    void stop() {
        // Complex logic hidden from user
    }
    void accelerate() {
        // Complex logic hidden from user
    }
};

int main() {
    Car car;
    car.start();
    car.accelerate();
    car.stop();
    return 0;
}
```

### Encapsulation
Encapsulation means keeping all the data (variables) and methods (functions) that work on that data together in one place (a class). It also means protecting the data from outside access for security.

- All the characteristics and behaviors of an object are kept together in a class.
- We use access modifiers (public, private, protected) to control who can access what.
- Data can only be changed using special functions (getters and setters), not directly.
- Encapsulation helps keep data safe and secure from unauthorized access or modification.

**Example:**
You cannot set the car's speed directly from outside the class. You must use the setSpeed function.

```cpp
class Car {
private:
    int speed; // Private variable
public:
    void setSpeed(int s) {
        // validation
        // any other logic that need to be check before set the speed
        if (s >= 0) speed = s;
    }
    int getSpeed() {
        return speed;
    }
};

int main() {
    Car car;
    car.setSpeed(60); // Safe way to set speed
    // car.speed = 100; // Not allowed, speed is private
    return 0;
}
```

### Inheritance
Inheritance means a class (child) can use the properties and behaviors (methods) of another class (parent). It helps to reuse code and extend existing functionality.

- The child class inherits characteristics and behaviors from the parent class.
- You can add new features or override existing ones in the child class.
- Makes code more organized and reduces duplication.

**Example:**
Suppose we have a `Car` class. We can create `ManualCar` and `ElectricCar` classes that inherit from `Car` and add their own features.

```cpp
class Car {
public:
    std::string brand;
    std::string model;
    bool isEngineOn;
    int currSpeed;
    void startEngine() {}
    void stopEngine() {}
    void brake() {}
    void accelerate() {}
};

class ManualCar : public Car {
public:
    int currentGear;
    void shiftGear() {}
};

class ElectricCar : public Car {
public:
    int battery;
    void chargeBattery() {}
};
```

### Polymorphism
Polymorphism means having many forms. It allows the same function or method to behave differently based on the object that is calling it. In OOP, there are two main types of polymorphism:

- **Compile-time (Static) Polymorphism:** Achieved by method overloading (same function name, different parameters).
- **Run-time (Dynamic) Polymorphism:** Achieved by method overriding (child class provides its own implementation of a function defined in the parent class).

**Example (Dynamic Polymorphism):**
Suppose both ManualCar and ElectricCar inherit from Car and override the accelerate method. Here, we use constructors and destructors to manage memory.

```cpp
#include <iostream>
using namespace std;

class Car {
public:
    Car() { cout << "Car created." << endl; }
    virtual ~Car() { cout << "Car destroyed." << endl; }
    virtual void accelerate() = 0; // Pure virtual function
};

class ManualCar : public Car {
public:
    ManualCar() { cout << "ManualCar created." << endl; }
    ~ManualCar() { cout << "ManualCar destroyed." << endl; }
    void accelerate() override {
        cout << "Manual car accelerating with gear shift." << endl;
    }
};

class ElectricCar : public Car {
public:
    ElectricCar() { cout << "ElectricCar created." << endl; }
    ~ElectricCar() { cout << "ElectricCar destroyed." << endl; }
    void accelerate() override {
        cout << "Electric car accelerating silently." << endl;
    }
};

int main() {
    Car* car1 = new ManualCar();
    Car* car2 = new ElectricCar();
    car1->accelerate(); // Calls ManualCar's accelerate
    car2->accelerate(); // Calls ElectricCar's accelerate
    delete car1; // Destructor called, memory freed
    delete car2; // Destructor called, memory freed
    return 0;
}
```

**Example (Static Polymorphism):**


```cpp
#include <iostream>
using namespace std;

class Math {
public:
    int add(int a, int b) {
        return a + b;
    }
    double add(double a, double b) {
        return a + b;
    }
};

int main() {
    Math m;
    cout << m.add(2, 3) << endl;      // Calls int version
    cout << m.add(2.5, 3.5) << endl;  // Calls double version
    return 0;
}
```


# UML DIAGRAMS

## What is a UML Diagram?
UML (Unified Modeling Language) diagrams are standardized ways to visually represent the design and structure of a software system. They help in understanding, documenting, and communicating the architecture and behavior of a system.

### Types of UML Diagrams
- **Structural (Static) Diagrams:** Show the components and their relationships (e.g., Class Diagram, Object Diagram, Component Diagram, Deployment Diagram, etc.)
- **Behavioral (Dynamic) Diagrams:** Show how components interact and behave over time (e.g., Sequence Diagram, Use Case Diagram, Activity Diagram, State Diagram, etc.)

---

## Class Diagram
A Class Diagram is a type of structural diagram that shows the classes in a system, their attributes, methods, and the relationships between them. It is widely used in object-oriented design.

<!-- 1: class structure -->

### Notation
- **Class Name** at the top (centered, bold)
- **Attributes** listed with visibility:
  - `+` Public
  - `#` Protected
  - `-` Private
- **Methods** listed with visibility and return type
- **Abstract classes** are marked with `<<abstract>>`

#### Example: UML Class Diagram for `Car`

```
+----------------------+
|        Car           |
+----------------------+
| - brand: string      |
| - model: string      |
| - engine: int        |
+----------------------+
| +startEngine(): void |
| +stopEngine(): void  |
| +accelerate(): void  |
| +brake(): void       |
+----------------------+
```

**Explanation:**
- The `Car` class has three private attributes: `brand`, `model`, and `engine`.
- It has four public methods: `startEngine()`, `stopEngine()`, `accelerate()`, and `brake()`.
- The `+` sign indicates public, and the `-` sign indicates private.

<!-- 2: class asscoiation.connection -->
## Associations in UML Class Diagrams

In UML, there are two main types of associations:

### 1. Class Association (Inheritance)
- Shows "is-a" relationships between classes.
- Symbol: `------|>`
- Example: `ManualCar` and `ElectricCar` are child classes that inherit from `Car`.

```
ManualCar ------|> Car
ElectricCar ------|> Car
```
- **Explanation:**
  - `ManualCar` and `ElectricCar` inherit from `Car` (they are types of Car).

---

### 2. Object Association (Between Objects)
Shows how objects relate to each other. There are three main types:

#### a) Simple Association ("uses" or "knows")
- Symbol: `----->`
- Example: A `Person` lives in a `House`.
```
Person -----> House
```

#### b) Aggregation ("has a" - parts can exist independently)
- Symbol: `---◇`
- Example: A `Room` contains `Bed`, `Chair`, and `Sofa`.
```
        Chair
         |
         |
         ◇   
Sofa ---◇Room◇--- Bed
```

#### c) Composition ("owns a" - parts cannot exist independently)
- Symbol: `---◆`
- Example: A `Chair` is made of `Arms`, `Seat`, and `Wheels`.
```
        Wheel
         |
         |
         ◆   
Arms ---◆Chair◆--- Seat
```

**Summary Table:**
| Type             | Symbol  | Example                | Ownership         |
|------------------|---------|------------------------|-------------------|
| Inheritance      | ---!>   | ManualCar ---!> Car    | is-a              |
| Simple Association| -----> | Person -----> House    | uses/knows        |
| Aggregation      | ---◇    | Room ◇--- Bed          | has-a (weak)      |
| Composition      | ---◆    | Chair ◆--- Seat        | owns-a (strong)   |


## Sequence Diagram
A Sequence Diagram is a type of behavioral UML diagram that shows how objects interact with each other in a particular scenario of a use case. It focuses on the order of messages exchanged between objects over time.

### Key Concepts
- **Object:** Represented at the top as a box with the object's name (e.g., `A`, `B`, `C`).
- **Lifeline:** A vertical dashed line below each object, showing the object's existence over time.
- **Activation Bar:** A thin rectangle (or thick vertical line) on the lifeline, showing when an object is active/performing an action. It is usually drawn as a narrow box over the lifeline during the period the object is executing a process or waiting for a response.
  - Example:
    ```
    A           B
    |           |
    | ======>   |   // Activation bar on A during its action
    |           |
    ```
- **Message:** An arrow between lifelines, representing communication. There are two main types:
  - **Synchronous (sync):** Sender waits for a response. Solid arrow with a filled arrowhead: `A --------|> B`
  - **Asynchronous (async):** Sender does not wait. Solid arrow with open arrowhead: `A ---------> B`
- **Response:** Dashed arrow back to the sender, often for return values: `B <|-------- A`

### Example Sequence Diagram

```
A           B           C
|           |           |
| --------->|           |   // async message from A to B
|           |---------> |   // async message from B to C
|           |<--------  |   // response from C to B (dashed)
| <-------- |           |   // response from B to A (dashed)
```

**Legend:**
- `--------->` : Asynchronous message
- `---------|>` : Synchronous message
- `<|--------` : Response (dashed line)

**Explanation:**
- `A` sends an async message to `B`.
- `B` sends an async message to `C`.
- `C` responds to `B` (dashed line).
- `B` responds to `A` (dashed line).

### Special Message Types in Sequence Diagrams

#### 1. Create Message
- Used to show when an object is created during the interaction.
- Shown as a dashed arrow with the keyword `create`.
```
A ---------> B : create
```

#### 2. Destroy Message
- Shows when an object is destroyed (often with an 'X' at the end of the lifeline).
- Shown as a solid arrow with the keyword `destroy` or a cross at the end.
```
A ---------> B : destroy
                   X
```

#### 3. Lost Message
- A message sent but not received by any known object (arrow points to nowhere).
```
A ---------> [lost]
```

#### 4. Found Message
- A message received by an object, but the sender is unknown (arrow comes from nowhere).
```
[found] ---------> B
```

**Explanation:**
- **Create:** Shows object creation during the sequence.
- **Destroy:** Shows object destruction during the sequence.
- **Lost:** Message sent but not received by any object in the diagram.
- **Found:** Message received by an object from an unknown sender.







