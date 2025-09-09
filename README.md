# 3D-Temperature-Visualization-inside-a-Box
This script fetches temperature data from Open-Meteo API for a given location and visualizes it as a 3D scatter plot inside a cube.


Got it 👍 Let’s go step by step in **English**, focusing on the math behind using **gradient (∇), divergence (∇·), and curl (∇×)** for 3D modeling (like temperature fields).

---

## 1) Scalar Field → Temperature

Temperature $T(x, y, z, t)$ is a **scalar field** — each point has a single value.

Inside a cube (0..1):

$$
T(x, y, z)
$$

---

## 2) Gradient (∇T)

Gradient measures the **rate and direction of change** of temperature:

$$
\nabla T = \left( 
\frac{\partial T}{\partial x}, 
\frac{\partial T}{\partial y}, 
\frac{\partial T}{\partial z} 
\right)
$$

👉 Meaning: tells you the direction in which temperature increases fastest.
In 3D visualization, gradient vectors show **heat flow direction**.

---

## 3) Divergence (∇·F)

If we define a **heat flux vector field**:

$$
\mathbf{F} = -k \nabla T
$$

($k$ = thermal conductivity)

Divergence is:

$$
\nabla \cdot \mathbf{F} = 
\frac{\partial F_x}{\partial x} + 
\frac{\partial F_y}{\partial y} + 
\frac{\partial F_z}{\partial z}
$$

👉 Meaning: how much heat is flowing **into or out of a small volume**.
It leads to the **heat equation**:

$$
\frac{\partial T}{\partial t} = \alpha \nabla^2 T
$$

---

## 4) Curl (∇×F)

Curl measures **rotation/whirlpool effect** of a vector field.

$$
\nabla \times \mathbf{F} =
\begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\
F_x & F_y & F_z
\end{vmatrix}
$$

👉 Meaning: if heat flow behaves like **circular motion** (important in convection currents).

---

## 5) Example Function

Let’s define a temperature field:

$$
T(x, y, z) = 20 + 5x + 3y^2 - 2z
$$

* Gradient:

$$
\nabla T = (5, 6y, -2)
$$

* Flux:

$$
\mathbf{F} = -k \nabla T = (-5k, -6ky, 2k)
$$

* Divergence:

$$
\nabla \cdot \mathbf{F} = -6k
$$

👉 Interpretation: constant heat loss everywhere.

---

## 6) Python Snippet (with Sympy)

```python
import sympy as sp

x, y, z, k = sp.symbols('x y z k')
T = 20 + 5*x + 3*y**2 - 2*z

# Gradient
grad_T = [sp.diff(T, var) for var in (x, y, z)]

# Flux (F = -k ∇T)
F = [-k*g for g in grad_T]

# Divergence
div_F = sum(sp.diff(F[i], var) for i,var in enumerate((x,y,z)))

print("Gradient:", grad_T)
print("Flux:", F)
print("Divergence:", div_F)
```

---

✅ **Summary**

* **Gradient (∇T):** slope of temperature field → fastest heating direction
* **Flux (F = -k∇T):** actual heat flow
* **Divergence (∇·F):** if heat is accumulating or escaping
* **Curl (∇×F):** rotational effects (like convection currents in fluids)

---

Do you want me to now **visualize this math in 3D** (temperature field + gradient vectors inside a cube) with Python?
