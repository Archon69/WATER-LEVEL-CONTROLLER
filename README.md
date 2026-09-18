# Automatic Water Level Controller Using Verilog HDL

## 📌 Project Overview

This project implements an **automatic water level controller using Verilog HDL** and a **Finite State Machine (FSM)**.

The system monitors the water level of a tank using three sensors placed at approximately **30%, 60%, and 90%** levels. Based on the sensor conditions, the FSM determines the current water level and controls the water pump.

The design was developed and simulated using **Verilog HDL** and can be implemented on an FPGA using tools such as **Xilinx Vivado**.

---

## 🎯 Objectives

* Design an automatic water level monitoring system.
* Implement the controller using an FSM.
* Monitor water levels at 30%, 60%, and 90%.
* Automatically control the water pump.
* Indicate water levels using LEDs.
* Verify the design using a Verilog testbench.
* Analyze the design using simulation waveforms.

---

## 🧠 FSM States

The controller contains four states:

| State  | Binary Code | Description               |
| ------ | ----------- | ------------------------- |
| EMPTY  | `00`        | Water level below 30%     |
| FILL30 | `01`        | Water level around 30–60% |
| FILL60 | `10`        | Water level around 60–90% |
| FULL   | `11`        | Water level reaches 90%   |

### State Encoding

```text
EMPTY  = 2'b00
FILL30 = 2'b01
FILL60 = 2'b10
FULL   = 2'b11
```

---

## 🔄 FSM Operation

The basic operation of the controller is:

```text
              sensor30
   EMPTY -----------------> FILL30
                              |
                              | sensor60
                              ↓
                           FILL60
                              |
                              | sensor90
                              ↓
                            FULL
```

When the water level decreases, the FSM moves back toward the lower-level states.

```text
FULL -----> FILL60 -----> FILL30 -----> EMPTY
       sensor90       sensor60       sensor30
```

---

## ⚙️ Inputs

| Input      | Description            |
| ---------- | ---------------------- |
| `clk`      | System clock           |
| `rst`      | Reset signal           |
| `sensor30` | 30% water-level sensor |
| `sensor60` | 60% water-level sensor |
| `sensor90` | 90% water-level sensor |

---

## 💡 Outputs

| Output     | Description                              |
| ---------- | ---------------------------------------- |
| `motor`    | Controls the water pump                  |
| `led30`    | Indicates 30% sensor status              |
| `led60`    | Indicates 60% sensor status              |
| `led90`    | Indicates 90% sensor status              |
| `ledFill`  | Indicates filling operation              |
| `ledDrain` | Indicates draining/lower-level condition |

---

## 🚰 Pump Control

The pump is controlled according to the FSM state.

* When the tank is empty or the water level is below the required level, the motor can be activated.
* As the water level increases, the FSM progresses through the intermediate states.
* When the tank reaches the `FULL` state, the motor is switched OFF.
* When the water level falls, the FSM moves toward the lower states and the pump can be activated again.

---

## 🧪 Simulation

The design is verified using a Verilog testbench.

The testbench generates:

* Clock signal
* Reset signal
* 30% sensor input
* 60% sensor input
* 90% sensor input

Different combinations of sensor signals are applied to verify the FSM transitions and motor/LED outputs.

### Test Sequence

```text
Reset
  ↓
Empty Tank
  ↓
30% Sensor Active
  ↓
60% Sensor Active
  ↓
90% Sensor Active
  ↓
Full Tank
  ↓
Water Level Decreases
  ↓
30% Sensor Active
  ↓
Pump Activated Again
```

---

## 🛠️ Tools Used

* **Verilog HDL**
* **Xilinx Vivado**
* **Vivado Simulator**
* **FPGA-based RTL design**
* **Finite State Machine (FSM)**

---

## 📁 Project Structure

```text
water-level-controller/
│
├── README.md
│
├── rtl/
│   └── water_lvl_controller.v
│
├── simulation/
│   └── testbench.v
│
├── docs/
│   └── block_diagram.png
│
└── screenshots/
    └── waveform.png
```

---

## 📊 Expected Simulation

The simulation waveform should show:

* Sensor inputs changing according to the test sequence.
* FSM state transitions from `EMPTY` → `FILL30` → `FILL60` → `FULL`.
* Motor turning OFF when the tank reaches the `FULL` state.
* FSM returning toward the lower states when the water level decreases.
* LED outputs changing according to the sensor and FSM conditions.

---

## 🚀 Future Improvements

The project can be further improved by adding:

* Real water-level sensors.
* ADC-based continuous water-level measurement.
* LCD/OLED water-level display.
* Buzzer for overflow indication.
* Manual/automatic pump selection.
* FPGA board implementation.
* Motor driver/relay interface.
* IoT-based water-level monitoring.
* Fault detection for sensor failure.

---

## 👨‍💻 Author

**Ameet Kumar Sahoo**

B.Tech – Electronics & Telecommunication Engineering

---

## 📜 License

This project is intended for educational and academic purposes.
