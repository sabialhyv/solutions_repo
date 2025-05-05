# Problem 3

# Trajectories of a Freely Released Payload Near Earth

---

## Motivation

When a payload is released from a moving rocket near Earth, its subsequent **trajectory** is determined by its **initial velocity**, **altitude**, and **direction**. This problem is a compelling application of **orbital mechanics**, offering insights into various outcomes like:

- Stable orbits (elliptical or circular)
- Reentry trajectories
- Escape trajectories (parabolic or hyperbolic)

Understanding these motions is crucial for real-world missions like **satellite deployment**, **space probes**, and **reentry planning**.

---

## Theoretical Background

### Newton's Law of Universal Gravitation

$$
F = \frac{G M m}{r^2}
$$

Where:

- \( F \) is the gravitational force,
- \( G = 6.674 \times 10^{-11} \, \text{Nm}^2/\text{kg}^2 \),
- \( M \) is Earth’s mass,
- \( m \) is the payload’s mass,
- \( r \) is the distance from Earth's center.

---

### Orbital Trajectory Classification

The shape of the trajectory depends on **total mechanical energy**:

$$
E = \frac{1}{2}mv^2 - \frac{GMm}{r}
$$


| Trajectory Type | Total Energy \(E\) | Eccentricity \(e\) |
|-----------------|--------------------|---------------------|
| Circular Orbit  | \(< 0\)            | 0                   |
| Elliptical Orbit| \(< 0\)            | \(0 < e < 1\)       |
| Parabolic       | \(= 0\)            | 1                   |
| Hyperbolic      | \(> 0\)            | \(e > 1\)           |

---

## Simulation Setup

We assume:

- 2D motion in a plane
- Central gravitational force from Earth
- No air resistance (vacuum)

We'll simulate the trajectory of a payload launched from **Earth’s low orbit** with different initial velocities.

---

## Constants and Parameters

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11       # gravitational constant [m^3 kg^-1 s^-2]
M = 5.972e24          # mass of Earth [kg]
R_earth = 6.371e6     # radius of Earth [m]

# Initial conditions
altitude = 400e3  # 400 km altitude (e.g., ISS orbit)
r0 = np.array([R_earth + altitude, 0])  # initial position
```

---

##  Numerical Simulation: Velocity Variants

```python
# Function for gravitational acceleration
def gravity(pos):
    r = np.linalg.norm(pos)
    return -G * M * pos / r**3

# Time step and simulation time
dt = 1  # seconds
t_max = 6000  # simulate for ~1.5 hours
steps = int(t_max / dt)

# Try multiple velocities
velocities = {
    "Sub-orbital (< v1)": 7000,
    "Circular orbit (v1)": np.sqrt(G * M / np.linalg.norm(r0)),
    "Elliptical (> v1)": 8500,
    "Escape velocity (v2)": np.sqrt(2 * G * M / np.linalg.norm(r0)),
    "Hyperbolic (> v2)": 12000
}
```

---

## Trajectory Simulation Function

```python
def simulate_trajectory(v0):
    pos = r0.copy()
    vel = np.array([0, v0])
    traj = [pos.copy()]
    
    for _ in range(steps):
        acc = gravity(pos)
        vel += acc * dt
        pos += vel * dt
        traj.append(pos.copy())
        if np.linalg.norm(pos) < R_earth:
            break  # impact with Earth
    return np.array(traj)
```

---

## Plotting All Trajectories

```python
plt.figure(figsize=(8, 8))
theta = np.linspace(0, 2*np.pi, 500)
earth_x = R_earth * np.cos(theta)
earth_y = R_earth * np.sin(theta)
plt.plot(earth_x, earth_y, color='blue', label='Earth')

for label, v0 in velocities.items():
    traj = simulate_trajectory(v0)
    plt.plot(traj[:,0], traj[:,1], label=label)

plt.axis('equal')
plt.xlabel('X position (m)')
plt.ylabel('Y position (m)')
plt.title('Trajectories of Released Payloads at 400 km Altitude')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```

---

## Interpretation of Results

- **Sub-orbital (v < v1)**: Object falls back to Earth (reentry).
- **Circular orbit (v = v1)**: Stable orbit, e.g., ISS.
- **Elliptical orbit (v1 < v < v2)**: Payload stays in orbit but with varying altitude.
- **Escape velocity (v = v2)**: Object just escapes Earth’s gravity.
- **Hyperbolic (v > v2)**: Object enters interplanetary space.

---

## Real-World Applications

| Trajectory Type | Mission Example |
|-----------------|-----------------|
| Sub-orbital     | Space tourism, sounding rockets |
| Circular Orbit  | ISS, GPS, Earth Observation |
| Elliptical Orbit| Transfer orbits, Molniya satellites |
| Escape Trajectory| Moon missions, interplanetary probes (Voyager, Mars rovers) |
| Hyperbolic Path | Gravity assist maneuvers, escape trajectories |

---

## Conclusion

By changing the **initial velocity** of a payload released from a moving spacecraft, we can achieve a wide range of **orbital trajectories** — from short-lived suborbital hops to interplanetary escapes. Understanding these dynamics is vital for mission design, space navigation, and satellite deployment.

The combination of **gravitational physics** and **numerical simulation** allows us to visualize and predict these complex motions in space.

