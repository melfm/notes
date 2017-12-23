# Linear Systems

A system of equations is a set or collection of equations that are dealt with at once.
Linear equations are simpler than non-linear equations. The simplest linear system is one with two equations and two variables.

## Standard Form Dynamics
State : Vector of system variables that entirely defines the system at a specific instance in time. No past history required (Markov property).
* Linear first order time-invariant dynamics in continuous time
	* Update equation : $\dot X(t) = Ax(t) + Bu(t)$
	* Measurement equation : $y(t) = Cx(t) + Du(t)$
* Linear first order time-invariant dynamics in discrete time
	* Update equation : $x_t = Ax_{t-1} + Bu_t$
	* Measurement equation : $y_t = Cx_t + Du_t$

## Linear Time Invariant Systems
- Transfer Function
	- Modesl output behaviours $z(t)$ for input $u(t)$
- State Space Modelling
	- Model detail variables (change over time) for the system

## Discrete Systems
A system with a countable number of states and therefore they may be described
in precise mathematical models.
