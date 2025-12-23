# Singleton Design Pattern

## 🛑 Problem

Imagine you are building a **logging system** where only one instance of a logger should exist throughout the application.
If multiple instances are created, it can lead to **inconsistent logs** and resource issues.

---

## 🖥 Bad Code Example

```python
class Logger:
    def __init__(self):
        self.logs = []

    def log(self, message):
        self.logs.append(message)
        print(f"Log: {message}")

# Usage
logger1 = Logger()
logger2 = Logger()

logger1.log("Starting app")
logger2.log("User logged in")

print(logger1.logs)  # ['Starting app']
print(logger2.logs)  # ['User logged in']
```

### ⚠ Problems with Bad Code

1. **Multiple instances** – Each Logger instance has its own logs.
2. **Inconsistent state** – Logs are not shared across instances.
3. **Violates Singleton principle** – Cannot guarantee a single instance.

---

## ✅ Good Code Example (Singleton Pattern)

```python
class Logger:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super(Logger, cls).__new__(cls)
            cls._instance.logs = []
        return cls._instance

    def log(self, message):
        self.logs.append(message)
        print(f"Log: {message}")

# Usage
logger1 = Logger()
logger2 = Logger()

logger1.log("Starting app")
logger2.log("User logged in")

print(logger1.logs)  # ['Starting app', 'User logged in']
print(logger2.logs)  # ['Starting app', 'User logged in']
```

---

## 💡 Benefits of Good Code

* **Single instance** – Ensures only one object exists.
* **Consistent state** – All parts of the app share the same logger.
* **Controlled access** – Centralized management of shared resources.
* **Easy to maintain** – No need to track multiple instances.

---

## 🔗 References

* [Refactoring Guru – Singleton Pattern](https://refactoring.guru/design-patterns/singleton/python)
