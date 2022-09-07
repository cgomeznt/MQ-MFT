Instalación MQ MFT
===================


Este manual describe como realizar la instalacion de MQ MFT Version 9.1.0.0 en Linux Centos 7.5

1.‐ Debemos tener instaladas los paquetes libgcc y libstdc++::

	# rpm -qa | egrep "libgcc|libstdc++"
	libstdc++-4.8.5-44.el7.x86_64
	libgcc-4.8.5-44.el7.x86_64
	libstdc++-4.8.5-44.el7.i686
	libgcc-4.8.5-44.el7.i686

Le colocamos un nombre al servidor::

	# hostnamectl set-hostname mq-serve

Garantizar que el DNS este respondiendo adecuadamente.

NOTA: MQ corre bajo una maquina virtual de JAVA, pero no es necesario instalarla porque ya viene embebida en el MQ MFT.


2.‐ Bajamos los instaladores de la pagina del fabricante, los archivos son:

IBM_MQ_9.1_LINUX_X86-64.tar.gz

WS_MQ_LINUX_ON_X86_64_7.5.0.2_IMG.tar.gz

WS_MQ_CLIENT_LIN_X86_64_7.5.0.2.tar.gz

MANAGED_FT_AGENT_4690_7.5.0.2_IMG.zip

 y se colocan en un directorio temporal, en este caso: /opt/mq_instaladores

3.‐ Descomprimimos IBM_MQ_9.1_LINUX_X86-64.tar.gz::

	# mkdir –p /opt/mq_instaladores/mqm
	# tar ‐xvf IBM_MQ_9.1_LINUX_X86-64.tar.gz ‐C /opt/mq_instaladores/mqm

Visulizar el contenido::

	# ls
	MQServer
	# cd MQServer/
	# ls
	Advanced                             MQSeriesFTService-9.1.0-0.x86_64.rpm  MQSeriesMsg_pl-9.1.0-0.x86_64.rpm
	copyright                            MQSeriesFTTools-9.1.0-0.x86_64.rpm    MQSeriesMsg_pt-9.1.0-0.x86_64.rpm
	crtmqpkg                             MQSeriesGSKit-9.1.0-0.x86_64.rpm      MQSeriesMsg_ru-9.1.0-0.x86_64.rpm
	lap                                  MQSeriesJava-9.1.0-0.x86_64.rpm       MQSeriesMsg_Zh_CN-9.1.0-0.x86_64.rpm
	licenses                             MQSeriesJRE-9.1.0-0.x86_64.rpm        MQSeriesMsg_Zh_TW-9.1.0-0.x86_64.rpm
	mqlicense.sh                         MQSeriesMan-9.1.0-0.x86_64.rpm        MQSeriesRuntime-9.1.0-0.x86_64.rpm
	MQSeriesAMQP-9.1.0-0.x86_64.rpm      MQSeriesMsg_cs-9.1.0-0.x86_64.rpm     MQSeriesSamples-9.1.0-0.x86_64.rpm
	MQSeriesAMS-9.1.0-0.x86_64.rpm       MQSeriesMsg_de-9.1.0-0.x86_64.rpm     MQSeriesSDK-9.1.0-0.x86_64.rpm
	MQSeriesBCBridge-9.1.0-0.x86_64.rpm  MQSeriesMsg_es-9.1.0-0.x86_64.rpm     MQSeriesServer-9.1.0-0.x86_64.rpm
	MQSeriesClient-9.1.0-0.x86_64.rpm    MQSeriesMsg_fr-9.1.0-0.x86_64.rpm     MQSeriesSFBridge-9.1.0-0.x86_64.rpm
	MQSeriesExplorer-9.1.0-0.x86_64.rpm  MQSeriesMsg_hu-9.1.0-0.x86_64.rpm     MQSeriesWeb-9.1.0-0.x86_64.rpm
	MQSeriesFTAgent-9.1.0-0.x86_64.rpm   MQSeriesMsg_it-9.1.0-0.x86_64.rpm     MQSeriesXRService-9.1.0-0.x86_64.rpm
	MQSeriesFTBase-9.1.0-0.x86_64.rpm    MQSeriesMsg_ja-9.1.0-0.x86_64.rpm     READMES
	MQSeriesFTLogger-9.1.0-0.x86_64.rpm  MQSeriesMsg_ko-9.1.0-0.x86_64.rpm     repackage



4.‐ Verificamos la licencia, en este caso se utiliza como producto de prueba::

	/opt/mq_instaladores/mqm/MQServer/mqlicense.sh ‐‐text_only

Pulsamo 1, para aceptar la licencia::

	Pulse Intro para seguir visualizando el acuerdo de 
	licencia, o entre "1" para aceptar el acuerdo, "2" para no 
	aceptarlo, "3" para imprimirlo, "4" para leer los términos 
	que no son IBM, "5" para visualizarlo en inglés o "99" para 
	volver a la pantalla anterior.
	1

	Agreement accepted:  Proceed with install.

5.‐ Para instalar todos los componentes ejecutamos::

	# rpm -ivh /opt/mq_instaladores/mqm/MQServer/MQSeries*.rpm
	Preparando...                         ################################# [100%]
	Creating group mqm
	Creating user mqm
	Actualizando / instalando...
	   1:MQSeriesRuntime-9.1.0-0          ################################# [  3%]
	   2:MQSeriesJRE-9.1.0-0              ################################# [  6%]
	   3:MQSeriesJava-9.1.0-0             ################################# [  9%]
	   4:MQSeriesServer-9.1.0-0           ################################# [ 12%]
	Updated PAM configuration in /etc/pam.d/ibmmq

	WARNING: System settings for this system do not meet recommendations for this product 
		 See the log file at "/tmp/mqconfig.9243.log" for more information

	   5:MQSeriesFTBase-9.1.0-0           ################################# [ 15%]
	   6:MQSeriesFTAgent-9.1.0-0          ################################# [ 18%]
	   7:MQSeriesFTService-9.1.0-0        ################################# [ 21%]
	   8:MQSeriesFTLogger-9.1.0-0         ################################# [ 24%]
	   9:MQSeriesFTTools-9.1.0-0          ################################# [ 26%]
	  10:MQSeriesAMQP-9.1.0-0             ################################# [ 29%]
	  11:MQSeriesAMS-9.1.0-0              ################################# [ 32%]
	  12:MQSeriesWeb-9.1.0-0              ################################# [ 35%]
	  13:MQSeriesXRService-9.1.0-0        ################################# [ 38%]
	  14:MQSeriesBCBridge-9.1.0-0         ################################# [ 41%]
	  15:MQSeriesSFBridge-9.1.0-0         ################################# [ 44%]
	  16:MQSeriesExplorer-9.1.0-0         ################################# [ 47%]
	  17:MQSeriesClient-9.1.0-0           ################################# [ 50%]
	  18:MQSeriesGSKit-9.1.0-0            ################################# [ 53%]
	  19:MQSeriesMan-9.1.0-0              ################################# [ 56%]
	  20:MQSeriesMsg_cs-9.1.0-0           ################################# [ 59%]
	  21:MQSeriesMsg_de-9.1.0-0           ################################# [ 62%]
	  22:MQSeriesMsg_es-9.1.0-0           ################################# [ 65%]
	  23:MQSeriesMsg_fr-9.1.0-0           ################################# [ 68%]
	  24:MQSeriesMsg_hu-9.1.0-0           ################################# [ 71%]
	  25:MQSeriesMsg_it-9.1.0-0           ################################# [ 74%]
	  26:MQSeriesMsg_ja-9.1.0-0           ################################# [ 76%]
	  27:MQSeriesMsg_ko-9.1.0-0           ################################# [ 79%]
	  28:MQSeriesMsg_pl-9.1.0-0           ################################# [ 82%]
	  29:MQSeriesMsg_pt-9.1.0-0           ################################# [ 85%]
	  30:MQSeriesMsg_ru-9.1.0-0           ################################# [ 88%]
	  31:MQSeriesMsg_Zh_CN-9.1.0-0        ################################# [ 91%]
	  32:MQSeriesMsg_Zh_TW-9.1.0-0        ################################# [ 94%]
	  33:MQSeriesSamples-9.1.0-0          ################################# [ 97%]
	  34:MQSeriesSDK-9.1.0-0              ################################# [100%]


