# PUTM CAN Logger

Data logger for the PUT Motorsport car (Malta). It records every frame from two CAN buses (CAN_M and CAN_PT) with timestamps to a microSD card in BLF format.

## Core features (planned)
- STM32H563RI (LQFP64): 2 × FDCAN, SDMMC 4-bit, 640 KB SRAM
- 2 × isolated CAN FD transceiver ADM3057E, silent (listen-only) mode by default
- FDCAN in bus monitoring mode in the car, the logger never transmits on the bus
- microSD over SDMMC, BLF log files
- RTC with battery backup
- Power from the LV system (protection, 5 V to 3.3 V)

## Status
Schematic in progress (KiCad, PUT Motorsport template).
