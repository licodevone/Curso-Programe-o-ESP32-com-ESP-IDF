# Instalação do ESP-IDF no WSL do Windows com UBUNTU

## Passos da instalação e configuração

> Seguir a documentação do git da Espressif

-https://github.com/espressif/vscode-esp-idf-extension/blob/master/docs/tutorial/wsl.md#usbipd_instructions

> Abrir o PowerShell do Windows como administrador

![alt text](image-16.png)

> Instalar o WSL

```
wsl --install
```

```
wsl -l -v
```

> Seguir a documentação de instalação do ESP-IDF da Espressif

- https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html

### <mark>OBSERVAÇÂO IMPORTANTE:</mark> 

<hr>

`Verificar se já existe algum compartilhamento da USB anterior, caso coloque a placa verá se existe ou não esse compartilhamento.`

![alt text](image-18.png)

- No PowerShell no Windows

![alt text](image-17.png)

`Caso exista digitar o comando para desatachar conforme imagem anterior`

```
usbipd unbind -a
```

`Caso receba o Warning  utilize o force como sugerido e mostrado na imagem e comando abaixo`

![alt text](image-19.png)

```
usbipd bind --busid 6-1 -f
```
> No Ubuntu verificar se a porta esta compartilhada

![alt text](image-44.png)

<hr>

> instalar a extensão `Remote development`

![alt text](image-20.png)

Abrir uma janela e clicar no link azul no final da janela do lado esquerdo `Open a Remote Window`

![alt text](image-21.png)

Caso tenha mais de uma instância do Linux instalada clico em `Connect to WSL using Distro`

![alt text](image-22.png)

Como tenho apenas uma clico em `Connect to WSL`  com isso o VSCOde irá preparar todo o cenário para trabalharmos com o Ubuntu no WSL do Windows

![alt text](image-23.png)

Clicando em Open folder conseigo ver que já se encontra no diretório do Ubuntu do WSL

![alt text](image-24.png)

> Instalar a extensão da Espressif no ambiente Ubuntu, caso tenha no Windows ele esta apenas na máquina Host

![alt text](image-25.png)

> Digitar F1 ou Crtl + Shift + p e escolher a opção ESP-IDF: Configure `ESP-IDF EXTENSION`

![alt text](image-26.png)

> Irá abrir a janela para escolher a pasta de configuração do WSL

![alt text](image-27.png)

> Escolher a versão Express

![alt text](image-28.png)

Escolher `Find ESP-IDF in your system`

- Escolher o diretório do Path da instalação do ESP-IDF da Espressif

![alt text](image-29.png)

![alt text](image-30.png)

> Escolher o diretório do Toolchain `.espressif`

![alt text](image-31.png)

> Clicar em `Install` para encontrar a instalação existente

![alt text](image-32.png)

![alt text](image-33.png)

> Ambiente configurado

![alt text](image-34.png)

> Clicar em `New Project` e mudar os dados de criação de um novo projeto

![alt text](image-35.png)

> Mudar o nome do projeto, diretório, placa e Target`Alvo` escolher a placa e a porta serial

![alt text](image-37.png)

![alt text](image-36.png)

> Clicar em `Choose template`

![alt text](image-38.png)

> Escolher o local do template

![alt text](image-39.png)

> escolhido o projeto Blink

![alt text](image-40.png)

> Clicar em `Create project ...`

![alt text](image-41.png)

> Projeto criado

![alt text](image-42.png)

```c
#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"

// Função principal do programa
void app_main(void)
{
    // Configuração do pino GPIO para o LED (número do pino pode variar)
    gpio_set_direction(GPIO_NUM_2, GPIO_MODE_OUTPUT);
    
    printf("Hello World! \n");  // Mensagem de inicialização

    while (1)                                  // Loop infinito
    {
        gpio_set_level(GPIO_NUM_2, 1);         // Liga o LED
        vTaskDelay(1000 / portTICK_PERIOD_MS); // Aguarda 1 segundo
        printf("LED - ON \n");                 // Mensagem de LED ligado

        gpio_set_level(GPIO_NUM_2, 0);         // Desliga o LED
        vTaskDelay(1000 / portTICK_PERIOD_MS); // Aguarda 1 segundo
        printf("LED - OFF \n");                // Mensagem de LED desligado
    }
}
```

