
## 🐧 From Linux to Applications

After learning Linux, the next step is to **apply that knowledge by building applications**.

---

## 📱 Types of Applications

Applications are broadly categorized into:

### 1. Client Applications
- Installed directly on a user’s computer  
- Example: Desktop software, local tools  

### 2. Web-Based Applications
- Hosted on servers  
- Accessed over the internet via browsers  
- Examples:  
  - Amazon  
  - Flipkart  
  - Myntra  

---

## 💡 What is an Application?

An **application** is a collection of features designed to solve a specific **business use case**.

---

## 🛠️ How Are Applications Built?

Typically, the development process involves:

1. Gathering requirements  
2. Choosing the **technology stack & programming language**  
3. Developing features  
4. Building the application (binary/package)  
5. Deploying or distributing the application  

---

## 🏗️ Web Application Architectures

There are two primary architecture styles:

### 1. Monolithic Architecture (Traditional)

In a monolithic setup:

- All features are part of a **single application**
  - Frontend  
  - Catalogue  
  - Cart  
  - Payment  
  - Shipping  
  - Dispatch  
- Runs as a **single unit on one server**

#### ❌ Limitations:

- Failure in one component affects the entire application  
- Locked into a **single technology stack** (e.g., Java, Python, Go)  
- Cannot scale individual components independently  
- Difficult to adopt different technologies for different features  

---

### 2. Microservices Architecture (Modern Approach)

In a microservices setup:

- Each feature is built as an **independent service**
- Services can use **different technologies**
  - Java, Node.js, Go, Python, etc.
- Each service is deployed **independently**
- Can run on:
  - Servers  
  - Kubernetes  

#### ✅ Advantages:

- Independent development and deployment  
- Technology flexibility  
- Better scalability (scale individual services)  
- Fault isolation (one service failure doesn’t break everything)  

#### ⚠️ Challenges:

- Complex to design and maintain  
- Requires strong DevOps and monitoring practices  

---

## 🛒 Example: E-Commerce Application

### Monolithic Approach:
- Entire system (cart, payment, shipping, etc.) is one application  
- Runs on a single server  
- Hard to scale or modify individual features  

### Microservices Approach:
- Each feature is a separate service  
- Can use different technologies per service  
- Can scale services independently  

---

## ⚖️ Which Architecture is Better?

There is **no one-size-fits-all answer**.

- **Microservices** → Flexible but complex  
- **Monolithic** → Simple but less scalable  

👉 The choice depends on:
- Business requirements  
- Team expertise  
- Cost considerations  
- Performance needs  

---

## 💰 Key Decision Factor: ROI

Architecture decisions should be driven by:

> **ROI (Return on Investment)**

- What value does the architecture provide?
- Is the complexity justified?

---

## 🔄 Industry Trends

- Many companies **migrate from Monolithic → Microservices**
- Some even **move back to Monolithic** due to:
  - Cost issues  
  - Performance concerns  
  - Operational complexity  

---

## 🎬 Real-World Example

Microservices have existed for a long time, but :contentReference[oaicite:0]{index=0} popularized them at scale.

---

## 📝 Assignment

1. What is **SQL vs NoSQL database**?  
2. When should you use **SQL vs NoSQL**?  
3. Who decides whether to use **Monolithic or Microservices architecture**?  

---

## 📌 Final Thought

> Choose architecture based on **your application needs**, not trends.