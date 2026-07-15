# Object-Oriented Design (OOD)

> Designing classes, interfaces, and patterns.

---

## Introduction

Object-Oriented Design (OOD) questions often appear in Amazon loops or interviews for Object-Oriented heavy languages (Java, C#). 

Unlike System Design (which focuses on servers and databases), OOD focuses on how you structure code within a single application.

You might be asked to: *"Design a Parking Lot"* or *"Design an Elevator System"*.

---

## The 45-Minute Framework

### 1. Clarify Requirements (5 mins)
- *Parking Lot:* Can it handle motorcycles, cars, and buses? Does it have multiple floors? How is payment handled?

### 2. Identify Core Entities (10 mins)
Extract the nouns from the requirements. These become your classes.
- `ParkingLot`, `Level`, `ParkingSpot`, `Vehicle`, `Ticket`.

### 3. Identify Relationships (10 mins)
How do the classes interact? Determine Inheritance, Composition, and Aggregation.
- A `Vehicle` is a base class. `Car` and `Motorcycle` inherit from `Vehicle`.
- A `ParkingLot` *has a* list of `Level` objects (Composition).
- A `Level` *has a* list of `ParkingSpot` objects.

### 4. Define the APIs (20 mins)
Write the skeleton code for the classes, focusing on the public methods. You usually don't need to implement the internal logic of every method unless asked.

```python
from enum import Enum
from abc import ABC, abstractmethod

# 1. Enums for Types
class VehicleSize(Enum):
    MOTORCYCLE = 1
    COMPACT = 2
    LARGE = 3

# 2. Abstract Base Classes
class Vehicle(ABC):
    def __init__(self, license_plate: str, size: VehicleSize):
        self.license_plate = license_plate
        self.size = size
        self.spots_needed = 1
        
    @abstractmethod
    def can_fit_in_spot(self, spot) -> bool:
        pass

# 3. Concrete Implementations
class Car(Vehicle):
    def __init__(self, license_plate: str):
        super().__init__(license_plate, VehicleSize.COMPACT)
        
    def can_fit_in_spot(self, spot) -> bool:
        return spot.size in [VehicleSize.COMPACT, VehicleSize.LARGE]
```

---

## SOLID Principles

Interviewers explicitly look for adherence to the SOLID principles in your design.

1. **Single Responsibility:** A class should do one thing. (A `Ticket` class should hold time data, it should not calculate prices. A `PriceCalculator` class should handle the math).
2. **Open/Closed:** Classes should be open for extension but closed for modification. (If we add a `Bus` type, we shouldn't have to rewrite the `ParkingLot` logic).
3. **Liskov Substitution:** A subclass should be able to replace its superclass without breaking the program.
4. **Interface Segregation:** Don't force classes to implement interfaces they don't use.
5. **Dependency Inversion:** Depend on abstractions, not concretions.

---

## Python Specifics for OOD

While Python is not as strictly Object-Oriented as Java, you must show you know how to write clean OOP in Python.

- Use the `enum` module for types.
- Use the `abc` module (`ABC`, `@abstractmethod`) to simulate Java Interfaces/Abstract classes.
- Use Type Hinting extensively.
- Understand the difference between class attributes and instance attributes (`self.var`).

---

## Key Takeaways

- Extract nouns to find Classes, extract verbs to find Methods.
- Build from the bottom up (start with `Vehicle` before building `ParkingLot`).
- Demonstrate knowledge of SOLID principles by heavily using inheritance and abstract classes.

---

## Related Topics

- [Python Classes](../part-09-object-oriented-python/01-classes-and-objects.md)
