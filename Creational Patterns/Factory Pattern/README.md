# Factory Design Pattern

## 🛑 Problem

Imagine you are building a system that creates **different types of shapes**: Circle, Square, Rectangle, etc.
If you create each shape directly in your code, adding new shapes requires modifying multiple parts of your program. This can get messy and **hard to maintain**.

---

## 🖥 Example of Bad Approach

* Directly instantiating objects everywhere.
* Every time a new shape is added, you need to update all code where shapes are created.
* Violates the **Open/Closed Principle** because code has to be modified instead of extended.

---

## ✅ Factory Pattern (Good Approach)

The **Factory Pattern** allows you to **create objects without specifying the exact class**. A Factory class or method handles object creation, making it easier to add new types.

### How It Works

* You define a **common interface** for your products (e.g., `Shape`).
* Each concrete product implements the interface (e.g., `Circle`, `Square`).
* The Factory class decides which concrete product to create based on input.

### Benefits

* **Decouples object creation from usage** – Clients don’t need to know which exact class is being used.
* **Open/Closed Principle** – Add new shapes without modifying existing code.
* **Easy to maintain** – Centralized creation logic.

---

## 🔹 How to Use

1. Read the README to understand the concept.
2. Think about the product types and interfaces you need.
3. Imagine a Factory that returns the correct product based on input.
4. Apply it in your code to simplify object creation.

---

## 💡 Tips

* Start by identifying objects that change frequently in your system.
* Use Factory Pattern to **avoid tightly coupled code**.
* Combine with other creational patterns if needed for more complex object creation scenarios.

Happy learning and experimenting with the Factory Pattern! 🚀
