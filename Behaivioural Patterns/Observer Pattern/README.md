# Observer Design Pattern

## 🛑 Problem

Imagine you have a **news system** where multiple users want to get updates whenever a new article is published.
If you directly notify each user manually, adding a new subscriber requires changing existing code, which is **hard to maintain**.

---

## 🖥 Bad Code Example

```python
class News:
    def __init__(self):
        self.subscriber1 = None
        self.subscriber2 = None

    def set_subscriber1(self, subscriber):
        self.subscriber1 = subscriber

    def set_subscriber2(self, subscriber):
        self.subscriber2 = subscriber

    def publish_news(self, news):
        if self.subscriber1:
            print(f"{self.subscriber1} received news: {news}")
        if self.subscriber2:
            print(f"{self.subscriber2} received news: {news}")

# Usage
news = News()
news.set_subscriber1("Alice")
news.set_subscriber2("Bob")
news.publish_news("New Python Version Released!")
```

### ⚠ Problems with Bad Code

1. **Rigid design** – Adding more subscribers requires modifying the class.
2. **Violates Open/Closed Principle** – Cannot add subscribers without changing existing code.
3. **Hard to scale** – Adding many subscribers becomes messy.

---

## ✅ Good Code Example (Observer Pattern)

```python
from abc import ABC, abstractmethod

# Observer interface
class Subscriber(ABC):
    @abstractmethod
    def update(self, message):
        pass

# Concrete observers
class User(Subscriber):
    def __init__(self, name):
        self.name = name

    def update(self, message):
        print(f"{self.name} received news: {message}")

# Subject
class NewsPublisher:
    def __init__(self):
        self.subscribers = []

    def subscribe(self, subscriber):
        self.subscribers.append(subscriber)

    def unsubscribe(self, subscriber):
        self.subscribers.remove(subscriber)

    def publish(self, news):
        for subscriber in self.subscribers:
            subscriber.update(news)

# Usage
alice = User("Alice")
bob = User("Bob")

publisher = NewsPublisher()
publisher.subscribe(alice)
publisher.subscribe(bob)

publisher.publish("New Python Version Released!")
publisher.unsubscribe(bob)
publisher.publish("Python 4.0 Coming Soon!")
```

---

## 💡 Benefits of Good Code

* **Flexible** – Can add or remove subscribers without changing the subject.
* **Open/Closed Principle** – Extending the system doesn’t require modifying existing code.
* **Scalable** – Works well even with many subscribers.
* **Easy to maintain and test** – Each observer is independent.

---

## 🔗 References

* [Refactoring Guru – Observer Pattern](https://refactoring.guru/design-patterns/observer/python)
