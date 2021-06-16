Take a look first at the README.md.
Here I explain the basic changes I made to run tensorflow lite micro on a
STM32F4-DISCOVERY board, with a STM32F407VGT6 and ST-Link V2.

## Setup


#### 1. Initialize the project template

``` console
$ cargo generate \
    --git https://github.com/knurling-rs/app-template \
    --branch main \
    --name tensorflowmicro
```

#### 2. Set `probe-run` chip

runner = "probe-run --chip STM32F407VGTx"

#### 3. Adjust the compilation target

target = "thumbv7em-none-eabihf" # Cortex-M4F (with FPU)

``` console
$ rustup target add thumbv7em-none-eabihf
```
#### 4. Add a HAL as a dependency
This seems to not be necessary to run the bin/tests:
stm32f4xx-hal = { version = "0.9.0", features = ["stm32f407"]}

#### 5. Import your HAL
This seems to not be necessary to run the bin/tests:
use stm32f4xx_hal as _;

#### (6. Get a linker script)

We have added a memory.x file, that has the following information:
```
MEMORY
{
  FLASH : ORIGIN = 0x08000000, LENGTH = 1024K
  RAM : ORIGIN = 0x20000000, LENGTH = 128K
}
```


#### 7. Run!
To run the examples:
$ cargo rb hello

To run the tests:
$ cargo test -p testsuite