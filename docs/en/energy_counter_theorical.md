# Energy Counter Theorical

**Energy Counter Theorical** is designed to calculate the amount energy diverted to the load. *This is an optional package.*

The amount of energy diverted is calculated based on the load power (in `W`) and the level of energy diverted every seconds.

!!! warning "Energy saved reported by this counter is for information only"
    Remember that values are calculated and not measured.  
    The values presented by this sensor are only estimations of energy diverted based on the configuration you made in Home Assistant.

To use this counter, add the following lines to your configuration file.

```yaml
packages:
  counter:
    url: https://github.com/XavierBerger/Solar-Router-for-ESPHome/
    file: solar_router/energy_counter_theorical.yaml
```
Then you have to define the **load power** in Home Assistant `Control` interface. The power entered has to reflect the power of the element plugged on solar router.

![alt text](images/SolarRouterEnergyCounterTheoricalConfiguration.png)

The instantaneous and cumulated energy diverted are available in `sensors` interface:

![alt text](images/SolarRouterEnergyCounterTheoricalSensors.png)