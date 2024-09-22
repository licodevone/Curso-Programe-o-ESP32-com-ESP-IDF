# Instalação passo a passo do ESP-IDF no Ubuntu

## Documentação

https://docs.espressif.com/projects/esp-idf/en/v5.1.4/esp32/get-started/linux-macos-setup.html

https://github.com/espressif/vscode-esp-idf-extension/blob/master/docs/tutorial/wsl.md#usbipd_instructions

## Instalação e pré-requisitos

### Instalação do WSL

![alt text](image-23.png)

### Escolher Versão Linux acima das versões 20 nesse caso foi a 22.04

![alt text](image-5.png)

![alt text](image-4.png)

### Ferramenta USBIPD para realizar o Bind

```
Winget install usbipd
```
![alt text](image-6.png)

### Instalação dos pacotes de ferramentas de pre-requisito no Linux 

https://docs.espressif.com/projects/esp-idf/en/v5.3.1/esp32/get-started/linux-macos-setup.html

```
sudo apt-get install git wget flex bison gperf python3 python3-pip python3-venv cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0
```

![alt text](image-8.png)

```
wsl -s ubuntu
```
![alt text](image-7.png)

### Instalação do Framework ESP-IDF

```
mkdir -p ~/esp
cd ~/esp
git clone -b v5.3.1 --recursive https://github.com/espressif/esp-idf.git
```

![alt text](image-9.png)

Entrando na pasta do ESP-IDF é possível verificar a instalação do Framework e todos os diretórios

![alt text](image-10.png)


Agora o script de instalação das variáveis de ambiente

```
./install.sh
```
![alt text](image-11.png)

Agora exportar as variáveis de ambiente

![alt text](image-12.png)

```
. ./export.sh
```

No PowerShell

```
usbipd list
```

![alt text](image-13.png)


Inserindo a placa na USB

![alt text](image-14.png)

Agora podemos encontrar o BUSID para realizar o Bind

```
usbipd bind --busid <BUSID>
```

```
usbipd attach --wsl --busid <BUSID>
```

```
usbipd detach --busid <BUSID>
```

![alt text](image-17.png)

Fazendo novamente o comando `usbipd list`

![alt text](image-16.png)

No terminal do Ubuntu 

```
dmesg | tail
```

![alt text](image-15.png)

Configuração das variáveis de ambiente no Ubuntu

```
. $HOME/esp/esp-idf/export.sh
```
Digitar i para inserir dados
![alt text](image-18.png)

clicar em `ESC` depois `:wq` para salvar e sair
![alt text](image-20.png)

![alt text](image-19.png)

Atualizar a configuração do arquivo .basshrc

```
$ source ~/.bashrc
```

![alt text](image-22.png)

Diretório de instalação do ESP_IDF no Ubuntu
![alt text](image-21.png)

Configuração do VSCode

Instalação de extensões

![alt text](image-24.png)

### Conectando no WSL com o VSCode

![alt text](image-25.png)

![alt text](image-26.png)

![alt text](image-27.png)

> Caso tenha duas versões posso escolher qual a distro desejo clicando em `Connect to WSL using Distro ...`

> Clicando em Open folder

![alt text](image-28.png)

A configuração da máqiuna virtual não herda as configurações da máquina Host

Configuração da extensão ESP-IDF

![alt text](image-29.png)

![alt text](image-30.png)

![alt text](image-31.png)

<mark> ### VMWARE Problema no VSCode ### </mark>

## VMWARE a configuração no VSCode não funcionou corretamente, apenas a configuração manual funcionou corretamente

![alt text](image.png)

Inserir no campo de pesquisa das configurações do VSCode

Abrir a página de configuração

![alt text](image-32.png)

![alt text](image-33.png)

![alt text](image-34.png)

![alt text](image-35.png)

> Verificar o caminho do diretório e clicar em install, ele não irá instalar mais irá configurar a versão já existente

![alt text](image-36.png)

Agora o VSCode informa a necessidade3 de instalação

![alt text](image-37.png)

![alt text](image-38.png)

![alt text](image-39.png)

![alt text](image-40.png)

![alt text](image-41.png)

![alt text](image-42.png)

![alt text](image-43.png)

![alt text](image-44.png)

![alt text](image-45.png)

![alt text](image-46.png)

![alt text](image-47.png)

![alt text](image-48.png)

![alt text](image-49.png)

![alt text](image-50.png)

![alt text](image-51.png)

![alt text](image-52.png)


<mark>
@ext:espressif.esp-idf-extension port
</mark>

```
sudo apt-get install git wget flex bison gperf python3 python3-pip python3-venv cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0
```

![alt text](image-1.png)

![alt text](image-2.png)

Comando no linux para encontrar os dispositivos conectados bem como portas usb

```
lsusb
```

![alt text](image-3.png)

![alt text](image-53.png)

Clicar em backup e Sync settings e entrar com a conta do Github

![alt text](image-54.png)

![alt text](image-55.png)



































