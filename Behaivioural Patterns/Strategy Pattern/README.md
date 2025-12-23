# Strategy Design Pattern

## 🛑 Problem

Imagine you are building a **payment system** that supports multiple payment methods: Credit Card, PayPal, Bitcoin, etc.
Without a flexible design, adding a new payment method requires modifying existing code. This violates the **Open/Closed Principle** and leads to messy, hard-to-maintain code.

---

## 🖥 Bad Code Example

```python
# Everything hardcoded in one class
class Payment:
    def pay_credit_card(self, amount):
        print(f"Paid {amount} using Credit Card.")

    def pay_paypal(self, amount):
        print(f"Paid {amount} using PayPal.")

# Usage
payment = Payment()
payment.pay_credit_card(100)
payment.pay_paypal(200)
```

---

## ⚠ Problems with Bad Code

1. **Rigid design** – Adding a new payment method requires changing the `Payment` class.
2. **Violates Open/Closed Principle** – The class is not closed for modification.
3. **Tightly coupled code** – Context and algorithms are mixed.
4. **Hard to test and maintain** – Each change risks breaking existing methods.

---

## ✅ Good Code Example (Strategy Pattern)

```python
from abc import ABC, abstractmethod

# Strategy interface
class PaymentStrategy(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

# Concrete strategies
class CreditCardPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"Paid {amount} using Credit Card.")

class PayPalPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"Paid {amount} using PayPal.")

# Context
class PaymentContext:
    def __init__(self, strategy: PaymentStrategy):
        self.strategy = strategy

    def set_strategy(self, strategy: PaymentStrategy):
        self.strategy = strategy

    def pay_amount(self, amount):
        self.strategy.pay(amount)

# Usage
context = PaymentContext(CreditCardPayment())
context.pay_amount(100)

context.set_strategy(PayPalPayment())
context.pay_amount(200)
```

---

## 💡 Benefits of Good Code

* **Flexible design** – Can switch algorithms at runtime.
* **Open/Closed Principle** – Adding a new payment method does not modify existing code.
* **Loose coupling** – Context is separated from algorithm implementations.
* **Maintainable and testable** – Each strategy is independent and easy to test.

---

## 🔗 References

* [Refactoring Guru – Strategy Pattern](https://refactoring.guru/design-patterns/strategy/python)
