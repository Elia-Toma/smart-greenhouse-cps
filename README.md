## 🌿 Smart Greenhouse CPS: From Model to Reality

A Cyber-Physical System (CPS) simulation modelling a smart greenhouse environment. Built using Ptolemy II, this project simulates environmental feedback loops, adaptive control logic, and a wireless communication topology.

## 📖 Project Overview

This project models a Cyber-Physical System for smart agriculture. It simulates the continuous natural fluctuations of a greenhouse environment and the discrete control logic required to maintain optimal conditions for plant growth.

The system handles communications, control logic, and continuous processes, dealing with real-world problems such as sensor noise and latency.

## 🏗️ System Architecture

The model is divided into several interconnected composite actors:

* 🌍 **Global Environment:** Mathematically models the natural chaos of the greenhouse.

  * **Temperature:** Fluctuates using a cosine function.

  * **Humidity:** Fluctuates using a sine function.

* **Distributed Sensors (Humidity & Temperature):** Simulate real-world sensors measuring the environment. To test the robustness of the control logic, these sensors are not ideal: they include **stochastic noise injection** (using Gaussian actors) and latency simulations.

* 🧠 **Adaptive Controller:** The brain of the system. It receives packets from the sensors and makes dynamic decisions. To prevent rapid, inefficient cycling of the actuators near the threshold values, it implements **hysteresis logic**:

  * **Sprinkler:** Activates when Humidity < 57%. Deactivates when Humidity > 67%.

  * **Vent:** Activates when Temperature < 20°C. Deactivates when Temperature > 25°C.

* **Intervention Actuators (Sprinkler & Vent):** Modulate the flow of water and air based on the commands received from the controller, feeding back into the environmental state.

* 📈 **Monitor:** Plots the real-time data, allowing users to compare the "ground truth" (ideal environment) with the "measured reality" (noisy sensor data).

## Networking & Directors

The simulation relies on two main Ptolemy II Directors:

1. **Discrete Event (DE) Director:** Orchestrates execution by processing timed events in strict chronological order, guaranteeing determinism.

2. **Wireless Director:** Decouples the component topology from connection logic. It uses publish/subscribe semantics via named channels (`C_Ext_Data`, `C_Int_Data`, `C_Controller`) to simulate an ad-hoc IoT network where physical wiring is not present.

## 🚀 How to Run the Simulation

To open and run this project, you need to have [Ptolemy II](https://ptolemy.berkeley.edu/ptolemyII/) installed on your machine.

1. Clone this repository: git clone https://github.com/YOUR_USERNAME/smart-greenhouse-cps.git


2. Open Ptolemy II (Vergil).

3. Navigate to `File -> Open` and select the `greenhouse_cps_model.xml` file.

4. Click the **Run** button (play icon) in the toolbar.

5. Plotter windows will open automatically, displaying the real-time graphs for temperature and humidity.
