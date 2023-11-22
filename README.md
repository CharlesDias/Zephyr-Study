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

1. Create a project folder

```shell
mkdir STM32H7-Project
```

2. And create a new virtual environment

```shell
python3 -m venv STM32H7-Project/.venv
```

3. Activate the virtual environment

```shell
source STM32H7-Project/.venv/bin/activate
```

4. Install west

```shell
pip install west
```

5. Access the project folder

```shell
cd STM32H7-Project
```

6. And initialize the Workspace for the project example application.

```shell
west init -m https://github.com/CharlesDias/Zephyr-on-STM32H7 --mr main Workspace
```

7. Update the Zephyr modules

```shell
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

### Building and running

To build the application, run the following command:

```shell
west build -b $BOARD app
```

where `$BOARD` is the target board.

You can use the `custom_stm32h7b0` board found in this repository.
Note that Zephyr sample boards may be used if an appropriate overlay is provided (see `app/boards`).

A sample debug configuration is also provided. To apply it, run the following command:

```shell
west build -b $BOARD app -- -DOVERLAY_CONFIG=debug.conf
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
