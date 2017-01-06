# Linear Systems

## Standard Form Dynamics
Def: State : Vector of system variables that entirely defines the system at a specific instance in time. No past history required (Markov property).

- Linear first order time-invariant dynamics in continuous time
	- Update equation : $\dot X(t) = Ax(t) + Bu(t)$
	- Measurement equation : $y(t) = Cx(t) + Du(t)$
- Linear first order time-invariant dynamics in discrete time
	- Update equation : $x_t = Ax_{t-1} + Bu_t$
	- Measurement equation : $y_t = Cx_t + Du_t$