![alt text](image-43.png)

> Agora Compilar e flechar o processador

![alt text](image-45.png)


### <mark>OBSERVAÇÂO IMPORTANTE:</mark> 

`Verificar a usb selecionada com o drive corretamente` e selecionar o método de envio `UART`

<hr>

![alt text](image-46.png)

<hr>

```
licodev@lesp:~/esp/teste-wsl$ export IDF_PATH='/home/licodev/esp/esp-idf'
'/home/licodev/.espressif/python_env/idf5.4_py3.10_env/bin/python' '/home/licodev/esp/esp-idf/tools/licodev@lesp:~/esp/teste-wsl$ '/home/licodev/.espressif/python_env/idf5.4_py3.10_env/bin/python' '/home/licodev/esp/esp-idf/tools/idf_monitor.py' -p /dev/ttyUSB0 -b 115200 --toolchain-prefix xtensa-esp32-elf- --target esp32 '/home/licodev/esp/teste-wsl/build/teste-wsl.elf'
--- esp-idf-monitor 1.4.0 on /dev/ttyUSB0 115200 ---
--- Quit: Ctrl+] | Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H ---
ets Jun  8 2016 00:22:57

rst:0x1 (POWERON_RESET),boot:0x13 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:7176
load:0x40078000,len:15564
ho 0 tail 12 room 4
load:0x40080400,len:4
0x40080400: _init at ??:?

load:0x40080404,len:3904
entry 0x40080640
I (31) boot: ESP-IDF v5.4-dev-1873-g41dd1a351b 2nd stage bootloader
I (31) boot: compile time Aug  5 2024 00:14:37
I (33) boot: Multicore bootloader
I (37) boot: chip revision: v1.0
I (41) boot.esp32: SPI Speed      : 40MHz
I (46) boot.esp32: SPI Mode       : DIO
I (50) boot.esp32: SPI Flash Size : 2MB
I (55) boot: Enabling RNG early entropy source...
I (60) boot: Partition Table:
I (64) boot: ## Label            Usage          Type ST Offset   Length
I (71) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (78) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (86) boot:  2 factory          factory app      00 00 00010000 00100000
I (93) boot: End of partition table
I (98) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=09450h ( 37968) map
I (119) esp_image: segment 1: paddr=00019478 vaddr=3ffb0000 size=0231ch (  8988) load
I (123) esp_image: segment 2: paddr=0001b79c vaddr=40080000 size=0487ch ( 18556) load
I (132) esp_image: segment 3: paddr=00020020 vaddr=400d0020 size=13948h ( 80200) map
I (161) esp_image: segment 4: paddr=00033970 vaddr=4008487c size=081d4h ( 33236) load
I (181) boot: Loaded app from partition at offset 0x10000
I (181) boot: Disabling RNG early entropy source...
I (193) cpu_start: Multicore app
I (201) cpu_start: Pro cpu start user code
I (202) cpu_start: cpu freq: 160000000 Hz
I (202) app_init: Application information:
I (204) app_init: Project name:     teste-wsl
I (210) app_init: App version:      1
I (214) app_init: Compile time:     Aug  5 2024 00:14:19
I (220) app_init: ELF file SHA256:  5fd8790ae...
I (225) app_init: ESP-IDF:          v5.4-dev-1873-g41dd1a351b
I (232) efuse_init: Min chip rev:     v0.0
I (236) efuse_init: Max chip rev:     v3.99 
I (241) efuse_init: Chip rev:         v1.0
I (246) heap_init: Initializing. RAM available for dynamic allocation:
I (253) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (259) heap_init: At 3FFB2BE8 len 0002D418 (181 KiB): DRAM
I (266) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (272) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (278) heap_init: At 4008CA50 len 000135B0 (77 KiB): IRAM
I (286) spi_flash: detected chip: generic
I (289) spi_flash: flash io: dio
W (293) spi_flash: Detected size(4096k) larger than the size in the binary image header(2048k). Using the size in the binary image header.
I (307) main_task: Started on CPU0
I (317) main_task: Calling app_main()
Hello WoldI (317) main_task: Returned from app_main()
```
> Projeto Blink com o WSL

