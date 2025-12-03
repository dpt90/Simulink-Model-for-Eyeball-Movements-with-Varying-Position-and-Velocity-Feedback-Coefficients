# Simulink-Model-for-Eyeball-Movements-with-Varying-Position-and-Velocity-Feedback-Coefficients

## **1. Introduction**

This project presents the implementation and analysis of a Simulink model that represents the dynamics of human eyeball movement with variable position and velocity feedback gains. The model is based on a simplified biomechanical representation of the extraocular muscle system, incorporating torque generation, viscous damping, and proportional feedback loops.

The objective of this experiment is to observe how different values of position feedback gain (Kₚ) and velocity feedback gain (Kᵥ) influence the transient and steady‑state response of the eye movement system.

---

## **2. System Description**

Eye movements are controlled by the extraocular muscles, which are innervated by cranial nerves responsible for executing precise motion within the orbit. The muscles attach to the sclera at one end and anchor to the bony orbit at the other. Contraction generates torque that rotates the eyeball.

A simplified dynamic model of the eye is considered, where:

* **J** represents the moment of inertia of the eyeball about its axis of rotation.
* **B** represents the viscous damping coefficient associated with rotational movement.
* **G** is the gain that converts the neural control signal into torque.
* **θ** is the angular position of the eyeball.
* **θₑᵣₑf** is the target angular position.
* Position feedback is applied with gain **Kₚ > 0**.
* Velocity feedback is applied with gain **Kᵥ > 0**.

---

## **3. Mathematical Model**

Given the system parameters:

```bash
G/J = 14400   (rad/s^2)
B/J = 24      (rad/s)
```

---

### **3.1 Transfer Function**

The open-loop transfer function of the plant (control input → system output) is:

```bash
H(s) = G / (J*s + B)
```

To normalize the transfer function, divide numerator and denominator by **J**:

```bash
H(s) = (G/J) / (s + B/J)
```

Substituting the given numerical values:

```bash
H(s) = 14400 / (s + 24)
```

This normalized transfer function is used as the base plant in the Simulink model.

---

## **4. Simulink Model Configuration**

Three scenarios are implemented to study the impact of variations in feedback gains:

### **a. Case 1: Position Feedback Only**

* ( K_p = 1 )
* ( K_v = 0 )

<img width="1920" height="775" alt="model a " src="https://github.com/user-attachments/assets/383359d0-35a8-47a4-8b06-1e0fb1613740" />

### **b. Case 2: Low Position Feedback**

* ( K_p = 0 )
* ( K_v = 0.01 )

<img width="1920" height="752" alt="model b" src="https://github.com/user-attachments/assets/ec38f630-a283-49af-a820-b357d634c9e2" />

### **c. Case 3: Combined Position and Velocity Feedback**

* ( K_p = 1.3 )
* ( K_v = 0.01 )

<img width="1920" height="776" alt="model c" src="https://github.com/user-attachments/assets/a53220ed-b045-48ff-8b9e-2b50f42b21c9" />

Each configuration is evaluated using a unit step input representing a desired change in eyeball position.

---

## **5. Model Responses**

The system responses corresponding to the above configurations show distinct characteristics:

### **Case 1: ( K_p = 1, K_v = 0 )**

* The response exhibits noticeable oscillations.
* Peak amplitude: approximately 1.73
* Significant overshoot due to high position gain and no damping feedback.
* Rise time: ~0.0093 s
* Peak time: ~0.0262 s
* Transient time: ~0.32 s

<img width="1920" height="1025" alt="result model a " src="https://github.com/user-attachments/assets/0c0cd901-96e0-41e4-898c-b6f9a268c42a" />

### **Case 2: ( K_v = 0.01, K_p = 0 )**

* The system becomes slow and underdamped.
* Minimal oscillation but very slow convergence.
* Rise time: ~0.0138 s
* Peak time: ~0.0291 s
* Transient time: ~0.0436 s

<img width="1920" height="1028" alt="result model b" src="https://github.com/user-attachments/assets/089db8d7-5d05-4dad-9d66-edb6ef60e771" />

### **Case 3: ( K_v = 0.01, K_p = 1.3 )**

* Velocity feedback introduces damping and stabilizes the response.
* System settles faster compared to Case 2.
* Very small overshoot and improved steady‑state accuracy.

<img width="1920" height="1028" alt="result model c" src="https://github.com/user-attachments/assets/7599c2fa-6003-463d-b42c-f5863376f515" />

---

## **6. Inference**

The experimental results indicate:

* Increasing **position gain (Kₚ)** increases responsiveness but may induce oscillations if not accompanied by damping.
* Very low **Kₚ** leads to slow system response and poor tracking performance.
* Adding **velocity feedback (Kᵥ)** significantly improves damping, reduces oscillations, and enhances stability.

Thus, a combination of moderate position feedback and sufficient velocity feedback yields the most stable and efficient eyeball movement control.

---

## **7. Conclusion**

A Simulink model was successfully developed to analyze eyeball movement dynamics with varying position and velocity feedback coefficients. The study demonstrates how feedback gain tuning influences system stability, response time, and damping characteristics. This model provides a simplified yet effective representation of neuromuscular control in ocular motion.

---

