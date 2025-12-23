# Factory Design Pattern

## 🛑 Problem

Imagine you are building a program that creates different **shapes** like Circle, Square, or Rectangle.
If you create each shape directly in your code, adding a new shape means you have to change a lot of code. This can be **confusing and hard to manage**.

---

## 🖥 Bad Code Example

```python
# Directly creating objects in your code
shape_type = "circle"
if shape_type == "circle":
    shape = Circle()
elif shape_type == "square":
    shape = Square()

shape.draw()
```

### ⚠ Problems with Bad Code

* The code is **tightly connected** to the shape classes.
* Adding a new shape means changing this code.
* Hard to **maintain and extend**.

---

## ✅ Good Code Example (Factory Pattern)

```python
# Factory class creates objects for you
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

* **Easier to use** – Client code doesn’t need to know which class is created.
* **Easy to add new shapes** – Just update the Factory, no need to touch other code.
* **Cleaner and more organized** – All creation logic is in one place.

---

## 🔹 How to Use

1. Identify objects that are created in many places.
2. Use a Factory to create them instead of doing it directly.
3. When adding new objects, only update the Factory.

---

**Tip:** Start with simple objects like Shapes or Products. Using Factory makes your code more **flexible and easier to maintain**.

Happy coding! 🚀