En la salida del comando anterior siempre debemos revisar el LOG, porque debemos asegurar que todo este en PASS::

	# cat  /tmp/mqconfig.9243.log
	mqconfig: Analyzing CentOS Linux release 7.9.2009 (Core) settings for IBM
		  MQ V9.1

	System V Semaphores
	  semmsl     (sem:1)  250 semaphores                     IBM>=32           PASS
	  semmns     (sem:2)  0 of 32000 semaphores      (0%)    IBM>=4096         PASS
	  semopm     (sem:3)  32 operations                      IBM>=32           PASS
	  semmni     (sem:4)  0 of 128 sets              (0%)    IBM>=128          PASS

	System V Shared Memory
	  shmmax              18446744073692774399 bytes         IBM>=268435456    PASS
	  shmmni              0 of 4096 sets             (0%)    IBM>=4096         PASS
	  shmall              0 of 18446744073692774399 pages (0%)    IBM>=2097152      PASS

	System Settings
	  file-max            1024 of 94452 files        (1%)    IBM>=524288       FAIL
	  pid_max             125 of 131072 processids   (0%)    IBM>=32768        PASS
	  threads-max         125 of 7594 threads        (1%)    IBM>=32768        FAIL

	Current User Limits (root)
	  nofile       (-Hn)  4096 files                         IBM>=10240        FAIL
	  nofile       (-Sn)  1024 files                         IBM>=10240        FAIL
	  nproc        (-Hu)  0 of 3797 processes        (0%)    IBM>=4096         WARN
	  nproc        (-Su)  0 of 3797 processes        (0%)    IBM>=4096         WARN

	mqconfig: Any values listed in the "Current User Limits" section are resource
		  limits for the user who ran mqconfig.
		  
		  If the user account that is used to invoke this script (root)
		  is not the same as the user account that is used to start the
		  queue manager, then the assessed values will not be accurate.
		  
		  If you normally start your queue managers as the mqm user, you
		  should switch to mqm and run mqconfig there.
		  
		  If other members of the mqm group also start queue managers, all
		  those members should run mqconfig, to ensure that their limits
		  are suitable for IBM MQ.

	mqconfig: A PASS score means your system meets the minimum IBM
		  recommendations but busy systems might need higher limits to run
		  production workloads.
		  
		  For performance-critical environments, further performance testing
		  should always be conducted using workloads that are representative
		  of the real volume.


Tal y como lo indica la salida en el LOG de la instalación de MQSeriesServer,(En este primera corrida existen varios puntos que debemos
corregir).


7.‐ Para solucionar estas observaciones debemos:

7.1 Modificar los semáforos, cantidad de archivos abiertos y tiempo de las conexiones colocando los valores
que indica el reporte, editando el archivo /etc/sysctl.conf::

	Vi /etc/sysctl.conf

	# Agregamos estas lineas
	mqm soft nofile 10240
	mqm hard nofile 10240

	mqm soft nproc 4096
	mqm hard nproc 4096

Ahora corregimos el máximo de archivos y de hilos::

	# cat /proc/sys/fs/file-max
	94452

	# sysctl -w fs.file-max=524288
	fs.file-max = 524288

	# cat /proc/sys/kernel/threads-max
	7594
	# sysctl -w kernel.threads-max=32768
	kernel.threads-max = 32768


7.3 Ejecutar el comando su mqm -c "/opt/mqm/bin/mqconfig" no debería salir ningún FAIL ni
WARNING::


	# su mqm -c "/opt/mqm/bin/mqconfig" 
	mqconfig: Analyzing CentOS Linux release 7.9.2009 (Core) settings for IBM
		  MQ V9.1

	System V Semaphores
	  semmsl     (sem:1)  250 semaphores                     IBM>=32           PASS
	  semmns     (sem:2)  0 of 32000 semaphores      (0%)    IBM>=4096         PASS
	  semopm     (sem:3)  32 operations                      IBM>=32           PASS
	  semmni     (sem:4)  0 of 128 sets              (0%)    IBM>=128          PASS

	System V Shared Memory
	  shmmax              18446744073692774399 bytes         IBM>=268435456    PASS
	  shmmni              0 of 4096 sets             (0%)    IBM>=4096         PASS
	  shmall              0 of 18446744073692774399 pages (0%)    IBM>=2097152      PASS

	System Settings
	  file-max            960 of 524288 files        (0%)    IBM>=524288       PASS
	  pid_max             123 of 131072 processids   (0%)    IBM>=32768        PASS
	  threads-max         123 of 32768 threads       (0%)    IBM>=32768        PASS

	Current User Limits (mqm)
	  nofile       (-Hn)  10240 files                        IBM>=10240        PASS
	  nofile       (-Sn)  10240 files                        IBM>=10240        PASS
	  nproc        (-Hu)  9 of 4096 processes        (0%)    IBM>=4096         PASS
	  nproc        (-Su)  9 of 4096 processes        (0%)    IBM>=4096         PASS

	mqconfig: Any values listed in the "Current User Limits" section are resource
		  limits for the user who ran mqconfig.
		  
		  If the user account that is used to invoke this script (mqm)
		  is not the same as the user account that is used to start the
		  queue manager, then the assessed values will not be accurate.
		  
		  If you normally start your queue managers as the mqm user, you
		  should switch to mqm and run mqconfig there.
		  
		  If other members of the mqm group also start queue managers, all
		  those members should run mqconfig, to ensure that their limits
		  are suitable for IBM MQ.

	mqconfig: A PASS score means your system meets the minimum IBM
		  recommendations but busy systems might need higher limits to run
		  production workloads.
		  
		  For performance-critical environments, further performance testing
		  should always be conducted using workloads that are representative
		  of the real volume.


8.‐ Debemos indicar que esta instalación es la instalación primaria, lo hacemos ejecutando el comando::

	# /opt/mqm/bin/setmqinst -i -p /opt/mqm/
	143 de 143 tareas se han completado con éxito.
	'Installation1' (/opt/mqm) establecido como la instalación primaria.

9.‐ Definimos en la variable PATH la ruta de los binarios de MQ en el archivo /etc/bashrc::

	# vi /etc/bashrc
	export PATH=$PATH:/opt/mqm/bin

Verificando la correcta instalación (Ejecutar este paso es opcional, al finalizar podemos eliminar los QManagers creados)
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

1.‐ Local (Ambos Qmanager en el mismo Equipo)

1.1.‐ Nos cambiamos al usuario mqm y nos ubicamos al directorio MQ_INSTALLATION_PATH/bin (El instalador crea el usuario)::

	# su – mqm
	# cd /opt/mqm/bin

Nos aseguramos de crear el .profile si no existe dentro del home del usuario mqm::

	$ cp /etc/bashrc .profile
	$ source .profile

1.2.‐ Ejecutamos los comandos, para setear las variables de ambientes de mq y con el segundo comando vemos los
datos de las variables::


	$ source ./setmqenv -s

	-bash-4.2$ dspmq
	dspmq      dspmqcsv   dspmqinf   dspmqras   dspmqspl   dspmqtrn   dspmqweb   
	dspmqaut   dspmqfls   dspmqinst  dspmqrte   dspmqtrc   dspmqver   
	-bash-4.2$ dspmqver 
	Name:        IBM MQ
	Version:     9.1.0.0
	Level:       p910-L180705
	BuildType:   IKAP - (Production)
	Platform:    IBM MQ for Linux (x86-64 platform)
	Mode:        64-bit
	O/S:         Linux 3.10.0-1160.31.1.el7.x86_64
	InstName:    Installation1
	InstDesc:    
	Primary:     Yes
	InstPath:    /opt/mqm
	DataPath:    /var/mqm
	MaxCmdLevel: 910
	LicenseType: Production

1.3.‐ Creamos un Q Manager llamado QMA::

	$ crtmqm QMA
	IBM MQ queue manager created.
	Directory '/var/mqm/qmgrs/QMA' created.
	The queue manager is associated with installation 'Installation1'.
	Creating or replacing default objects for queue manager 'QMA'.
	Default objects statistics : 84 created. 0 replaced. 0 failed.
	Completing setup.
	Setup completed.

