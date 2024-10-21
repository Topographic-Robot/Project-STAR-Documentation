MSP432 (Replaced by ESP32)
--------------------------

The MSP432, previously considered, is a microcontroller from Texas Instruments designed for low-power applications with a strong focus on energy efficiency and performance.

Advantages
~~~~~~~~~~

- **Low Power Consumption**: Designed to operate efficiently with minimal power.
- **High Precision**: Offers high precision in analog measurements with its integrated ADC.
- **Ease of Use**: Simplified development environment with support from Texas Instruments.

Disadvantages
~~~~~~~~~~~~~

- **Limited Connectivity**: Lacks built-in Wi-Fi and Bluetooth, requiring additional modules for connectivity.
- **Cost**: Slightly more expensive compared to the ESP32.
- **Community Support**: Less extensive community support and fewer libraries compared to the ESP32.

Decision Rationale
==================

The final decision to use the ESP32 was based on several key factors:

1. **Integrated Connectivity**: The ESP32's built-in Wi-Fi and Bluetooth are essential for the topographical mapping robot, allowing for seamless data transmission and remote control capabilities without needing additional hardware.
2. **Community and Development Resources**: The extensive libraries and community support available for the ESP32 will significantly speed up development and troubleshooting processes, ensuring a more efficient project timeline.
3. **Cost Efficiency**: The ESP32's affordability makes it a cost-effective solution, allowing for budget allocation towards other critical components of the robot.
4. **Performance Requirements**: The dual-core processor and high clock speed of the ESP32 provide the necessary computational power to handle complex mapping algorithms and data processing tasks.
5. **Flexibility and Scalability**: The ESP32 offers flexibility in programming and the ability to scale the project with additional features without significant changes to the hardware platform.
