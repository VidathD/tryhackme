# Attacking ICS Plant #1

## Introduction to OT/ICS

Operational Technology (OT) refers to systems used to monitor and control industrial operations. Industrial Control Systems (ICS) includes systems used to monitor and control industrial processes.

If IT operators have dozens of years of experience securing networks, systems and applications, OT operators are pretty new to this topic. Moreover, in OT/ICS development availability is always preferred over integrity and confidentiality. In other words ICS software are designed to be fast but, often, insecure.

Supervisory Control and Data Acquisition (SCADA) systems are used to control and automate industrial processes. SCADA systems include:

- Supervisory computers: the servers used to manage the process gathering data on the process and communicating with filed devices (PLC/RTU). In smaller deployments HMI is embedded in a single computer, in larger deploy HMI is installed into a dedicated computer.
- Programmable Logic Controllers (PLC): digital computers used mainly for automating industrial processes. They are used to continuously monitor sensors (input) and make decisions controlling devices (output).
- Remote Terminal Units (RTU): nowadays, RTUs and PLCs functionalities overlap with each other. RTUs are usually preferred for wider geographical telemetry, whereas PLCs are better with local controls.
- Communication network: the network connecting all SCADA components (Ethernet, Serial, telephones, radio, cellular...). Network failures do not necessarily impact negatively on the plant process.  Both RTUs and PLCs should be designed to operate autonomously, using the last instruction given from the supervisory system.
- Human Machine Interface (HMI): displays a digitalized representation of the plant. Operators can interact with the plant issuing commands using mouse, keyboards or touch screens. Operators can make supervisory decisions adjusting or overriding the normal plant behaviour.


In short and simple words:

- industries are managed by sophisticated, mission critical computers (SCADA systems);
- security is not the first priority in OT/ICS;
- operators can manually override the behaviour of the plant via mouse/keyboard/touchscreen, locally or remotely;
- a malicious software can override the behaviour of the plant like HMI does.

For more information see [Guide to Industrial Control Systems (ICS) Security (NIST 800-82)](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-82r2.pdf).

---

## Introduction to Modbus Protocol

Modbus is an industrial protocol developed by Modicon, acquired by Schneider Electric. Modbus is widely used to connect industrial devices; protocol specification is available and royalty-free.

Modbus protocol is a master/slave protocol: the master reads and writes slaves' registers.

Modbus RTU is usually used via RS-485 (serial network): one master is present with one or more slaves. Each slave has a unique 8-bit address. 

Modbus data is used to read and write “registers” which are 16-bit long. The most common register is called “holding register” which is readable and writable; registry type “input register” is readable only. The registers “coil” and “discrete input” are 1-bit long: coils are readable and writable, discrete inputs are readable only.

Modbus register types:
- Discrete Input (Status Input): 1 bit, RO
- Coil (Discrete Output): 1 bit, R/W
- Input Register: 16 bit, RO
- Holding Register: 16 bit R/W

Most commonly Modbus function:

| Function Code | Register Type                    |
| ------------- | -------------------------------- |
| 1             | Read Coil                        |
| 2             | Read Discrete Input              |
| 3             | Read Holding Registers           |
| 4             | Read Input Registers             |
| 5             | Write Single Coil                |
| 6             | Write Single Holding Register    |
| 15            | Write Multiple Coils             |
| 16            | Write Multiple Holding Registers |

Modbus TCP encapsulates Modbus RTU request and response data packets in a TCP packet transmitted over standard Ethernet networks. The TCP Modbus standard port is 502.

For more information see [Modbus 101 - Introduction to Modbus](https://www.csimn.com/CSI_pages/Modbus101.html).

Before starting, download the attached script package and install the Modbus TCP library for Python with the following command:

```
pip3 install pymodbus==1.5.2
```

### Answers

Create a venv with and install pymodbus. The module `six` also seems to be missing. Install it as well.
```zsh
python3 -m venv ics1
pip3 install pymodbus==1.5.2 six
```

1. Which is the function used to read holding registers in pymodbus library?
> **Answer: read_holding_registers**
2. Which is the function used to write holding registers in pymodbus library?
    - write_register
---

## Discovery

Connect to the plant using the browser ([http://MACHINE_IP](http://machine_ip)) and learn how the bottle-filling plant works.

We have three phases:
1. Initialization: the plant is starting from the beginning. The roller moves the first bottle under the nozzle.
2. Filling: once a bottle is under the nozzle, the nozzle opens and the water flows in the bottle.
3. Moving: once the bottle is filled, the roller starts again moving the next empty bottle under the nozzle.

When the phase 3 ends, the plant starts again with phase 2.

From the three phases described above, we can observe:
- Sensors: used to read a state of the plant.
- Actuators: used to alter the state of the plant.

Example: a sensor can detect if a bottle is under the nozzle, while an actuator can open or close the nozzle.

Mind we can press the `ESC` button to start the plant from the beginning.

VirtuaPlant can be downloaded from [GitHub](https://github.com/jseidl/virtuaplant/network/members).

### Answers

1. 