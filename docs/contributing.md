# Contributing to development

**Solar Router for [ESPHome](http://esphome.io)** is design to be modular to make easy the customisation to various power meters and various regulators.  
You want to contribute? You are welcome and you will find bellow some recommendation to do so.

## Setup development environement

To contribute to **Solar-Router-for-ESPHome** and develop a new feature on your computer and propose a *merge request*, you should:

- [Create and activate a Python virtual environment](https://docs.python.org/3/library/venv.html)
- Install ESPHome CLI:`pip install esphome` 
- Fork [the repository](https://github.com/XavierBerger/Solar-Router-for-ESPHome) on Github
- Clone the repository on your PC
- Create a branch starting from **main**
- Install and test your code on you device : `esphome run my_configuration/yaml`
- Update the code and push update on your repository
- Propose a pull request from your fork to the official repository

## Developing a **Hardware**

You can propose any hardware based on your needs. If this new hardware require to use GPIO, the pins used by your hardware have to be configuration into `subsitution` section.

A documentation have be added describing this new hardware and its constraints (Ex: GPIO capabilities). See [update documentation](#update-documentation) chapter bellow.

## Developping a **Power Meter**

A **Power Meter** is a component designed to provide and periodically update a sensor named `real_power`.

```yaml linenums="1"
sensor:
  # Sensor showing the actual power consumption
  - id: real_power
    platform: template
    name: "Real Power"
    device_class: "power"
    unit_of_measurement: "W"
    update_interval: 1s
```

!!! tip "Tip: See already developped power meter for examples"

This sensor is used by the **Solar Router Engine** to get the value of power exchanged with the grid.

If this new power meter needs specific configuration, required parameters have to be added into `substitution` section.

A documentation have to be added describing the power meter and how to configure it. See [update documentation](#update-documentation) chapter bellow.

## Developping a **Regulator**

A **Regulator** has to manage the energy sent to the load based on the `regulator_opening` sensor state. `regulator_opening` state can vary from 0 (where no energy is sent to the load) to 100 (where all the energy possible is sent to the load).

The following code represent and example (extracted from [regulator_triac.yaml](https://github.com/XavierBerger/Solar-Router-for-ESPHome/blob/main/solar_router/regulator_triac.yaml)) of usage based on `light` component using `brightness` to control the energy diverted:

```yaml linenums="1"
script:
  # Apply regulation on triac using light component
  - id: regulation_control
    mode: single
    then:
      # Apply opening level on triac using light component
      - light.turn_on:
          id: dimmer_controller
          brightness: !lambda return id(regulator_opening).state/100.0;
```

!!! tip "Tip: See already developped regulators for examples"

If this new power meter needs specific configuration, required parameters have to be added into `substitution` section.

A documentation have to be added describing the power meter and how to configure it. See [update documentation](#update-documentation) chapter bellow.

## Update **Documentation**

Documentation is written using [mkdocs](https://www.mkdocs.org/) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

To install `mkdocs`, you need to install [Python](https://python.org) and then :

- Create a virtual environment (see [Python documentation](https://docs.python.org/3/library/venv.html)).
- Install the required module with the following command `pip install -r requirements.txt`.

Documentation is stored in `docs` directory. To see you modification in real time in your browser, execute the command `mkdocs serve` and browse [http://127.0.0.1:8000](http://127.0.0.1:8000)

{% include "changelog.md"%}