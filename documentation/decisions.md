## 2026-11-13 – MCU: STM32H563RIT (LQFP64)

2x FDCAN, ram > ok 256KB / G0 ok 144KB, G4 128 KB,
będzie zapas gdy karta się zatnie plus miejsce na program

SDMMC - szybki zapis 4 bit zamiast SPI
LQFP 

pasuje H5 i H7, ale H7 bardziej skomplikowany, więcej zasilań, większy pobór, trudniejsza obsługa pamięci

U3 - 1 FDCAN - nie pasuje 

## 2026-11-20 – MCU: macierz decyzyjna

### Progi

| Wymaganie | Skąd | Próg zwykły CAN | Próg CAN FD na obu |
| --- | --- | --- | --- |
| Ruch na obu magistralach | CAN_PT: DBC soft-v2.0 12 × 200 Hz = 2400/s; bag 08.11 (setpointy 486 Hz) = 3550/s. CAN_M: bag, 8 z 31 kom.  ≈750/s (dolna granica) 3550 + 750 = 4300 ramek/s | 4300r/s | 4300r/s |
| Szybkość zapisu na kartę | 4300 ramek na sekundę x 48 B (python-can, can/io/blf.py) ( jedna ramka w zapisie blf , klasyczny CAN bez kompresji) = 206 400 B/s ≈ 0,21 MB/s. Zapas 0,21M/s x 3 bo dojdzie CAN FD, wynik bez 23 komunikatów CAN_M | 0,6MB/s | 4300 x 116 B = 0,50MB/s, zapas x2 = 1,0MB/s |
| Bufor w RAM | Producent dupuszcza do 250 ms na zapis bloku (SanDisk microSDHC Product Manual) Ramki dalej przychodzą i czekają w RAM, (surowe ramki) . 24Bx 4300 x 0,25s ≈ 26KB, 24B  = czas 8B + ID 4 + DLC 4 + dane 8B, zapas x 2 - 26KB x 2 = 52KB.  Przy SDXC (500ms)  4300 x 24 B x 0,5s = 52 KB, z zapasem x2 = 104KB .    | 52KB | 80 B (czas 8 + ID 4 + DLC 4 + dane 64) x 4300 x 0,25s = 86KB, zapas x2 = 172KB |
| Kontrolery CAN | 2 magistrale CAN_M , CAN_PT  z osobnym bitrate i CAN FD od tego roku | 2 x FDCAN | 2 x FDCAN |
| Obudowa | Lutowanie ręczne: LQFP | LQFP | LQFP |

### Kto przechodzi progi

| MCU | FDCAN | Karta SD | RAM | Obudowa | Przechodzi: zwykły CAN? | Przechodzi: CAN FD na obu? | W płytkach zespołu |
| --- | --- | --- | --- | --- | --- | --- | --- |
| STM32G484RE | 3 | SPI (brak SDMMC) | 128 KB (96 KB SRAM + 32 KB CCM) | LQFP64 | TAK | NIE  | FRONTBOX dev-hard-v2.1, DV_ASMC dev-hard-v1.0.0, BMS_LV hard-v2.0.1 |
| STM32G0B1RE | 2 | SPI (brak SDMMC) | 144 KB | LQFP64 | TAK | NIE | brak; G0C1KCT (ta sama seria G0) w TIRE_TEMP dev-hard-v3.0 i TIRE_PRESSURE_INTERFACE |
| STM32H563RI | 2 | SDMMC1 | 640 KB | LQFP64 | TAK | NIE | brak; H573RIT (ta sama seria H5) w AMS_MASTER od v3.1 |
| STM32H723VG | 3 | SDMMC1, SDMMC2 | 564 KB | LQFP100 | TAK | TAK | nie ma |
| STM32U385RG | 1 | SDMMC1 | 256 KB | LQFP64 | NIE | TAK | nie ma |
| STM32U3B5RG | 2 | SDMMC1 | 640 KB | LQFP64 | TAK | TAK | nie ma |

### Decyzja

MCU:
