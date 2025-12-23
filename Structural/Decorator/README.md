# Decorator Design Pattern

## 🛑 Problem

Imagine you are building a **coffee shop system** where you want to offer different add-ons like milk, sugar, or whipped cream.
If you create a separate class for every possible combination (e.g., `CoffeeWithMilk`, `CoffeeWithMilkAndSugar`), the number of classes grows quickly and is **hard to maintain**.

---

## 🖥 Bad Code Example

```python
class Coffee:
    def cost(self):
        return 5

class CoffeeWithMilk(Coffee):
    def cost(self):
        return super().cost() + 2

class CoffeeWithSugar(Coffee):
    def cost(self):
        return super().cost() + 1

# Usage
coffee1 = CoffeeWithMilk()
print(coffee1.cost())  # 7

coffee2 = CoffeeWithSugar()
print(coffee2.cost())  # 6
```

### ⚠ Problems with Bad Code

1. **Combinatorial explosion** – Each combination requires a new class.
2. **Rigid and hard to maintain** – Adding a new add-on requires creating more classes.
3. **Violates Open/Closed Principle** – Must modify or add classes for new features.

---

## ✅ Good Code Example (Decorator Pattern)

```python
from abc import ABC, abstractmethod

# Component interface
class Coffee(ABC):
    @abstractmethod
    def cost(self):
        pass

# Concrete component
class SimpleCoffee(Coffee):
    def cost(self):
        return 5

# Decorator base class
class CoffeeDecorator(Coffee):
    def __init__(self, coffee):
        self._coffee = coffee

    @abstractmethod
    def cost(self):
        pass

# Concrete decorators
class MilkDecorator(CoffeeDecorator):
    def cost(self):
        return self._coffee.cost() + 2

class SugarDecorator(CoffeeDecorator):
    def cost(self):
        return self._coffee.cost() + 1

# Usage
coffee = SimpleCoffee()
print(coffee.cost())  # 5

coffee_with_milk = MilkDecorator(coffee)
print(coffee_with_milk.cost())  # 7

coffee_with_milk_and_sugar = SugarDecorator(coffee_with_milk)
print(coffee_with_milk_and_sugar.cost())  # 8
```

---

## 💡 Benefits of Good Code

* **Flexible** – Add or remove decorators at runtime.
* **Open/Closed Principle** – No need to modify existing classes.
* **Reusable** – Decorators can be combined in any order.
* **Easy to maintain** – Adding a new feature only requires a new decorator class.

---

## 🔗 References

* [Refactoring Guru – Decorator Pattern](https://refactoring.guru/design-patterns/decorator/python)
