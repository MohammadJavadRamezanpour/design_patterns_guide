# Factory Design Pattern

## 🛑 Problem

Imagine you are building a system that creates **different types of shapes**: Circle, Square, Rectangle, etc.
If you create each shape directly in your code, adding new shapes requires modifying multiple parts of your program. This can get messy and **hard to maintain**.

---

## 🖥 Bad Code Example

```python
# Directly creating objects in client code
shape_type = "circle"
if shape_type == "circle":
    shape = Circle()
elif shape_type == "square":
    shape = Square()

shape.draw()
```

### ⚠ Problems with Bad Code

* Client code is **tightly coupled** to concrete classes.
* Adding a new shape requires modifying multiple places.
* Violates the **Open/Closed Principle**.

---

## ✅ Good Code Example (Factory Pattern)

```python
# Factory creates objects instead of the client
class ShapeFactory:
    @staticmethod
    def create_shape(shape_type):
        if shape_type.lower() == "circle":
            return Circle()
        elif shape_type.lower() == "square":
            return Square()
        else:
            raise ValueError(f"Unknown shape type: {shape_type}")

# Usage
shape = ShapeFactory.create_shape("circle")
shape.draw()
shape = ShapeFactory.create_shape("square")
shape.draw()
```

### Benefits of Good Code

* Decouples object creation from usage.
* Open/Closed Principle – Adding new shapes doesn’t require changing client code.
* Centralized, maintainable object creation logic.

---

## 🔹 How to Use

1. Identify objects that change frequently.
2. Use a Factory to create these objects instead of directly instantiating them.
3. Extend the Factory when adding new types without modifying client code.

---

## 💡 Tips

* Start with simple objects like Shapes or Products.
* Use Factory Pattern to **avoid tightly coupled code** and make your system more flexible.

Happy learning and experimenting with the Factory Pattern! 🚀
