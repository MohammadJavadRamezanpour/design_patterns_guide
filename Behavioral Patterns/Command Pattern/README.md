# Command Design Pattern

## 🛑 Problem

Imagine you are building a **remote control app** that can turn devices ON and OFF (like a Light or a Fan).
If you directly put all the logic inside the remote, adding new devices or actions will make the code **messy and hard to change**.

---

## 🖥 Bad Code Example

```python
class RemoteControl:
    def press_button(self, device, action):
        if device == "light" and action == "on":
            print("Light turned ON")
        elif device == "light" and action == "off":
            print("Light turned OFF")
        elif device == "fan" and action == "on":
            print("Fan turned ON")
        elif device == "fan" and action == "off":
            print("Fan turned OFF")
```

### ⚠ Problems with Bad Code

* Too many `if-else` conditions.
* Adding a new device means changing this class.
* The remote control knows too much about device logic.
* Hard to maintain as the app grows.

---

## ✅ Good Code Example (Command Pattern)

```python
# Command interface
class Command:
    def execute(self):
        pass

# Receiver classes
class Light:
    def on(self):
        print("Light turned ON")

    def off(self):
        print("Light turned OFF")

# Concrete Commands
class LightOnCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.on()

class LightOffCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.off()

# Invoker
class RemoteControl:
    def press_button(self, command):
        command.execute()

# Usage
light = Light()
remote = RemoteControl()

remote.press_button(LightOnCommand(light))
remote.press_button(LightOffCommand(light))
```

---

## 💡 Benefits of Good Code

* No large `if-else` blocks.
* Easy to add new commands without changing existing code.
* The remote control is simple and clean.
* Actions are separated from the object that calls them.

---

## 🔹 When to Use Command Pattern

* When you want to separate **who calls an action** from **how it is performed**.
* When you have many actions and want clean, organized code.
* When adding new actions should be easy.

---

This pattern keeps your code **flexible, clean, and easy to extend**.
