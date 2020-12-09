# Vmware on Raspberry PI 4

- [1. Descrição](#link1)
- [2. Objetivos](#link2)
- [3. Instalação](#link3)
- [4. Administração](#link4)
- [5. Máquinas Virtuais](#link5)

<a id="link1"></a>
## 1. Descrição

A virtualização é o processo de criar apartir de software uma simulação ou versão virtual de algo que até então era apenas 
físico, por exemplo (servidores, armazenamento, rede, etc).

Imagine 3 servidores que rodem em cada um, uma aplicação. Só que cada um está usando 30% da capacidade disponível.</br>
Atraves da virtualização podemos em um novo servidor criar versões virtuais dos antigos servidores e rodar as 3 aplicações
aproveitando melhor os recursos e reutilizar os antigos hardwares para outras aplicações.

Cada servidor virtual é chamado de virtual machine e tem as mesmas caracteristicas das máquinas físicas (Sistema operacional,
memória, disco, rede, etc)

Existem vários softwares disponíveis no mercado, disponíveis para rodar em máquinas cliente ou em um servidor.

Para a demostração a seguir será utilizado o VMware ESXi, rodando diretamente no hardware do servidor sem 
exigir um sistema operacional.

Existem versões desktop que são executados em máquinas que rodam Microsoft Windows, Linux e macOS

ex: VirtuaBox, VMware Workstation, Windows Virtual PC

<a id="link2"></a>
## 2. Objetivos

- Instalar o VMware ESXi em um raspberry pi4 com 4GB de ram (8GB recomendado)
- Utilizar a interface de administração
- Criar máquins virtuais
- Executar comandos básicos

<a id="link3"></a>
## 3. Instalação

Essa instalação é baseada na apresentada pelo canal NetworkChuck (links no final).

Itens necessários:

- Cartão de memória
- Raspberry PI 4 (4GB ou 8GB)
- 2 pen drivers

	- Instalar o raspian lite usando o instalador oficial Raspberry
	
	![Screenshot](/images/vm03.jpg)

	![Screenshot](/images/vm04.jpg)
	
	![Screenshot](/images/vm05.jpg)
	
	- Logar e atualizar a eeprom

	Login: pi</br>
	Password: raspberry

	![Screenshot](/images/vm06.jpg)

	![Screenshot](/images/vm07.jpg)
	
	sudo rpi-eeprom-update</br>
	sudo rpi-eeprom-update -a
	
	![Screenshot](/images/vm08.jpg)

	- Realizar erase do cartão

	![Screenshot](/images/vm09.jpg)
	
	- Baixar Raspberry Pi Firmware
	
	Latest Raspberry Pi Firmware: https://bit.ly/2HpIaG6</br>
	UEFI Raspberry Pi Firmware: https://bit.ly/3jota8D

	extrair conteúdo dos 2 arquivos

	copiar</br>
	C:\Users\user\Downloads\rasp_firm\firmware-master\firmware-master\boot\*.*

	para a raiz do cartão sd

	delete os 4 arquivos kernel

	copiar</br>
	C:\Users\user\Downloads\rasp_firm\RPi4_UEFI_Firmware_v1.20\*.*

	para a raiz do cartão sd (with replace)

	No cartão edite arquivo config.txt
	acrescente no final dele: gpu_mem=16

	Salve o arquivo, remova o cartão

	![Screenshot](/images/vm10.jpg)

	![Screenshot](/images/vm11.jpg)
	
	![Screenshot](/images/vm12.jpg)


	- Preparar ESXi versão Arm para instalação
	
	Baixar o arquivo ISO</br>
	VMWare Installer ISO: https://bit.ly/2J0bSCn

	Caso não tenha, crie sua conta e realize download do arquivo iso

	ex: VMware-VMvisor-Installer-7.0.0-17230755.aarch64.iso

	
	![Screenshot](/images/vm13.jpg)

	![Screenshot](/images/vm14.jpg)

	Gravar o ISO em um pendrive usando o Rufos (windows)

	Selecione o arquivo ISO, e em tamanho do cluster = 32 quilobytes

	clique em iniciar, após terminar, insira o cartão SD no raspberry e o pendrive
	
	![Screenshot](/images/vm15.jpg)	
	
	- Instando o ESXi
	
	Ligue o raspberry e no teclado clique ESC até entrar na tela de configuração
	
	Desabilite o limite de 3GB de RAM
	
	![Screenshot](/images/vm16.jpg)

	![Screenshot](/images/vm17.jpg)

	![Screenshot](/images/vm18.jpg)

	![Screenshot](/images/vm19.jpg)

	![Screenshot](/images/vm20.jpg)

	![Screenshot](/images/vm21.jpg)	

	![Screenshot](/images/vm22.jpg)

	![Screenshot](/images/vm23.jpg)	
	
	Selecione para dar boot pelo pen driver
	
	![Screenshot](/images/vm24.jpg)

	![Screenshot](/images/vm25.jpg)	
	
	Iniciando a instalação
	
	Configure senha de root
	
	Configure as configurações de rede, nesse exemplo, vamos deixar IP via DHCP

	![Screenshot](/images/vm26.jpg)

	![Screenshot](/images/vm27.jpg)

	![Screenshot](/images/vm28.jpg)

	![Screenshot](/images/vm29.jpg)

	![Screenshot](/images/vm30.jpg)

	![Screenshot](/images/vm31.jpg)	

	![Screenshot](/images/vm32.jpg)

	![Screenshot](/images/vm33.jpg)		
	
	![Screenshot](/images/vm34.jpg)		

	Após instação completa, mais uma vez entre na tela de configuração para dar boot pelo Pen Drive e não pelo cartão
	
	![Screenshot](/images/vm35.jpg)

	![Screenshot](/images/vm36.jpg)

	![Screenshot](/images/vm37.jpg)

	![Screenshot](/images/vm38.jpg)

	![Screenshot](/images/vm39.jpg)

	![Screenshot](/images/vm40.jpg)	

	![Screenshot](/images/vm41.jpg)

	![Screenshot](/images/vm42.jpg)		
	
	![Screenshot](/images/vm43.jpg)			

	![Screenshot](/images/vm44.jpg)				
	
<a id="link4"></a>
## 4. Administração	

- Via browser

	Acesse o browser e digite o IP do servidor, em seguida entre com usuário root e senha definida na instalação.

	![Screenshot](/images/vm50.jpg)		
	
	![Screenshot](/images/vm51.jpg)			

	![Screenshot](/images/vm52.jpg)		
	
- Via terminal	

	Habilite o SSH para podemos acessar via terminal

	![Screenshot](/images/vm53.jpg)			

	![Screenshot](/images/vm54.jpg)	

- Via console SSH no browser

	![Screenshot](/images/vm55.jpg)	
	
	![Screenshot](/images/vm56.jpg)	
	
	
<a id="link5"></a>
## 5. Máquinas Virtuais

Agora que o servidor está pronto e funcionando, podemos criar as máquinas virtuais.

Computadores dentro do nosso computador principal (host).

Os recursos da máquina serão compartilhados entre o sistema host (VMware ESXi) e as máquinas virtuais.

Dessa forma, cada VM usará parte da memória, processsador, disco, rede

Antes de criar as VMs, executar 2 etapas

- Adicionar um HD externo, que fará o papel da storage, onde serão salvos os discos das VMs

	![Screenshot](/images/vm57.jpg)	

	![Screenshot](/images/vm58.jpg)	


- Baixar imagens ISO dos sistemas que iremos instalar. no nosso exemplo será uma imagem do Ubuntu 20 para a arquitetura ARM.

	Vamos baixar para o computador local onde o abrimos o browser e depois faremos o upload para o ESXi

	![Screenshot](/images/vm59.jpg)	

- Criar a VM


	![Screenshot](/images/vm60.jpg)	

	![Screenshot](/images/vm61.jpg)	
	
	![Screenshot](/images/vm62.jpg)		

	![Screenshot](/images/vm63.jpg)	

	![Screenshot](/images/vm64.jpg)	
	
	![Screenshot](/images/vm65.jpg)		

	![Screenshot](/images/vm66.jpg)	

	![Screenshot](/images/vm67.jpg)	
	
	![Screenshot](/images/vm68.jpg)		

	![Screenshot](/images/vm69.jpg)	










https://ubuntu.com/download/server/arm
https://www.vmware.com/
https://www.youtube.com/watch?v=6aLyZisehCU