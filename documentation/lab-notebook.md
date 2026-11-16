# Lab notebook – PUTM CAN Logger
## 2026-11-13

utworzyłem arkusze hierarchiczne, etykiety hierarchiczne, can_tx, can_rx, can_l, can_h, 
pin s - silent, przy s - s nieaktywnym normalnie odbiera i wysyła, przy stanie aktywnym tylko słucha, logger ma nie nadawać ack na magistralę tylko być w trybie silent bo ramki błedu mogłyby popsuć odczyty. (podwójne zabezpieczenie tryb bus monitoring w FDCAN i pin S w transceiverze)

