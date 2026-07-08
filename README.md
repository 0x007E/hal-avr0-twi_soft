[![Version: 1.0 Release](https://img.shields.io/badge/Version-1.0%20Release-green.svg)](https://github.com/0x007e/hal-avr0-twi_soft) ![Release](https://github.com/0x007e/hal-avr0-twi_soft/actions/workflows/release.yml/badge.svg) [![License GPLv3](https://img.shields.io/badge/License-GPLv3-lightgrey)](https://www.gnu.org/licenses/gpl-3.0.html)

# `hal-avr0-twi_soft` - AVR0 Software TWI Hardware Abstraction

The `hal-avr0-twi_soft` is a lightweight `software-twi` hardware abstraction library for `AVR0` microcontrollers. It provides a clean interface for `software-twi` initialization and communication while hiding direct register-level interaction from higher software layers. The library is intended for projects that want to separate low-level device startup code from application logic and establish a small, reusable system layer for AVR0 targets.

## Features

- `Software-TWI` master configuration for AVR0 devices.
- `Software-TWI` master communication for AVR0 devices.
- Encapsulation of low-level register access.
- Compact and reusable API for embedded projects.
- Foundation for layered HAL architectures.

> The `hal-avr0-twi_soft` library reduces coupling by providing a focused interface for essential `software-twi` system services. This improves portability inside a project, keeps startup code organized, and makes higher-level modules easier to maintain.

## File Structure

![File Structure](https://blog.sunriax.at/hal-avr0-twi_soft/twi__soft_8c__incl.png)

```
hal/
├── common/
|   ├── defines/
|   |   └── TWI_defines.h
|   └── enums/
|       └── TWI_enums.h
└── avr0/
    └── twi/
        ├── twi_soft.c
        └── twi_soft.h
```

## Downloads

The library can be downloaded (`zip` or `tar`), cloned or used as submodule in a project.

| Type      | File               | Description              |
|:---------:|:------------------:|:-------------------------|
| Library   | [zip](https://github.com/0x007E/hal-avr0-twi_soft/releases/latest/download/library.zip) / [tar](https://github.com/0x007E/hal-avr0-twi_soft/releases/latest/download/library.tar.gz) | AVR0 system library |

### Using with `git clone`

```sh
mkdir -p ./hal/
git clone https://github.com/0x007E/hal-common.git ./hal
mv ./hal/hal-common ./hal/common

mkdir -p ./hal/avr0
git clone https://github.com/0x007E/hal-avr0-twi_soft.git ./hal/avr0
mv ./hal/avr0/hal-avr0-twi_soft ./hal/avr0/twi
```

### Using as `git submodule`

```sh
git submodule add https://github.com/0x007E/hal-common.git        ./hal/common
git submodule add https://github.com/0x007E/hal-avr0-twi_soft.git ./hal/avr0/twi
```

## Programming

Additional parameters like twi clock speed, used pins and many more can be setup in the [header file](./twi_soft.h). A user friendly description can be found [here](https://0x007e.github.io/hal-avr0-twi_soft/twi__soft_8h.html).

```c
#include "../hal/avr0/twi/twi_soft.h"

int main(void)
{
	twi_soft_init();

    while (1)
    {
        TWI_Error error = TWI_None;

        // TWI-WRITE command
        twi_soft_start();
	
        error |= twi_soft_address(high_byte, TWI_Write);
        error |= twi_soft_set(middle_byte);
        error |= twi_soft_set(low_byte);

        twi_soft_stop();

        // TWI-READ command
        twi_soft_start();
	
        error |= twi_soft_address(high_byte, TWI_Read);
        error |= twi_soft_get(data, TWI_ACK);
        error |= twi_soft_get(data, TWI_NACK);

        twi_soft_stop();
    }
}
```

## Additional Information

| Type       | Link               | Description              |
|:----------:|:------------------:|:-------------------------|
| AVR0-Series | [pdf](https://ww1.microchip.com/downloads/en/DeviceDoc/megaAVR0-series-Family-Data-Sheet-DS40002015B.pdf) | megaAVR® 0-series family datasheet |

---

R. GAECHTER