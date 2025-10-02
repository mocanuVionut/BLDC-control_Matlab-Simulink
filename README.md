# BLDC-control_Matlab-Simulink
This project delivers a full **brushless DC (BLDC) motor control system** developed in MATLAB/Simulink and deployed on a physical Texas Instruments board. It combines simulation and real hardware execution to regulate torque, current, and speed in real time.

- Features cascaded control loops (outer speed loop, inner current loops)  
- Supports both **PI** and **LQR** controllers  
- Includes SCI interface for real-time monitoring and parameter tuning  
- Bridges theory and practical system validation on hardware  

# Model Structure and Functionalities
The SIMULINK model consists of several interconnected modules:

Estimation Module: Determines the position of the motor's three phases and calculates its rotational speed.

Voltage Control Module: Allows switching between manual and automatic operation modes. It regulates the direct voltage (Ud), associated with the magnetic flux, and the quadrature voltage (Uq), associated with the motor's torque.

Serial Communication Interface (SCI) Module: Handles data reception and transmission between the model and a host PC, allowing for real-time monitoring and adjustment.

# Control Methodology
To manage the motor's performance, two types of controllers were implemented, each with distinct characteristics:

**PI** (Proportional-Integral) Controller: A simple and fast solution, effective in many applications.

**LQR** (Linear-Quadratic Regulator) Controller: An advanced method that provides stable and robust control.

These controllers were applied within a complex control structure:

1. Current Control: The PI and LQR controllers were used separately to regulate the motor currents. These currents are measured by monitoring the voltage drop across three shunt resistors.

2. Speed Control: To regulate the speed, the two controller types (PI and LQR) were combined in a cascaded control structure, where the outer speed loop generates the references for the inner current loop.

# Monitoring and Potential for Optimization
The control results can be visualized in real-time through a dedicated interface, "PC_host_SCI_interface_PI". Data transmission via the SCI protocol offers a significant advantage: the ability to dynamically modify control parameters (such as the speed reference or controller gains) without needing to stop and restart the entire program.

In the current speed control implementation, the direct voltage (Ud) was set to zero, with the control focusing exclusively on the quadrature component (Uq) to maximize torque. As a direction for future development, the Field Weakening method can be implemented. This involves applying a negative value to the Ud voltage, allowing the motor to achieve speeds that exceed its nominal speed.
