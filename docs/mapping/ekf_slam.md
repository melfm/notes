# EKF SLAM


### Map Types
- Location based
- Feature based

## Localization
- Given :
    - Control inputs and motion model
    - Sensor measurements and measurement model relative to the environment
    - Environment model
- Find : Vehicle position

### Problems:
- Initial conditions :
    - Local : Tracking position through motions with inputs and measurements
    - Global : Unknown initial position
    - Kidnapped: Incorrect initial position

### Assumptions
- Known static environment
- Passive Estimation : Control law does not seek to minimize estimation error
- Single vehicle