1.4.‐ Iniciamos el QMananger::

	$ strmqm QMA
	IBM MQ queue manager 'QMA' starting.
	The queue manager is associated with installation 'Installation1'.
	5 log records accessed on queue manager 'QMA' during the log replay phase.
	Log replay for queue manager 'QMA' complete.
	Transaction manager state recovered for queue manager 'QMA'.
	IBM MQ queue manager 'QMA' started using V9.1.0.0.

1.5.‐ Iniciamos la consola de comando de MQ para trabajar con el QManager recién creado, IMPORTANTE dentro de ella es que se va escribir otros comandos::

	$ runmqsc QMA
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager QMA.

1.6.‐ Creamos una cola local de pruebas llamada QUEUE1 (Esto es dentro del CLI que dejo abierto el comando anterior, Escribimos esto:

DEFINE QLOCAL (QUEUE1)::

	DEFINE QLOCAL (QUEUE1)
	     1 : DEFINE QLOCAL (QUEUE1)
	AMQ8006I: IBM MQ queue created.

Luego escribimos end::

	end
	     2 : end
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.


1.7.‐ Ejecutamos el comando amqsput para colocar un mensaje de prueba en la cola anteriormente creada, este comando se encuentra en la ruta MQ_INSTALLATION_PATH/samp/bin. Coloca algún texto para el contenido del mensaje. Un enter con línea vacía indica el fin del mensaje::

	$ cd /opt/mqm/samp/bin/

	$ ./amqsput QUEUE1 QMA
	Sample AMQSPUT0 start
	target queue is QUEUE1
	Hola Mundo.

	Sample AMQSPUT0 end

1.8.‐ Ejecutamos el comando amqsget para retirar el mensaje que colocamos en la cola anteriormente::


	$ ./amqsput QUEUE1 QMA
	Sample AMQSPUT0 start
	target queue is QUEUE1
	Hola Mundo.

	Sample AMQSPUT0 end
	-bash-4.2$ ./amqsget QUEUE1 QMA
	Sample AMQSGET0 start
	message <Hola Mundo.>

	no more messages
	Sample AMQSGET0 end

2.‐ Remoto (Qmanagers en servidores Diferentes)
Para probar de forma remota necesitamos dos equipos uno que sea el Sender y otro el Receiver, en nuestro caso 

mq‐fte01 será el sender y mq‐fte‐02 será el reciver.


2.1.‐ En el receiver::

	$ crtmqm QMB
	IBM MQ queue manager created.
	Directory '/var/mqm/qmgrs/QMB' created.
	The queue manager is associated with installation 'Installation1'.
	Creating or replacing default objects for queue manager 'QMB'.
	Default objects statistics : 84 created. 0 replaced. 0 failed.
	Completing setup.
	Setup completed.


	$ strmqm QMB
	IBM MQ queue manager 'QMB' starting.
	The queue manager is associated with installation 'Installation1'.
	5 log records accessed on queue manager 'QMB' during the log replay phase.
	Log replay for queue manager 'QMB' complete.
	Transaction manager state recovered for queue manager 'QMB'.
	IBM MQ queue manager 'QMB' started using V9.1.0.0.

Ejecutar el runmqsc QMB y ir ejecutando el siguiente CLI::

	DEFINE QLOCAL (RECEIVER.Q)
	DEFINE LISTENER (LISTENER1) TRPTYPE (TCP) CONTROL (QMGR) PORT (1414)
	START LISTENER (LISTENER1)
	DEFINE CHANNEL (QMA.QMB) CHLTYPE (RCVR) TRPTYPE (TCP)
	end


	$ runmqsc QMB
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager QMB.


	DEFINE QLOCAL (RECEIVER.Q)
	     1 : DEFINE QLOCAL (RECEIVER.Q)
	AMQ8006I: IBM MQ queue created.
	DEFINE LISTENER (LISTENER1) TRPTYPE (TCP) CONTROL (QMGR) PORT (1414)
	     2 : DEFINE LISTENER (LISTENER1) TRPTYPE (TCP) CONTROL (QMGR) PORT (1414)
	AMQ8626I: IBM MQ listener created.
	START LISTENER (LISTENER1)
	     3 : START LISTENER (LISTENER1)
	AMQ8021I: Request to start IBM MQ listener accepted.
	DEFINE CHANNEL (QMA.QMB) CHLTYPE (RCVR) TRPTYPE (TCP)
	     4 : DEFINE CHANNEL (QMA.QMB) CHLTYPE (RCVR) TRPTYPE (TCP)
	AMQ8014I: IBM MQ channel created.
	end
	     5 : end
	4 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.

Ejecutar un netstat -natp | grep -i listen y veremos el puerto 1414 en escucha ::

	# netstat -natp | grep -i listen
	tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      875/sshd            
	tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      970/master          
	tcp6       0      0 :::1414                 :::*                    LISTEN      14088/runmqlsr      
	tcp6       0      0 :::22                   :::*                    LISTEN      875/sshd            
	tcp6       0      0 ::1:25                  :::*                    LISTEN      970/master  


2.2.‐ En el Sender, como estos comando ya los ejecutamos en las primeras pruebas 

$ crtmqm QMA # Nos dirá AMQ8110E: IBM MQ queue manager already exists.

$ strmqm QMA # Nos IBM MQ queue manager running::

	$ crtmqm QMA 
	AMQ8110E: IBM MQ queue manager already exists.
	
	$ strmqm QMA 
	IBM MQ queue manager running.


	DEFINE QREMOTE (LOCAL.DEF.OF.REMOTE.QUEUE) RNAME (RECEIVER.Q) RQMNAME ('QMB') XMITQ (QMB)

	DEFINE CHANNEL (QMA.QMB) CHLTYPE (SDR) CONNAME ('192.168.1.110(1414)') XMITQ (QMB) TRPTYPE (TCP)

En el comando strmqm QMA, ejecutar los siguientes CLI::

	DEFINE QLOCAL (QMB) USAGE (XMITQ)
	DEFINE QREMOTE (LOCAL.DEF.OF.REMOTE.QUEUE) RNAME (RECEIVER.Q) RQMNAME ('QMB') XMITQ (QMB)

	DEFINE CHANNEL (QMA.QMB) CHLTYPE (SDR) CONNAME ('192.168.1.110(1414)') XMITQ (QMB) TRPTYPE (TCP)
	START CHANNEL(QMA.QMB)
	end

Esta es la ejecución del comando anterior y sus salidas::

	$ strmqm QMA 
	IBM MQ queue manager running.
	-bash-4.2$ runmqsc QMA
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager QMA.


	DEFINE QLOCAL (QMB) USAGE (XMITQ)
	     1 : DEFINE QLOCAL (QMB) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
		        
	DEFINE QREMOTE (LOCAL.DEF.OF.REMOTE.QUEUE) RNAME (RECEIVER.Q) RQMNAME (QMB') XMITQ (QMB)
	     3 : DEFINE QREMOTE (LOCAL.DEF.OF.REMOTE.QUEUE) RNAME (RECEIVER.Q) RQMNAME (QMB') XMITQ (QMB)
	AMQ8405I: Syntax error detected at or near end of command segment below:-
	DEFINE QREMOTE (LOCAL.DEF.OF.REMOTE.QUEUE) RNAME (RECEIVER.Q) RQMNAME (QMB'

		       
	DEFINE QREMOTE (LOCAL.DEF.OF.REMOTE.QUEUE) RNAME (RECEIVER.Q) RQMNAME ('QMB') XMITQ (QMB)
	     4 : DEFINE QREMOTE (LOCAL.DEF.OF.REMOTE.QUEUE) RNAME (RECEIVER.Q) RQMNAME ('QMB') XMITQ (QMB)
	AMQ8006I: IBM MQ queue created.
	DEFINE CHANNEL (QMA.QMB) CHLTYPE (SDR) CONNAME ('192.168.1.110(1414)') XMITQ (QMB) TRPTYPE (TCP)
	     5 : DEFINE # hostnamectl set-hostname mq-serverCHANNEL (QMA.QMB) CHLTYPE (SDR) CONNAME ('192.168.1.110(1414)') XMITQ (QMB) TRPTYPE (TCP)
	AMQ8014I: IBM MQ channel created.
	START CHANNEL(QMA.QMB)
	     6 : START CHANNEL(QMA.QMB)
	AMQ8018I: Start IBM MQ channel accepted.
	end
	     7 : end
	6 MQSC commands read.
	All valid MQSC commands were processed.


2.3.‐ Colocamos un mensaje en la cola del sender para probar, un enter para salir del CLI::

	$ ./amqsput LOCAL.DEF.OF.REMOTE.QUEUE QMA
	Sample AMQSPUT0 start
	target queue is LOCAL.DEF.OF.REMOTE.QUEUE
	Esta es la prueba

	Sample AMQSPUT0 end

2.4.‐ En el receiver leemos los mensajes, un enter para salir del CLI::

	$ ./amqsget RECEIVER.Q QMB
	Sample AMQSGET0 start
	message <Esta es la prueba>


	no more messages
	Sample AMQSGET0 end

Creación de Usuario para conexión de Agentes.
++++++++++++++++++++++++++++++++++++++++++++


Con la finalidad de que la conexión de los agentes sea transparente, se debe crear un usuario para que la autenticación se realice de forma local y no con el usuario donde se esta ejecutando el agente de transferencia de archivos, para este caso el usuario es usrmq. 

NOTA: Websphere MQ al momento de realizar la búsqueda del usuario los hace en Mayúscula, por ende debemos crear el mismo usuario tanto en mayúsculas como en minúscula.::

	# adduser -c "Usuario para la conexión de agentes FTE" usrmq
	# usermod -G mqm usrmq


	# adduser -c "Usuario para la conexión de agentes FTE" USRMQ
	# usermod -G mqm USRMQ


Creación y Configuración de Coordinator, Commander, Agente del AS400 y Agentes clientes en el servidor MQ.
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Para la creación de las colas necesarias para el funcionamiento de MQ FTE debemos realizar lo siguiente:

1.‐ Crear el archivo /etc/src‐mqm.sh con el siguiente contenido. (Este es el contenido puede cambiar según sea el Ambiente, DEV, QA y PROD)::

	# vi /etc/src‐mqm.sh

	#!/bin/bash

	export COORDINATOR="CRC01CRD"
	export COORDINATOR_PORT="1414"
	export COMMANDER="CRC01CMM"
	export COMMANDER_PORT="1416"
	export SRVFS_CLIENT="SRVFSAGN"
	export SRVFS_CLIENT_PORT="1418"


2.‐ Agregar las siguientes líneas en el archivo /etc/bashrc para que las variables estén disponibles para cualquier usuario::

	# vi /etc/bashrc 
	source /etc/src‐mqm.sh

3.‐ Modifica la variable PATH para poder ejecutar los comandos de MQ desde cualquier punto. Esto lo hacemos agregando la siguiente línea en el archivo /etc/bashrc::

	# vi /etc/bashrc
	export PATH=$PATH:/opt/mqm/bin

4.‐ Descomprimir el archivo bin-MQ.tar en la ruta /usr/local/bin. Estos scripts los deben adecuar según sea el Ambiente DEV, QA, PROD::

	# tar -xvf bin-MQ.tar -C /

	agent_def.sh             checkLoggerStatus.sh       delete-monitors.sh            ListaQM.txt
	agents.lst               checkQmanagerStatus.sh     delete-qmanager-agent.sh      memoria.proceso.sh
	checkAgentStatus.sh      create-basic-relations.sh  display-channel.sh            mq-status.crontab
	checkAgentStatus.sh.old  create-commander.sh        display-channel-status.sh     mq-status.crontab2
	check_channel_status.sh  create-coordinator.sh      display-qmanager.sh           start-channel.sh
	checkChannelStatus.sh    create-logger.sh           free_size.sh                  start-qmanager.sh
	check_dspmq.sh           create-Qmanager.sh         generate-XML-supervisores.sh  stop-qmanager.sh
	checkEnvioArchivos.sh    create-srvfs-agent.sh      Limpiar_Cache.sh              supervisores_detenidos.sh
	checkEnviosBCVIN1.sh     create-template.sh         limpiar_file_cache.sh         tools
	checkEnviosBCVIN.sh      create-transfer.sh         limpieza_logs_FFDC.sh         TranferFiles
	checkEnviosBCVOUT.sh     daemon-watch.sh            ListaQM_2.txt


IMPORTANTE editar los scripts y configurar la variable HOST según corresponda.

Nos aseguramos que tengamos todos los env necesarios::

	$ source .profile
	
	$ env
	COMMANDER_PORT=1416
	XDG_SESSION_ID=2
	HOSTNAME=mq-server
	AS400_CLIENT=CRC03AGN
	SHELL=/bin/bash
	TERM=xterm-256color
	HISTSIZE=1000
	AS400_CLIENT_PORT=1418
	USER=mqm
	LCOMMANDER=CRC01CMM
	COORDINATOR=CRC01CRD
	MAIL=/var/spool/mail/mqm
	PATH=/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/opt/mqm/bin
	PWD=/var/mqm
	LANG=en_US.UTF-8
	HISTCONTROL=ignoredups
	SHLVL=1
	HOME=/var/mqm
	LOGNAME=mqm
	COORDINATOR_PORT=1414
	LESSOPEN=||/usr/bin/lesspipe.sh %s
	_=/bin/env

Nos vamos a la ruta en donde están los scripts::

	$ cd /usr/local/bin/


5.‐ Para Crear el Coordinator ejecutar el script: create‐coordinator.sh::

	$ ./create-coordinator.sh 
	IBM MQ queue manager created.
	Directory '/var/mqm/qmgrs/CRC01CRD' created.
	The queue manager is associated with installation 'Installation1'.
	Creating or replacing default objects for queue manager 'CRC01CRD'.
	Default objects statistics : 84 created. 0 replaced. 0 failed.
	Completing setup.
	Setup completed.
	IBM MQ queue manager 'CRC01CRD' starting.
	The queue manager is associated with installation 'Installation1'.
	5 log records accessed on queue manager 'CRC01CRD' during the log replay phase.
	Log replay for queue manager 'CRC01CRD' complete.
	Transaction manager state recovered for queue manager 'CRC01CRD'.
	IBM MQ queue manager 'CRC01CRD' started using V9.1.0.0.
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : 		DEFINE LISTENER (CRC01CRD.LST) TRPTYPE (TCP) CONTROL (QMGR) PORT (1414)
	AMQ8626I: IBM MQ listener created.
	     2 : 		START LISTENER (CRC01CRD.LST)
	AMQ8021I: Request to start IBM MQ listener accepted.
	     3 : 		DEFINE CHANNEL (SYSTEM.ADMIN.SVRCONN) CHLTYPE (SVRCONN)
	AMQ8014I: IBM MQ channel created.
	     4 : 		START CHANNEL (SYSTEM.ADMIN.SVRCONN)
	AMQ8018I: Start IBM MQ channel accepted.
	     5 : 		DEFINE QLOCAL (CRC01CRD.DQ) USAGE (NORMAL)
	AMQ8006I: IBM MQ queue created.
	     6 : 		ALTER QMGR DEADQ(CRC01CRD.DQ)
	AMQ8005I: IBM MQ queue manager changed.
	     7 : 		ALTER QMGR  CHLAUTH(DISABLED)
	AMQ8005I: IBM MQ queue manager changed.
	     8 :                 SET CHLAUTH(*)  TYPE(BLOCKUSER) USERLIST(*MQADMIN) ACTION(REMOVE)
	AMQ8877I: IBM MQ channel authentication record set.
	     9 : 		SET CHLAUTH(SYSTEM.*) TYPE(ADDRESSMAP) ADDRESS(*) USERSRC(CHANNEL) ACTION(REPLACE)
	AMQ8877I: IBM MQ channel authentication record set.
	    10 :                 SET CHLAUTH(*)  TYPE(ADDRESSMAP) ADDRESS(*)  USERSRC(CHANNEL) ACTION(ADD)
	AMQ8877I: IBM MQ channel authentication record set.
	    11 : 		ALTER AUTHINFO('SYSTEM.DEFAULT.AUTHINFO.IDPWOS') AUTHTYPE(IDPWOS) CHCKCLNT(NONE)
	AMQ8567I: IBM MQ authentication information changed.
	    12 : 		ALTER CHANNEL(SYSTEM.ADMIN.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('usrmq')
	AMQ8016I: IBM MQ channel changed.
	    13 : 		ALTER CHANNEL(SYSTEM.DEF.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('usrmq')
	AMQ8016I: IBM MQ channel changed.
	    14 : 		REFRESH SECURITY TYPE(CONNAUTH)
	AMQ8560I: IBM MQ security cache refreshed.
	14 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Ejejcutamos el comando para definirlo como Coordinator.
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCM0242I: Direct the following MQSC definitions for your coordination queue manager 'CRC01CRD' to an MQSC session if you have not already done so.

	DEFINE TOPIC('SYSTEM.FTE') TOPICSTR('SYSTEM.FTE') REPLACE
	ALTER TOPIC('SYSTEM.FTE') NPMSGDLV(ALLAVAIL) PMSGDLV(ALLAVAIL)
	DEFINE QLOCAL(SYSTEM.FTE) LIKE(SYSTEM.BROKER.DEFAULT.STREAM) REPLACE
	ALTER QLOCAL(SYSTEM.FTE) DESCR('Stream for MQMFT Pub/Sub interface')
	* Altering namelist: SYSTEM.QPUBSUB.QUEUE.NAMELIST
	* Value prior to alteration:
	DISPLAY NAMELIST(SYSTEM.QPUBSUB.QUEUE.NAMELIST)
	ALTER NAMELIST(SYSTEM.QPUBSUB.QUEUE.NAMELIST) +
	 NAMES(SYSTEM.BROKER.DEFAULT.STREAM+
	 ,SYSTEM.BROKER.ADMIN.STREAM,SYSTEM.FTE)
	* Altering PSMODE.  Value prior to alteration:
	DISPLAY QMGR PSMODE
	ALTER QMGR PSMODE(ENABLED)


	BFGCM0243I: A file has been created that contains the MQSC definitions for your coordination queue manager. The file can be found here: '/var/mqm/mqft/config/CRC01CRD/CRC01CRD.mqsc'.
	Executind Commands in CRC01CRD.mqsc to create Coordinator 
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


     1 : DEFINE TOPIC('SYSTEM.FTE') TOPICSTR('SYSTEM.FTE') REPLACE
AMQ8690I: IBM MQ topic created.
     2 : ALTER TOPIC('SYSTEM.FTE') NPMSGDLV(ALLAVAIL) PMSGDLV(ALLAVAIL)
AMQ8691I: IBM MQ topic changed.
     3 : DEFINE QLOCAL(SYSTEM.FTE) LIKE(SYSTEM.BROKER.DEFAULT.STREAM) REPLACE
AMQ8006I: IBM MQ queue created.
     4 : ALTER QLOCAL(SYSTEM.FTE) DESCR('Stream for MQMFT Pub/Sub interface')
AMQ8008I: IBM MQ queue changed.
       : * Altering namelist: SYSTEM.QPUBSUB.QUEUE.NAMELIST
       : * Value prior to alteration:
     5 : DISPLAY NAMELIST(SYSTEM.QPUBSUB.QUEUE.NAMELIST)
AMQ8550I: Display namelist details.
   NAMELIST(SYSTEM.QPUBSUB.QUEUE.NAMELIST)
   NAMCOUNT(2)                          
   NAMES(SYSTEM.BROKER.DEFAULT.STREAM   
        ,SYSTEM.BROKER.ADMIN.STREAM)    
   DESCR(A list of queues for the queued Pub/Sub interface to monitor)
   ALTDATE(2022-09-06)                     ALTTIME(17.07.08)
     6 : ALTER NAMELIST(SYSTEM.QPUBSUB.QUEUE.NAMELIST) +
       :  NAMES(SYSTEM.BROKER.DEFAULT.STREAM+
       :  ,SYSTEM.BROKER.ADMIN.STREAM,SYSTEM.FTE)
AMQ8551I: IBM MQ namelist changed.
       : * Altering PSMODE.  Value prior to alteration:
     7 : DISPLAY QMGR PSMODE
AMQ8408I: Display Queue Manager details.
   QMNAME(CRC01CRD)                        PSMODE(ENABLED)
     8 : ALTER QMGR PSMODE(ENABLED)
AMQ8005I: IBM MQ queue manager changed.
8 MQSC commands read.
No commands have a syntax error.
All valid MQSC commands were processed.


6.‐ Para Crear el Commander ejecutar el script: create‐commander.sh::

	$ ./create-commander.sh 
	IBM MQ queue manager created.
	Directory '/var/mqm/qmgrs/CRC01CMM' created.
	The queue manager is associated with installation 'Installation1'.
	Creating or replacing default objects for queue manager 'CRC01CMM'.
	Default objects statistics : 84 created. 0 replaced. 0 failed.
	Completing setup.
	Setup completed.
	IBM MQ queue manager 'CRC01CMM' starting.
	The queue manager is associated with installation 'Installation1'.
	5 log records accessed on queue manager 'CRC01CMM' during the log replay phase.
	Log replay for queue manager 'CRC01CMM' complete.
	Transaction manager state recovered for queue manager 'CRC01CMM'.
	IBM MQ queue manager 'CRC01CMM' started using V9.1.0.0.
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CMM.


	     1 : 		DEFINE LISTENER (CRC01CMM.LST) TRPTYPE (TCP) CONTROL (QMGR) PORT (1416)
	AMQ8626I: IBM MQ listener created.
	     2 : 		START LISTENER (CRC01CMM.LST)
	AMQ8021I: Request to start IBM MQ listener accepted.
	     3 : 		DEFINE CHANNEL (SYSTEM.ADMIN.SVRCONN) CHLTYPE (SVRCONN)
	AMQ8014I: IBM MQ channel created.
	     4 : 		START CHANNEL (SYSTEM.ADMIN.SVRCONN)
	AMQ8018I: Start IBM MQ channel accepted.
	     5 : 		DEFINE QLOCAL (CRC01CMM.DQ) USAGE (NORMAL)
	AMQ8006I: IBM MQ queue created.
	     6 : 		ALTER QMGR DEADQ(CRC01CMM.DQ)
	AMQ8005I: IBM MQ queue manager changed.
	     7 : 		ALTER QMGR  CHLAUTH(DISABLED)
	AMQ8005I: IBM MQ queue manager changed.
	     8 :                 SET CHLAUTH(*)  TYPE(BLOCKUSER) USERLIST(*MQADMIN) ACTION(REMOVE)
	AMQ8877I: IBM MQ channel authentication record set.
	     9 :                 SET CHLAUTH(*)  TYPE(ADDRESSMAP) ADDRESS(*)  USERSRC(CHANNEL) ACTION(ADD)
	AMQ8877I: IBM MQ channel authentication record set.
	    10 : 		SET CHLAUTH(SYSTEM.*) TYPE(ADDRESSMAP) ADDRESS(*) USERSRC(CHANNEL) ACTION(REPLACE)
	AMQ8877I: IBM MQ channel authentication record set.
	    11 :                 ALTER AUTHINFO('SYSTEM.DEFAULT.AUTHINFO.IDPWOS') AUTHTYPE(IDPWOS) CHCKCLNT(NONE)
	AMQ8567I: IBM MQ authentication information changed.
	    12 : 		ALTER CHANNEL(SYSTEM.ADMIN.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('usrmq')
	AMQ8016I: IBM MQ channel changed.
	    13 : 		ALTER CHANNEL(SYSTEM.DEF.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('usrmq')
	AMQ8016I: IBM MQ channel changed.
	    14 :                 REFRESH SECURITY TYPE(CONNAUTH)
	AMQ8560I: IBM MQ security cache refreshed.
	14 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	######################################################################
	Ejecutando Comando para crear el Commander
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCL0245I: The file '/var/mqm/mqft/config/CRC01CRD/command.properties' has been created successfully.


7.‐ Para Crear el agente del AS400 ejecutar el script: create-srvfs-agent.sh::

	$ ./create-srvfs-agent.sh 
	IBM MQ queue manager created.
	Directory '/var/mqm/qmgrs/SRVFSAGN' created.
	The queue manager is associated with installation 'Installation1'.
	Creating or replacing default objects for queue manager 'SRVFSAGN'.
	Default objects statistics : 84 created. 0 replaced. 0 failed.
	Completing setup.
	Setup completed.
	IBM MQ queue manager 'SRVFSAGN' starting.
	The queue manager is associated with installation 'Installation1'.
	5 log records accessed on queue manager 'SRVFSAGN' during the log replay phase.
	Log replay for queue manager 'SRVFSAGN' complete.
	Transaction manager state recovered for queue manager 'SRVFSAGN'.
	IBM MQ queue manager 'SRVFSAGN' started using V9.1.0.0.
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : 		DEFINE LISTENER (SRVFSAGN.LST) TRPTYPE (TCP) CONTROL (QMGR) PORT (1418)
	AMQ8626I: IBM MQ listener created.
	     2 : 		START LISTENER (SRVFSAGN.LST)
	AMQ8021I: Request to start IBM MQ listener accepted.
	     3 : 		DEFINE CHANNEL (SYSTEM.ADMIN.SVRCONN) CHLTYPE (SVRCONN)
	AMQ8014I: IBM MQ channel created.
	     4 : 		START CHANNEL (SYSTEM.ADMIN.SVRCONN)
	AMQ8018I: Start IBM MQ channel accepted.
	     5 : 		DEFINE QLOCAL (SRVFSAGN.DQ) USAGE (NORMAL)
	AMQ8006I: IBM MQ queue created.
	     6 : 		ALTER QMGR DEADQ(SRVFSAGN.DQ)
	AMQ8005I: IBM MQ queue manager changed.
	     7 : 		ALTER QMGR  CHLAUTH(DISABLED)
	AMQ8005I: IBM MQ queue manager changed.
	     8 : 		SET CHLAUTH(*)  TYPE(BLOCKUSER) USERLIST(*MQADMIN) ACTION(REMOVE)
	AMQ8877I: IBM MQ channel authentication record set.
	     9 : 		SET CHLAUTH(SYSTEM.*) TYPE(ADDRESSMAP) ADDRESS(*) USERSRC(CHANNEL) ACTION(REPLACE)
	AMQ8877I: IBM MQ channel authentication record set.
	    10 : 		SET CHLAUTH(*)  TYPE(ADDRESSMAP) ADDRESS(*)  USERSRC(CHANNEL) ACTION(ADD)
	AMQ8877I: IBM MQ channel authentication record set.
	    11 :                 ALTER AUTHINFO('SYSTEM.DEFAULT.AUTHINFO.IDPWOS') AUTHTYPE(IDPWOS) CHCKCLNT(NONE)
	AMQ8567I: IBM MQ authentication information changed.
	    12 : 		ALTER CHANNEL(SYSTEM.ADMIN.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('usrmq')
	AMQ8016I: IBM MQ channel changed.
	    13 : 		ALTER CHANNEL(SYSTEM.DEF.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('usrmq')
	AMQ8016I: IBM MQ channel changed.
	    14 :                 REFRESH SECURITY TYPE(CONNAUTH)
	AMQ8560I: IBM MQ security cache refreshed.
	       : 		
	14 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.COMMAND.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.COMMAND.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.DATA.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.DATA.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.REPLY.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.REPLY.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.STATE.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.STATE.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.EVENT.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.EVENT.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHAGT1.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHAGT1.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHTRN1.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHTRN1.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHOPS1.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHOPS1.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHSCH1.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHSCH1.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHMON1.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHMON1.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHADM1.SRVFSAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHADM1.SRVFSAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.




8.‐ Una vez creados el Qmanager de los agentes básicos, debemos crear las relaciones entre ellos (colas, canales y
listeners), para esto ejecutamos el script: create‐basic‐relations.sh::

	$ ./create-basic-relations.sh 



	Creating Channels for SRVFSAGN
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : 	DEFINE CHANNEL (SRVFSAGN.A.CRC01CRD) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1414)') XMITQ (CRC01CRD)
	AMQ8014I: IBM MQ channel created.
	     2 : 	DEFINE QLOCAL (CRC01CRD) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	       : 
	     3 : 	DEFINE CHANNEL (CRC01CRD.A.SRVFSAGN) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	       : 
	     4 : 	DEFINE CHANNEL (SRVFSAGN.A.CRC01CMM) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1416)') XMITQ (CRC01CMM)
	AMQ8014I: IBM MQ channel created.
	     5 : 	DEFINE QLOCAL (CRC01CMM) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	       : 	
	     6 : 	DEFINE CHANNEL (CRC01CMM.A.SRVFSAGN) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	     7 : 	END
	6 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.



	Creating Channels for CRC01CRD
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : 	DEFINE CHANNEL (CRC01CRD.A.SRVFSAGN) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1418)') XMITQ (SRVFSAGN)
	AMQ8014I: IBM MQ channel created.
	     2 : 	DEFINE QLOCAL (SRVFSAGN) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	       : 
	     3 : 	DEFINE CHANNEL (SRVFSAGN.A.CRC01CRD) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	       : 
	     4 : 	DEFINE CHANNEL (CRC01CRD.A.CRC01CMM) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1416)') XMITQ (CRC01CMM)
	AMQ8014I: IBM MQ channel created.
	     5 : 	DEFINE QLOCAL (CRC01CMM) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	       : 
	     6 : 	DEFINE CHANNEL (CRC01CMM.A.CRC01CRD) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	     7 : 	END
	6 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.



	Creating Channels for CRC01CMM
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CMM.


	     1 : 	DEFINE CHANNEL (CRC01CMM.A.SRVFSAGN) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1418)') XMITQ (SRVFSAGN)
	AMQ8014I: IBM MQ channel created.
	     2 : 	DEFINE QLOCAL (SRVFSAGN) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	       : 
	     3 : 	DEFINE CHANNEL (SRVFSAGN.A.CRC01CMM) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	       : 
	     4 : 	DEFINE CHANNEL (CRC01CMM.A.CRC01CRD) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1414))') XMITQ (CRC01CRD)
	AMQ8014I: IBM MQ channel created.
	     5 : 	DEFINE QLOCAL (CRC01CRD) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	       : 
	     6 : 	DEFINE CHANNEL (CRC01CRD.A.CRC01CMM) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	     7 : 	END
	6 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.

	Stating Channels CRC01CMM
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CMM.


	     1 : 	START CHANNEL (CRC01CMM.A.SRVFSAGN)
	AMQ8018I: Start IBM MQ channel accepted.
	     2 : 	START CHANNEL (CRC01CMM.A.CRC01CRD)
	AMQ8018I: Start IBM MQ channel accepted.
	2 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Stating Channels CRC01CRD
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CMM.


	     1 : 	START CHANNEL (CRC01CRD.A.SRVFSAGN)
	AMQ8227E: Channel CRC01CRD.A.SRVFSAGN not found.
	     2 : 	START CHANNEL (CRC01CRD.A.CRC01CMM)
	AMQ8018I: Start IBM MQ channel accepted.
	       : 
	2 MQSC commands read.
	No commands have a syntax error.
	One valid MQSC command could not be processed.
	Stating Channels SRVFSAGN
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CMM.


	     1 : 	START CHANNEL (SRVFSAGN.A.CRC01CRD)
	AMQ8227E: Channel SRVFSAGN.A.CRC01CRD not found.
	     2 : 	START CHANNEL (SRVFSAGN.A.CRC01CMM)
	AMQ8018I: Start IBM MQ channel accepted.
	       : 
	2 MQSC commands read.
	No commands have a syntax error.
	One valid MQSC command could not be processed.


	END....END..!!!!!!!!!!!!!!

Consultamos para ver como vamos::

	$ dspmq
	QMNAME(QMA)                                               STATUS(Ended unexpectedly)
	QMNAME(QMB)                                               STATUS(Ended unexpectedly)
	QMNAME(CRC01CRD)                                          STATUS(Running)
	QMNAME(CRC01CMM)                                          STATUS(Running)
	QMNAME(SRVFSAGN)                                          STATUS(Running)



9.‐ para crear los agentes debemos listarlos en el archivo agents.lst, el mismo debe contener nombre del qmanager
agente, Descripción (sin espacios en blanco) y el número del puerto. Se muestra un ejemplo::

	$ cat agents.lst 
	##Este es la lista de agentes para MQ FTE
	# Si este archivo no existe los camando de creación no se ejecutan.
	# El formato debe ser XXX:YYY:ZZZ, donde:
	# WWW = Nombre del Agente
	# XXX = Descripción (El nombre no debe contener espacios en blanco)
	# YYY = Puerto
	# ZZZ = Nombre del Agente
	#
	# WWW:XXX:YYY:ZZZ
	#
	#BNSCNTAGN:BANESCO_NAIGUATA:8104:BNSCNTAGN.AG
	#PLTCNTAGN:PLATCO_NAIGUATA:8204:PLTCNTAGN.AG
	#MERNTAGN:MERCANTIL_NAIGUATA:8304:MERNTAGN.AG
	#PROVNTAGN:PROVINCIAL_NAIGUATA:8404:PROVNTAGN.AG
	#BNCNTAGN:BNC_NAIGUATA:8504:BNCNTAGN.AG
	#TREDNTAGN:TRANRED_NAIGUATA:8604:TREDNTAGN.AG
	#BDVNTAGN:BDV_NAIGUATA:8704:BDVNTAGN.AG
	#BCRBNTAGN:BANCARIBE_NAIGUATA:8804:BCRBNTAGN.AG
	#BODNTAGN:BOD_NAIGUATA:8904:BODNTAGN.AG
	#BTESNTAGN:BANCO_TESORO_NAIGUATA:9004:BTESNTAGN.AG
	#BEXTNTAGN:BANCO_EXTERIOR:9104:BTESNTAGN.AG
	#BDSNTAGN:BANCO_DEL_SUR_NAIGUATA:9204:BDSNTAGN.AG
	#BVDCNTAGN:BANCO_VENEZOLANO_CREDITO_NAIGUATA:9304:BVDCNTAGN.AG
	#CTBKNTAGN:CITIBANK_NAIGUATA:9404:CTBKNTAGN.AG
	##BSFTNTAGN:BANCO_SOFITASA_NAIGUATA:9504:BSFTNTAGN.AG
	#BAVNTAGN:BANCO_AGRICOLA_NAIGUATA:9604:BAVNTAGN.AG
	#BBPNTAGN:BANCO_BICENTENARIO:9704:BBPNTAGN.AG
	#BANFNTAGN:BANCO_BANFANB:9804:BANFNTAGN.AG
	#CBKNTAGN:CBK_NAIGUATA:2420:CBKNTAGN.AG
	#APPFS01NTAGN:W12APPFS01_NAI:2422:APPFS01NTAGN.AG
	#FSNG01AGN:W12APPFS01_NAI:2424:FSNG01AGN.AG
	BNC2NTAGN:BNC2_NAIGUATA:9904:BNC2NTAGN.AG

10.‐ Una vez organizada la información en el archivo agents.lst, debemos ejecutar el script create-Qmanager.sh, este se encarga de crear toda las definición del qmanager y las relaciones con el coordinator, commander y el qmanager del agente del as400, una vez finalizado esta actividad, hace un llamado al script agent_def.sh para realizar toda la configuración referente a las colas que se necesitan para la transferencia de archivo::

	$ ./create-Qmanager.sh 
	IBM MQ queue manager created.
	Directory '/var/mqm/qmgrs/BNC2NTAGN' created.
	The queue manager is associated with installation 'Installation1'.
	Creating or replacing default objects for queue manager 'BNC2NTAGN'.
	Default objects statistics : 84 created. 0 replaced. 0 failed.
	Completing setup.
	Setup completed.
	IBM MQ queue manager 'BNC2NTAGN' starting.
	The queue manager is associated with installation 'Installation1'.
	5 log records accessed on queue manager 'BNC2NTAGN' during the log replay phase.
	Log replay for queue manager 'BNC2NTAGN' complete.
	Transaction manager state recovered for queue manager 'BNC2NTAGN'.
	IBM MQ queue manager 'BNC2NTAGN' started using V9.1.0.0.
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : 			DEFINE LISTENER (BNC2NTAGN.LST) TRPTYPE (TCP) CONTROL (QMGR) PORT (9904)
	AMQ8626I: IBM MQ listener created.
	     2 : 			START LISTENER (BNC2NTAGN.LST)
	AMQ8021I: Request to start IBM MQ listener accepted.
	     3 : 			DEFINE CHANNEL (SYSTEM.ADMIN.SVRCONN) CHLTYPE (SVRCONN)
	AMQ8014I: IBM MQ channel created.
	     4 : 			START CHANNEL (SYSTEM.ADMIN.SVRCONN)
	AMQ8018I: Start IBM MQ channel accepted.
	     5 : 			DEFINE QLOCAL (BNC2NTAGN.DQ) USAGE (NORMAL)
	AMQ8006I: IBM MQ queue created.
	     6 : 			ALTER QMGR DEADQ(BNC2NTAGN.DQ)
	AMQ8005I: IBM MQ queue manager changed.
	     7 : 			ALTER QMGR  CHLAUTH(DISABLED)
	AMQ8005I: IBM MQ queue manager changed.
	     8 : 	                SET CHLAUTH(*)  TYPE(BLOCKUSER) USERLIST(*MQADMIN) ACTION(REMOVE)
	AMQ8877I: IBM MQ channel authentication record set.
	     9 :         	        SET CHLAUTH(*)  TYPE(ADDRESSMAP) ADDRESS(*)  USERSRC(CHANNEL) ACTION(ADD)
	AMQ8877I: IBM MQ channel authentication record set.
	    10 : 			SET CHLAUTH(SYSTEM.*) TYPE(ADDRESSMAP) ADDRESS(*) USERSRC(CHANNEL) ACTION(REPLACE)
	AMQ8877I: IBM MQ channel authentication record set.
	    11 : 	                ALTER AUTHINFO('SYSTEM.DEFAULT.AUTHINFO.IDPWOS') AUTHTYPE(IDPWOS) CHCKCLNT(NONE)
	AMQ8567I: IBM MQ authentication information changed.
	    12 : 			ALTER CHANNEL(SYSTEM.ADMIN.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('usrmq')
	AMQ8016I: IBM MQ channel changed.
	    13 : 			ALTER CHANNEL(SYSTEM.DEF.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('usrmq')
	AMQ8016I: IBM MQ channel changed.
	    14 :         	        REFRESH SECURITY TYPE(CONNAUTH)
	AMQ8560I: IBM MQ security cache refreshed.
	       : 
	       : 
	       : 
	    15 : 			DEFINE CHANNEL (BNC2NTAGN.A.CRC01CRD) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1414)') XMITQ (CRC01CRD)
	AMQ8014I: IBM MQ channel created.
	    16 : 			DEFINE CHANNEL (CRC01CRD.A.BNC2NTAGN) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	    17 : 			DEFINE QLOCAL (CRC01CRD) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	       : 
	    18 : 			DEFINE CHANNEL (BNC2NTAGN.A.CRC01CMM) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1416)') XMITQ (CRC01CMM)
	AMQ8014I: IBM MQ channel created.
	    19 : 			DEFINE CHANNEL (CRC01CMM.A.BNC2NTAGN) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	    20 : 			DEFINE QLOCAL (CRC01CMM) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	       : 
	    21 : 			DEFINE CHANNEL (BNC2NTAGN.A.SRVFSAGN) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(1418)') XMITQ (SRVFSAGN)
	AMQ8014I: IBM MQ channel created.
	    22 : 			DEFINE CHANNEL (SRVFSAGN.A.BNC2NTAGN) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	    23 : 			DEFINE QLOCAL (SRVFSAGN) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	    24 : 			END
	23 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.




	Definir qmanager en el coordinator
	Creando definiciones en el COORDINATOR (CRC01CRD) para el agente BNC2NTAGN
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : 		DEFINE CHANNEL (CRC01CRD.A.BNC2NTAGN) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(9904)') XMITQ (BNC2NTAGN)
	AMQ8014I: IBM MQ channel created.
	     2 : 		DEFINE QLOCAL (BNC2NTAGN) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	     3 : 		DEFINE CHANNEL (BNC2NTAGN.A.CRC01CRD) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	     4 : 		END
	3 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.




	Definir qmanager en el commander
	Creando definiciones en el COMMANDER (CRC01CMM) para el agente BNC2NTAGN
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CMM.


	     1 : 		DEFINE CHANNEL (CRC01CMM.A.BNC2NTAGN) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(9904)') XMITQ (BNC2NTAGN)
	AMQ8014I: IBM MQ channel created.
	     2 : 		DEFINE QLOCAL (BNC2NTAGN) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	     3 : 		DEFINE CHANNEL (BNC2NTAGN.A.CRC01CMM) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	     4 : 		END
	3 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.




	Creando definiciones en el SRVFS (SRVFSAGN) para el agente BNC2NTAGN
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager SRVFSAGN.


	     1 : 		DEFINE CHANNEL (SRVFSAGN.A.BNC2NTAGN) CHLTYPE (SDR) DISCINT(0) CONNAME ('mq-server(9904)') XMITQ (BNC2NTAGN)
	AMQ8014I: IBM MQ channel created.
	     2 : 		DEFINE QLOCAL (BNC2NTAGN) USAGE (XMITQ)
	AMQ8006I: IBM MQ queue created.
	     3 : 		DEFINE CHANNEL (BNC2NTAGN.A.SRVFSAGN) CHLTYPE (RCVR)
	AMQ8014I: IBM MQ channel created.
	     4 : 		END
	3 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	########################################################################################
	#Llamando a la deficion para las colas de FTE                                          #
	########################################################################################
	Creando QLOCAL: SYSTEM.FTE.COMMAND.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.COMMAND.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.DATA.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.DATA.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.REPLY.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.REPLY.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.STATE.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.STATE.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.EVENT.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.EVENT.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHAGT1.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHAGT1.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHTRN1.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHTRN1.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHOPS1.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHOPS1.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHSCH1.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHSCH1.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHMON1.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHMON1.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	Creando QLOCAL: SYSTEM.FTE.AUTHADM1.BNC2NTAGN.AG
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager BNC2NTAGN.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.AUTHADM1.BNC2NTAGN.AG) DEFPRTY(0) DEFSOPT(SHARED) GET(ENABLED) MAXDEPTH(5000) 	MAXMSGL(4194304) MSGDLVSQ(PRIORITY) PUT(ENABLED) RETINTVL(999999999) SHARE NOTRIGGER USAGE(NORMAL) REPLACE 
	AMQ8006I: IBM MQ queue created.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.


Consultamos ::

	$ dspmq -all
	QMNAME(CRC01CRD)                                          STATUS(Running)
	    TRPTYPE(TCP) PID(1393) IPADDR() PORT(1414) BACKLOG(100)
	QMNAME(CRC01CMM)                                          STATUS(Running)
	    TRPTYPE(TCP) PID(1659) IPADDR() PORT(1416) BACKLOG(100)
	QMNAME(SRVFSAGN)                                          STATUS(Running)
	    TRPTYPE(TCP) PID(2106) IPADDR() PORT(1418) BACKLOG(100)
	QMNAME(BNC2NTAGN)                                         STATUS(Running)
	    TRPTYPE(TCP) PID(3478) IPADDR() PORT(9904) BACKLOG(100)

Creación y Configuración de File Logger
+++++++++++++++++++++++++++++++++++++++

1.‐ Ejecutar el comando fteCreateLogger para crear el archivo con la definición de las colas para el COORDINATOR::

	$ fteCreateLogger -loggerType FILE -fileLoggerMode CIRCULAR -fileSize 50MB -fileCount 10 filelogger1
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCL0426I: Direct the following MQSC definitions for logger 'FILELOGGER1' to queue manager 'CRC01CRD'.

	DEFINE QLOCAL(SYSTEM.FTE.LOG.RJCT.FILELOGGER1) +
	 DESCR('Messages rejected by the FTE logger.') +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(999999999) +
	 MAXMSGL(4194304) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.LOG.CMD.FILELOGGER1) +
	 DESCR('Command messages to control the FTE logger.') +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(999999999) +
	 MAXMSGL(4194304) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(5000) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE


	BFGCL0424I: A file has been created containing the MQSC definitions to create your logger. The file can be found here: '/var/mqm/mqft/config/CRC01CRD/loggers/FILELOGGER1/FILELOGGER1_create.mqsc'.
	BFGCL0425I: A file has been created containing the MQSC definitions to delete your logger. The file can be found here: '/var/mqm/mqft/config/CRC01CRD/loggers/FILELOGGER1/FILELOGGER1_delete.mqsc'.
	BFGCL0415I: Logger configured successfully.


2.‐ El comando anterior genera un archivo el cual debemos ejecutarlo sobre el COORDINATOR::

	$ runmqsc $COORDINATOR < /var/mqm/mqft/config/CRC01CRD/loggers/FILELOGGER1/FILELOGGER1_create.mqsc
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : DEFINE QLOCAL(SYSTEM.FTE.LOG.RJCT.FILELOGGER1) +
	       :  DESCR('Messages rejected by the FTE logger.') +
	       :  DEFPRTY(0) +
	       :  DEFSOPT(SHARED) +
	       :  GET(ENABLED) +
	       :  MAXDEPTH(999999999) +
	       :  MAXMSGL(4194304) +
	       :  MSGDLVSQ(PRIORITY) +
	       :  PUT(ENABLED) +
	       :  RETINTVL(999999999) +
	       :  SHARE +
	       :  NOTRIGGER +
	       :  USAGE(NORMAL) +
	       :  REPLACE
	AMQ8006I: IBM MQ queue created.
	     2 : DEFINE QLOCAL(SYSTEM.FTE.LOG.CMD.FILELOGGER1) +
	       :  DESCR('Command messages to control the FTE logger.') +
	       :  DEFPRTY(0) +
	       :  DEFSOPT(SHARED) +
	       :  GET(ENABLED) +
	       :  MAXDEPTH(999999999) +
	       :  MAXMSGL(4194304) +
	       :  MSGDLVSQ(PRIORITY) +
	       :  PUT(ENABLED) +
	       :  RETINTVL(5000) +
	       :  SHARE +
	       :  NOTRIGGER +
	       :  USAGE(NORMAL) +
	       :  REPLACE
	AMQ8006I: IBM MQ queue created.
	2 MQSC commands read.
	No commands have a syntax error.
	All valid MQSC commands were processed.


3.‐ Iniciamos el Looger::

	$ fteStartLogger filelogger1
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCL0287I: The request to start the logger on this machine has been submitted.
	BFGCL0526I: Logger log files located at: /var/mqm/mqft/logs/CRC01CRD/loggers/FILELOGGER1/logs

Los archivos de logs lo podemos encontrar en la siguiente ruta::

	$ ls -l /var/mqm/mqft/logs/CRC01CRD/loggers/FILELOGGER1
	total 12
	-rw------- 1 mqm mqm  53 Sep  6 17:49 FILELOGGER10-20220906174950388.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER11-20220906174950388.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER12-20220906174950388.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER13-20220906174950388.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER14-20220906174950389.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER15-20220906174950389.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER16-20220906174950389.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER17-20220906174950389.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER18-20220906174950389.log
	-rw------- 1 mqm mqm   0 Sep  6 17:49 FILELOGGER19-20220906174950389.log
	-rw-rw-r-- 1 mqm mqm   0 Sep  6 17:49 logger.lck
	-rw-rw-r-- 1 mqm mqm   4 Sep  6 17:49 logger.pid
	drwxrwsrwx 2 mqm mqm 122 Sep  6 17:49 logs
	-rw-rw-rw- 1 mqm mqm   0 Sep  6 17:49 mqmftpc.lck
	-rw-rw-rw- 1 mqm mqm   4 Sep  6 17:49 mqmftpc.pid

Hacemos unas verificaciones::

	$ ps -ef | grep mqm

	$ netstat -nat | grep -i listen
	tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN     
	tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     
	tcp6       0      0 ::1:25                  :::*                    LISTEN     
	tcp6       0      0 :::1414                 :::*                    LISTEN     
	tcp6       0      0 :::1416                 :::*                    LISTEN     
	tcp6       0      0 :::1418                 :::*                    LISTEN     
	tcp6       0      0 :::9904                 :::*                    LISTEN     
	tcp6       0      0 :::22                   :::*                    LISTEN 




Creado el:
2014‐10‐02 13:27
Autor:
Nelson R. Perez

Última actualización:
2022-09-06 11:55
Mantenedor:
Carlos Gómez

