# \# DzikiBoT-STM32-Nucle-L432KC

# 

# Projekt robota \*\*mini-sumo\*\* na płytce \*\*STM32 Nucleo-L432KC\*\*. Kod jest pisany z założeniem:

# \- `main.c` ma być maksymalnie chudy,

# \- cała obsługa peryferiów siedzi w osobnych plikach (`tf\_luna\_i2c.\*`, `tcs3472.\*`, `ssd1306.\*`, `motor\_bldc.\*`, `tank\_drive.\*`, `debug\_uart.\*`, `i2c\_scan.\*`),

# \- łatwo można przełączyć się między trybem \*\*diagnostycznym\*\* (OLED + UART) a późniejszym \*\*trybem walki\*\* (AI / logika minisumo).

# 

# \## Sprzęt / magistrale

# \- MCU: STM32 Nucleo-L432KC

# \- I²C prawa strona: I2C1 (PB6/PB7)

# \- I²C lewa strona: I2C3 (PC0/PC1)

# \- Czujniki dystansu: 2× TF-Luna (I²C, 0x10) – prawa/lewa

# \- Czujniki koloru: 2× TCS3472 (I²C, 0x29) – prawa/lewa

# \- OLED: SSD1306 (0x3C) na I2C1

# \- Napęd: 2× ESC na TIM1

# &nbsp; - TIM1 CH1 = PA8  → ESC prawy

# &nbsp; - TIM1 CH4 = PA11 → ESC lewy

# &nbsp; - start: `ESC\_ArmNeutral(3000)`

# 

# \## Moduły

# \- tf\_luna\_i2c.c/.h

# \- tcs3472.c/.h

# \- ssd1306.c/.h, oled\_panel.c/.h

# \- motor\_bldc.c/.h

# \- tank\_drive.c/.h

# \- debug\_uart.c/.h, i2c\_scan.c/.h, config.c/.h

# 

# \## Logika w `main.c`

# 1\. HAL\_Init() + zegary

# 2\. MX\_GPIO / USART2 / I2C1 / TIM1 / I2C3

# 3\. DebugUART\_Init() + I2C\_Scan\_All()

# 4\. Init TF-Luna (R/L), TCS3472 (R/L), OLED

# 5\. ESC\_Init() + ESC\_ArmNeutral(3000)

# 6\. Tank\_Init() + DriveTest\_Start()

# 7\. Pętla: Tank\_Update(), odczyty, OLED, UART

# 

# \## Temperatura TF-Luna

# Jeśli zawsze jest 25.0°C → to jest temperatura modułu albo trzymasz pierwszą ramkę.



