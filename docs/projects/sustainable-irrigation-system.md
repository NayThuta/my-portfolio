# **Sustainable Irrigation System**

<div style="text-align: center; padding: 20px 0;">
  <img src="/res/contrast.jpg" alt="Contrast Between Monsoons and Drought" style="max-width: 60%; height: auto;">
  <br>
  <em>Figure: Contrast between wet monsoons and drought-struck summers in third-world farms, addressed by our solution.</em>
</div>

## **Overview**
In regions like Southeast Asia and sub-Saharan Africa, third-world farmers face the stark contrast of heavy monsoon rains and severe summer droughts, threatening crop survival. This project developed a microcontroller-based smart irrigation system to optimize water usage and enhance crop resilience using real-time environmental feedback. My primary contribution was designing the hardware layout, ensuring a robust, scalable, and cost-effective solution tailored to these challenges, driving the project from concept to prototype.

---

## **My Primary Contributions**

### **Hardware Design & Layout**
<div style="text-align: center; padding: 20px 0;">
  <img src="/res/component_breakdown.png" alt="Component Breakdown of the Smart Irrigation System" style="max-width: 100%; height: auto;">
  <br>
  <em>Figure: Physical breakdown of the system components on the transparent board.</em>
</div>

- **Overall Layout Design**: I laser-cutted a transparent board layout, enabling clear visibility of components for maintenance and troubleshooting, a key feature for rural use.
- **Component Placement**: I strategically placed placeholders for the PIC18F4550 microcontroller, rain sensor (RB1), water level sensor (ADC input), three pump relays (RB2, RB3, RB6), a button (RB0 interrupt), and status LEDs (PORTD), optimizing space and accessibility.
- **Soldering and Assembly**: I hand-soldered components onto the brown PCB, ensuring secure and reliable connections under resource constraints.
- **Wiring and Circuit Design**: 
    1. I developed an efficient circuit design, minimizing jumper wires by routing traces strategically.
    2. My design reduced complexity and improved durability, aligning with the PIC18F4550’s pin configuration.

---

## **Key Features**
- **Real-Time Environmental Feedback**: Adapts to weather conditions with rain and water level sensors, reducing water waste through dynamic adjustments, as enabled by my sensor integration.
- **Automated Pump Control**: Sequentially activates pumps based on sensor data or manual input, ensuring even distribution, a result of my relay placement.
- **Precision Irrigation with PWM**: Uses Pulse Width Modulation to fine-tune water flow, supporting diverse crop needs, facilitated by my circuit optimization.

---

## **Technical Specifications**

### **Hardware Components**
- **Microcontroller**: PIC18F4550
- **Sensors**:
    1. Rain sensor (RB1 input)
    2. Water level sensor (ADC input)
- **Actuators**: 3 pump relays (RB2, RB3, RB6)
- **User Interface**:
    1. Button (RB0 interrupt)
    2. Status LEDs (PORTD)
- **Power Management**: 12V DC power supply with voltage regulation

### **System Architecture**
<div style="text-align: center; padding: 20px 0;">
  <img src="/res/sys_arc_sis.jpg" alt="System Architecture Diagram" style="max-width: 100%; height: auto;">
  <br>
  <em>Figure: High-level system architecture for the smart irrigation system.</em>
</div>

??? note "Crucial Technical Implementation (Credit: Joseph Wong & Jonathan Chua Jie Xin)"
    <div style="padding: 10px;">
    <strong>A. Environmental Feedback and Automated Response</strong><br>
    This logic enables the system to automatically adjust water flow based on rain detection and water level, ensuring efficient irrigation:
    
    ```c
    if (PORTBbits.RB1 == 0) { // rain detected
        SetDutyCycleTo(5.0, Period); // Reduce water flow
    } else {
        SetDutyCycleTo(12.3, Period); // Normal flow
    }
    ADCON0bits.GO = 1; // Start ADC conversion
    while(ADCON0bits.GO == 1); // Wait for conversion
    if (ADRESH > HIGH) { // Water level high
        pump();
    }
    ```
    <em>This snippet demonstrates real-time adaptation to environmental conditions using sensor feedback and automated actuation.</em>
    <br><br>
    <strong>B. Pump Control Function</strong><br>
    The core actuation logic, which sequentially activates three pumps to distribute water efficiently:
    
    ```c
    void pump(void){
        PORTDbits.RD1 = 1;
        PORTBbits.RB2 = 0; delay(1000); PORTBbits.RB2 = 1;
        PORTBbits.RB3 = 0; delay(1000); PORTBbits.RB3 = 1;
        PORTBbits.RB6 = 0; delay(1000); PORTBbits.RB6 = 1;
        PORTDbits.RD1 = 0;
    }
    ```
    <em>This function is responsible for the physical actuation of the irrigation pumps, ensuring even water distribution across the system.</em>
    </div>

