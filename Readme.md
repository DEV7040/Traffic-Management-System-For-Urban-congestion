# 🚦 Traffic Management Simulation

A **Java Swing-based Traffic Management Simulation** that demonstrates dynamic traffic signal control for multiple lanes. The system simulates vehicle detection, automatically manages traffic lights, and provides **emergency vehicle priority** for faster traffic clearance.

## 📌 Project Overview

Traditional traffic signals operate using fixed timers, which can cause unnecessary waiting when some lanes have little or no traffic.

This project demonstrates a simple **intelligent traffic management approach** where:

* 🚗 Vehicles are randomly generated in different lanes.
* 🟢 A lane with detected vehicles can receive a green signal.
* ⏱️ A maximum waiting time is implemented to prevent excessive delays.
* 🚨 Emergency vehicles can be given priority.
* 🔴 Traffic signals automatically return to red after the green-light duration.

The project is developed using **Java Swing GUI**.

---

## ✨ Features

* 🚦 **4-Lane Traffic Simulation**
* 🚗 Random vehicle generation
* 🟢 Automatic green-light activation
* 🔴 Automatic red-light switching
* ⏱️ Maximum waiting time control
* 🚨 Emergency vehicle priority
* 🖥️ Interactive Java Swing GUI
* 📊 Real-time vehicle count
* 🔄 Continuous traffic simulation using a timer

---

## 🛠️ Technologies Used

| Technology     | Purpose                           |
| -------------- | --------------------------------- |
| **Java**       | Core programming language         |
| **Java Swing** | Graphical User Interface          |
| **AWT**        | GUI components and event handling |
| **OOP**        | Object-oriented program structure |
| **Timer**      | Periodic traffic simulation       |
| **Random**     | Vehicle generation                |

---

## 🏗️ Project Structure

```text
TrafficGUI/
│
├── TrafficGUI.java
└── README.md
```

---

## ⚙️ How It Works

### 1. Traffic Simulation

Every **1 second**, the simulation checks all four lanes.

Vehicles are randomly added to lanes:

```java
if (rand.nextInt(10) < 3)
    lane.addVehicle();
```

### 2. Vehicle Detection

When vehicles are detected in a lane, the traffic signal changes from:

```text
🔴 RED → 🟢 GREEN
```

The vehicles waiting in that lane are then cleared.

### 3. Maximum Waiting Time

If a lane has been waiting for **60 seconds**, the system automatically gives it a green signal to prevent indefinite waiting.

### 4. Green Signal Duration

A green signal remains active for approximately **5 seconds** before changing back to red.

```text
🟢 GREEN
   ↓
5 seconds
   ↓
🔴 RED
```

### 5. Emergency Vehicle Priority

The emergency button gives **Lane 1** immediate priority.

```text
🚨 Emergency Vehicle Detected
             ↓
      Lane 1 Priority
             ↓
        🟢 GREEN
```

---

## 🖥️ GUI

The application provides a graphical interface containing:

* Four traffic lanes
* Vehicle count for each lane
* Traffic-light indicators
* Emergency vehicle button
* Real-time simulation

---

## ▶️ How to Run

### Prerequisites

Make sure **Java JDK** is installed.

Check your Java version:

```bash
java -version
```

Check the compiler:

```bash
javac -version
```

### Compile

Open the terminal in the project folder and run:

```bash
javac TrafficGUI.java
```

### Run

```bash
java TrafficGUI
```

The Traffic Management Simulation window will open.

---

## 🧠 Concepts Demonstrated

This project is useful for understanding:

* Java Classes and Objects
* Inheritance
* Encapsulation
* Java Swing
* Event Handling
* ActionListener
* JFrame and JPanel
* GridLayout
* BorderLayout
* Timers
* Random Number Generation
* GUI Painting
* Basic traffic-control logic

---

## 🚀 Future Improvements

The project can be extended with:

* 🚗 Different vehicle types
* 🚑 Separate ambulance detection
* 🚒 Fire truck priority
* 🚓 Police vehicle priority
* 📷 Camera-based vehicle detection
* 📊 Traffic statistics dashboard
* 🧠 AI-based traffic prediction
* 🚦 Adaptive traffic signal timing
* 🛣️ More than four lanes
* 📈 Traffic density graphs
* 🔊 Emergency vehicle alerts

---

## 🎯 Project Objective

The main objective of this project is to demonstrate how **dynamic traffic signal management** can be implemented using Java programming and GUI technologies.

It serves as an educational simulation and can be further developed into a more advanced **Smart Traffic Management System**.

---

## 👨‍💻 Author's

Devesh Gujarathi
Dhananjay Gaikwad
Viraj Hiray
Chaitanya Suryawanshi
Shruti Shinde
Aditi Shinde

Computer Engineering Student



This project is created for **educational and academic purposes**.
