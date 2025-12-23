# Adapter Design Pattern

## 🛑 Problem

Imagine you have a **drawing application** that works with a `VectorShape` interface, but you also want to use `RasterShape` objects.
Since their interfaces are different, you cannot use `RasterShape` directly with your existing code. Making changes everywhere is **tedious and error-prone**.

---

## 🖥 Bad Code Example

```python
class VectorShape:
    def draw_vector(self):
        print("Drawing vector shape")

class RasterShape:
    def draw_raster(self):
        print("Drawing raster shape")

# Client code expects objects with draw_vector()
def draw_all(shapes):
    for shape in shapes:
        shape.draw_vector()

# Usage
vector = VectorShape()
raster = RasterShape()

# This crashes because RasterShape doesn't have draw_vector()
draw_all([vector, raster])  
# AttributeError: 'RasterShape' object has no attribute 'draw_vector'
```

### ⚠ Problems with Bad Code

1. **Incompatible interfaces** – Cannot use RasterShape where VectorShape is expected.
2. **Tightly coupled code** – Client must know about both types.
3. **Hard to maintain** – Every place expecting VectorShape needs changes.

---

## ✅ Good Code Example (Adapter Pattern)

```python
# Target interface
class VectorShape:
    def draw_vector(self):
        print("Drawing vector shape")

# Adaptee
class RasterShape:
    def draw_raster(self):
        print("Drawing raster shape")

# Adapter
class RasterToVectorAdapter(VectorShape):
    def __init__(self, raster_shape):
        self.raster_shape = raster_shape

    def draw_vector(self):
        # Translate the method call to the adaptee's method
        self.raster_shape.draw_raster()

# Usage
raster = RasterShape()
adapter = RasterToVectorAdapter(raster)
adapter.draw_vector()  # Works with existing code expecting VectorShape
```

---

## 💡 Benefits of Good Code

* **Compatible interfaces** – Adapter allows using existing classes without changing them.
* **Loose coupling** – Client code depends on the Target interface only.
* **Flexible** – You can adapt multiple classes easily without modifying existing code.
* **Maintainable** – Adding new adapters does not affect client code.

---

## 🔗 References

* [Refactoring Guru – Adapter Pattern](https://refactoring.guru/design-patterns/adapter/python)
