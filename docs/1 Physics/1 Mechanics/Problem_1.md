# Problem 1

---

## **Investigating the Range as a Function of the Angle of Projection**

### **1. Theoretical Foundation**

Projectile motion describes the motion of an object launched into the air under the influence of gravity, assuming no air resistance. The path followed is a parabola.

Let’s consider an object projected with initial velocity \( v_0 \) at an angle \( \theta \) from the horizontal:

- Horizontal motion: \( x(t) = v_0 \cos(\theta) \cdot t \)
- Vertical motion: \( y(t) = v_0 \sin(\theta) \cdot t - \frac{1}{2} g t^2 \)

To find the **range** \( R \), we determine the total time of flight (when \( y(t) = 0 \)):

\[
t_{\text{flight}} = \frac{2 v_0 \sin(\theta)}{g}
\]

Substitute into horizontal motion:

\[
R = v_0 \cos(\theta) \cdot \frac{2 v_0 \sin(\theta)}{g} = \frac{v_0^2 \sin(2\theta)}{g}
\]

This shows that the range depends on:
- \( v_0 \): Initial speed
- \( \theta \): Projection angle
- \( g \): Gravitational acceleration

📌 **Important**: The range is maximum when \( \sin(2\theta) = 1 \) → \( \theta = 45^\circ \)

---

### **2. Analysis of the Range**

Let’s analyze how different variables affect the range:

- **Angle**: Range increases until \( 45^\circ \), then decreases.
- **Initial velocity \( v_0 \)**: Since \( R \propto v_0^2 \), doubling the speed quadruples the range.
- **Gravity \( g \)**: Higher gravity (like on Jupiter) shortens the range.

We can plot range vs angle for various \( v_0 \) values to visualize the relationships.

---

### **3. Practical Applications**

- **Sports**: Kicking or throwing a ball.
- **Engineering**: Launching objects from a catapult or cannon.
- **Astrophysics**: Spacecraft trajectories.
- **Military**: Ballistics and targeting systems.

In real life, additional factors like air drag, terrain height, or wind alter the results.

---

### **4. Implementation (Python Script)**

Below is a basic Python script using matplotlib and numpy:

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # gravitational acceleration (m/s^2)
v0_values = [10, 20, 30]  # initial velocities in m/s
angles = np.linspace(0, 90, 500)  # degrees

plt.figure(figsize=(10, 6))

for v0 in v0_values:
    theta_rad = np.radians(angles)
    R = (v0 ** 2) * np.sin(2 * theta_rad) / g
    plt.plot(angles, R, label=f'v0 = {v0} m/s')

plt.title('Range vs Angle of Projection')
plt.xlabel('Angle (degrees)')
plt.ylabel('Range (meters)')
plt.legend()
plt.grid(True)
plt.show()
```

---

### **5. Limitations and Improvements**

- Assumes no air resistance (idealized).
- Assumes flat terrain.
- Wind, spin, and shape of the projectile can significantly affect the real path.
- In real-world applications, numerical simulations or empirical data are needed.

---