---

## **Challenges & Solutions**

### **Challenge 1: Ensuring Precise Component Placement**
**Problem:** Sensor accuracy depended on alignment, a challenge I tackled.

**Solution:** I created AutoCAD layouts, used meticulous soldering, optimized PCB routing, and validated alignment through testing.

### **Challenge 2: Managing Complex Wiring**
**Problem:** Multiple connections risked failure, which I addressed.

**Solution:** I designed a streamlined layout, minimized jumper wires, routed traces effectively, and enhanced durability with a transparent board.

---

## **Results & Impact**
### **Achievement of Project Scope**
The project successfully completed its intended scope, delivering a functional smart irrigation system prototype tailored for third-world farming communities. This milestone reflects the team's ability to design, assemble, and test a solution despite resource constraints, with my hardware layout and PCB design playing a key role in its realization.

### **Addressing Specific Needs**
- **Monsoon Rainfall Management**: The system’s rain sensor (connected to RB1) detects heavy rainfall and reduces water flow, preventing waterlogging during monsoons. This ensures crops aren’t overwhelmed, a common issue for farmers with limited drainage infrastructure.
- **Drought Resilience**: During dry seasons, users can trigger pumps (RB2, RB3, RB6) via the master control button (RB0) to maintain soil moisture, addressing water scarcity with minimal manual effort.
- **Affordability and Simplicity**: The minimized jumper wire design and component placement reduce production costs and maintenance needs, making it accessible for small-scale farmers.

### **Practical Outcomes**
- The prototype successfully adapted to simulated monsoon and drought cycles, proving its versatility.
- Farmers can rely on reduced manual intervention, freeing time for other tasks.

---

## **Personal Learning Points**

This project was a pivotal learning experience that enhanced my technical and professional capabilities:

- **Microcontroller and Embedded C Expertise**: Reviewing teammates’ embedded C code for the PIC18F4550 deepened my proficiency in microcontroller programming, enabling me to optimize firmware for system reliability and efficiency.
- **Circuit Analysis and Design**: Designing the PCB layout and soldering components strengthened my skills in circuit analysis and design, ensuring precise integration of sensors and actuators under resource constraints.
- **AutoCAD and Laser Cutting**: Using AutoCAD to create precise system layouts and laser cutting the transparent board layout honed my ability to produce accurate, maintainable hardware designs tailored for rural use.
- **Collaboration and Problem-Solving**: Coordinating with hardware and software teams sharpened my collaboration and problem-solving skills, allowing me to communicate technical concepts clearly and deliver solutions in challenging environments.

These lessons have equipped me to tackle complex engineering and business challenges with confidence and a solution-oriented mindset.

---

## **Demo Video**

Watch a real-life demonstration of the Sustainable Irrigation System prototype in action:

<div style="text-align: center; padding: 20px 0;">
  <video width="560" height="315" controls style="max-width: 100%; height: auto;">
    <source src="/res/demo_subbed.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <br>
  <em> Video: Sustainable Irrigation System Project Demo (Credit: Wong Wen Hui).</em>
</div>

## **Future Enhancements**

**Possible Improvements**: IoT for remote monitoring, machine learning for predictions, a mobile app, and solar power.

**Scalability Considerations**: My modular approach supports expansion, standardized components, and varied configurations. 

---

<p align="center">
  <a href="/projects/">← Back to Projects</a><span style="padding: 0 5px;"></span>|<span style="padding: 0 5px;"></span><a href="#top">↑ Back to Top</a>
</p> 