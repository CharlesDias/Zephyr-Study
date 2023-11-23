[![Build](https://github.com/CharlesDias/Zephyr-Study/actions/workflows/build.yml/badge.svg)](https://github.com/CharlesDias/Zephyr-Study/actions/workflows/build.yml)

# Zephyr RTOS Study

**Note:** This repository is based on the [zephyrproject-rtos/example-application](https://github.com/zephyrproject-rtos/example-application) template.

This repository contains some Zephyr example applications validated on the following boards:

- Nordic [nRF52840-DK][nrf52840_dk]
- STMicroelectronics [NUCLEO-H743ZI][nucleo_h743zi]
- STMicroelectronics [STM32H7B3I-DK][stm32h7b3i_dk]
- FANKE FK7B0M1-VBT6 V1.0, named here as custom_stm32h7b0

[nrf52840_dk]: https://www.nordicsemi.com/Products/Development-hardware/nrf52840-dk
[nucleo_h743zi]: https://www.st.com/en/evaluation-tools/nucleo-h743zi.html
[stm32h7b3i_dk]: https://www.st.com/en/evaluation-tools/stm32h7b3i-dk.html

## Getting Started

### Setup the development environment

If you haven't set up the Zephyr development environment on your machine, go to the 
official [Zephyr Getting Started Guide](https://docs.zephyrproject.org/latest/getting_started/index.html) 
and follow the instructions. However, if you already have, you can create a new virtual environment dedicated 
to this project. In this way, you can use different Zephyr versions for different projects.

The following steps initialize the workspace and clone all Zephyr modules. This needs to be done just one.

1. Create a project folder and access it.

```shell
mkdir Zephyr-Workspace
cd Zephyr-Workspace
```

2. And create a new virtual environment inside `Zephyr-Workspace` folder.

```shell
python3 -m venv .venv
```

3. And activate the virtual environment.

```shell
source .venv/bin/activate
```

4. Install west

```shell
pip install west
```

5. And initialize the Workspace for the project example application.

```shell
west init -m https://github.com/CharlesDias/Zephyr-on-STM32H7 --mr main Workspace
```

6. Access the `Workspace` folder and clone the Zephyr modules

```shell
cd Workspace
west update
```

8. Export a Zephyr CMake package. 

```shell
west zephyr-export
```

9. Install the Python dependencies.

```shell
pip install -r ~/zephyrproject/zephyr/scripts/requirements.txt
```

**ATTENTION: Remember to activate the virtual environment every time that you initiate a new shell console.**

### Building and running

Access the `Zephyr-Study` folder.

```shell
cd Zephyr-Study
```

To build the application, run the following command:

```shell
west build -b $BOARD samples/app
```

where `$BOARD` is the target board.

You can use the `custom_stm32h7b0` board found in this repository.
Note that Zephyr sample boards may be used if an appropriate overlay is provided (see `app/boards`).

A sample debug configuration is also provided. To apply it, run the following command:

```shell
west build -b $BOARD samples/app -- -DOVERLAY_CONFIG=debug.conf
```

Once you have built the application, run the following command to flash it:

```shell
west flash
```

### Testing

To execute Twister integration tests, run the following command:

```shell
west twister -T tests --integration
```

## Kconfig interfaces

Access the complete information on [Interactive Kconfig interfaces](https://docs.zephyrproject.org/latest/build/kconfig/menuconfig.html#interactive-kconfig-interfaces) Zephyr's webpage.

There are two interactive configuration interfaces available for exploring the available Kconfig options and making temporary changes: `menuconfig` and `guiconfig`.

### Run the configuration interfaces

1. Build your application as usual using either `west`:

```shell
west build -b $BOARD samples/app
```

   .. zephyr-app-commands::
      :tool: all
      :cd-into:
      :board: <board>
      :goals: build
      :compact:

2. To run the terminal-based `menuconfig` interface, use this command:

```shell
west build -t menuconfig
```

3. To run the graphical `guiconfig`, use this command:

```shell
west build -t guiconfig
```

**ATTENTION:** 

The configuration file used during the build is always `build/zephyr/.config`. If you have another saved configuration that you want to build with, copy it to `build/zephyr/.config`. Make sure to back up your original configuration file.