```
licodev@lesp:~/esp/wsl-blink$ export IDF_PATH='/home/licodev/esp/esp-idf'
'/home/licodev/.espressif/python_env/idf5.4_py3.10_env/bin/python' '/home/licodev/esp/esp-idf/tools/licodev@lesp:~/esp/wsl-blink$ '/home/licodev/.espressif/python_env/idf5.4_py3.10_env/bin/python' '/home/licodev/esp/esp-idf/tools/idf_monitor.py' -p /dev/ttyUSB0 -b 115200 --toolchain-prefix xtensa-esp32-elf- --target esp32 '/home/licodev/esp/wsl-blink/build/wsl-blink.elf'
--- esp-idf-monitor 1.4.0 on /dev/ttyUSB0 115200 ---
--- Quit: Ctrl+] | Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H ---
ets Jun  8 2016 00:22:57

rst:0x1 (POWERON_RESET),boot:0x13 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:7176
load:0x40078000,len:15564
ho 0 tail 12 room 4
load:0x40080400,len:4
0x40080400: _init at ??:?

load:0x40080404,len:3904
entry 0x40080640
I (31) boot: ESP-IDF v5.4-dev-1873-g41dd1a351b 2nd stage bootloader
I (31) boot: compile time Aug  5 2024 00:24:35
I (33) boot: Multicore bootloader
I (37) boot: chip revision: v1.0
I (41) boot.esp32: SPI Speed      : 40MHz
I (46) boot.esp32: SPI Mode       : DIO
I (50) boot.esp32: SPI Flash Size : 2MB
I (55) boot: Enabling RNG early entropy source...
I (60) boot: Partition Table:
I (64) boot: ## Label            Usage          Type ST Offset   Length
I (71) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (78) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (86) boot:  2 factory          factory app      00 00 00010000 00100000
I (93) boot: End of partition table
I (97) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=096a0h ( 38560) map
I (119) esp_image: segment 1: paddr=000196c8 vaddr=3ffb0000 size=02364h (  9060) load
I (123) esp_image: segment 2: paddr=0001ba34 vaddr=40080000 size=045e4h ( 17892) load
I (132) esp_image: segment 3: paddr=00020020 vaddr=400d0020 size=13ff0h ( 81904) map
I (162) esp_image: segment 4: paddr=00034018 vaddr=400845e4 size=0846ch ( 33900) load
I (181) boot: Loaded app from partition at offset 0x10000
I (182) boot: Disabling RNG early entropy source...
I (194) cpu_start: Multicore app
I (202) cpu_start: Pro cpu start user code
I (202) cpu_start: cpu freq: 160000000 Hz
I (202) app_init: Application information:
I (205) app_init: Project name:     wsl-blink
I (210) app_init: App version:      1
I (215) app_init: Compile time:     Aug  5 2024 00:24:19
I (221) app_init: ELF file SHA256:  728a14c1e...
I (226) app_init: ESP-IDF:          v5.4-dev-1873-g41dd1a351b
I (232) efuse_init: Min chip rev:     v0.0
I (237) efuse_init: Max chip rev:     v3.99 
I (242) efuse_init: Chip rev:         v1.0
I (247) heap_init: Initializing. RAM available for dynamic allocation:
I (254) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (260) heap_init: At 3FFB2C30 len 0002D3D0 (180 KiB): DRAM
I (266) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (273) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (279) heap_init: At 4008CA50 len 000135B0 (77 KiB): IRAM
I (287) spi_flash: detected chip: generic
I (290) spi_flash: flash io: dio
W (294) spi_flash: Detected size(4096k) larger than the size in the binary image header(2048k). Using the size in the binary image header.
I (308) main_task: Started on CPU0
I (318) main_task: Calling app_main()
Hello World! 
LED - ON 
LED - OFF 
LED - ON 
LED - OFF 
LED - ON 
LED - OFF 
LED - ON 
LED - OFF 
LED - ON 
LED - OFF 
LED - ON 
LED - OFF 
```

![alt text](image-47.png)