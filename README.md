# LECTURE 1 (INTRODUCTION TO SYSTEM DESIGN)

## LLD: Low Level Design
-  Scalability: The system should work well even if the number of users or data increases a lot.
-  Maintainability: It should be easy to fix bugs or add new features without breaking old ones.
-  Reusability: The same code should work in different parts of the app without rewriting it.

---

## HLD vs LLD vs DSA
- HLD (High Level Design): Focuses on system architecture, technology stack, database choices, server scaling, and cost optimization.
- LLD (Low Level Design): Focuses on code structure, class diagrams, and implementation details.
- DSA (Data Structures & Algorithms): Used to solve problems in LLD; DSA is the brain of the application, while LLD is the skeleton.

---

## Algorithm: Rider Mapping
Rider mapping algorithms are used to efficiently match riders with drivers in ride-sharing platforms. The main goals are to minimize wait times, optimize routes, and maximize resource utilization.

---

## Summary
- HLD focuses on system architecture.
- LLD focuses on code structure.
- DSA is used to solve problems in LLD.

---

# LECTURE 2 (OOPs Pillars: Abstraction, Encapsulation)

## History of Programming

### 1. Machine Language (0/1)
- Direct interaction with CPU
- Prone to errors
- Not scalable

### 2. Assembly Language
- Example: `MOV A, 61H`
- Prone to errors
- Not scalable (direct interaction with hardware)
- Tedious to write and maintain

### 3. Procedural Programming
- Uses functions
- Control structures: if-else, switch
- Loops
- Code is a set of instructions

#### Example (Procedural Approach)
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

### 4. Object-Oriented Programming (OOP)
- Real-world modeling
- Data security
- Highly scalable and reusable
- Objects interact with each other and have characteristics (attributes) and behaviors (methods)
- All these characteristics and behaviors are grouped into a class, making the code more organized, reusable, and easier to maintain.

#### Example (OOP Approach)
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

# LECTURE 3 (OOPs Pillars: Inheritance, Encapsulation)

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








