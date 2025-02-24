> [!CAUTION]
> THIS MODULE HAS NOT BEEN TESTED, SO I DO NOT RECOMMEND USING IT, IF YOU
> INSTALL IT YOU DO IT AT YOUR OWN RISK !!!!

# Azoteq Adapter
This module allows you to configure the drivers for your keyboard divided in the slave part.

Compatible with all boards with pro micro like the Nice!Nano, Puchi-Ble, clones and others.

Shields supported:
- azoteq_adapter_left
- azoteq_adapter_right

# Usage

- **Example for the left Shield:**
  ```bash
  west build -b nice_nano_v2 -- -DSHIELD="corne_left azoteq_adapter_left"
  ```

- **Example for the right Shield:**
  ```bash
  west build -b nice_nano_v2 -- -DSHIELD="corne_right azoteq_adapter_right"
  ```

# Configuration
Enable the drivers in the config file:

```conf
CONFIG_INPUT=y
CONFIG_INPUT_AZOTEQ_IQS5XX=y
# CONFIG_ZMK_INPUT_AZOTEQ_IQS5XX_IDLE_SLEEPER=y
# CONFIG_INPUT_AZOTEQ_IQS5XX_INIT_PRIORITY=60
```

To use this module, first add it to your `config/west.yml` by adding a new
entry to `remotes` and `projects`:

```yaml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/petejohanson
    - name: mctechnology17 # <-- enable the drivers and this module
      url-base: https://github.com/mctechnology17
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: azoteq-input-module # <-- enable the drivers
      remote: mctechnology17
      revision: main
    - name: zmk-azoteq-adapter # <-- enable this module
      remote: mctechnology17
      revision: main
  self:
    path: config
```

Now simply indicate in the board and the shield in the `build.yaml` file:

```yaml
---
include:
  - board: nice_nano_v2
    shield: corne_left azoteq_adapter_left
  - board: nice_nano_v2
    shield: corne_right azoteq_adapter_right
```

[//]: # ( vim: set fdm=marker: )
