# Vmware on raspberry pi

1) Instalar o raspian lite usando o instalador oficial Raspberry

2) Realizar update da eeprom

Login: pi
Password: raspberry

sudo rpi-eeprom-update
sudo rpi-eeprom-update -a

sudo rebbot

3) Realizar erase do cartão

realizar download

Latest Raspberry Pi Firmware: https://bit.ly/2HpIaG6
UEFI Raspberry Pi Firmware: https://bit.ly/3jota8D

extrair conteúdo

copy C:\Users\user\Downloads\rasp_firm\firmware-master\firmware-master\boot\*.*

para a raiz do cartão sd

delete os 4 arquivos kernel

copy C:\Users\user\Downloads\rasp_firm\RPi4_UEFI_Firmware_v1.20\*.*

para a raiz do cartão sd (with replace)

No cartão edite arquivo config.txt
acrescente no final dele: gpu_mem=16

salve o arquivo, remova cartão

4) Install do ESXi versão Arm

Download 
VMWare Installer ISO: https://bit.ly/2J0bSCn

Caso não tenha, crie sua conta, realize download do arquivo iso

ex: VMware-VMvisor-Installer-7.0.0-17230755.aarch64.iso

Vamos gravar esse iso em um pendrive usando o Rufos (windows)

Selecione o arquivo ISO, e em tamanho do cluster = 32 quilobytes

clique em iniciar, apoós terminar, insira p cartão SD no raspberry e o pendrive

Ligue o raspberry e mo teclado clique ESC

=======================

Login

Habillitar o ssh



/etc/init.d/usbarbitrator stop
chkconfig usbarbitrator off

https://ubuntu.com/download/server/arm







