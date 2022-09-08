Montar un servidor MQ

En un servidor hacer la instalación del Agente Principal.

En el mismo servidor en donde se instalo el Agente Principal, configurar otro Agente como secundario.

Asumimos que los agentes estaran instalados en un mismo servidor, crear una estructura de carpeta para cada agente::

	#  mkdir -p /opt/SRVFSAGN.AG/{ENTRADA,SALIDA}
	#  mkdir -p /opt/BNC2NTAGN.AG/{ENTRADA,SALIDA}

	# touch /opt/SRVFSAGN.AG/SALIDA/SRVFSAGN.to.BNC2NTAGN
	# touch /opt/BNC2NTAGN.AG/SALIDA/BNC2NTAGN.to.SRVFSAGN

	# chown -R mqm. /opt/BNC2NTAGN.AG
	# chown -R mqm. /opt/SRVFSAGN.AG/

Capturar en el Servidor MQ MFT el LOG::

	$ tail -f FILELOGGER10-20220906174950388.log


Realizar una transferencia desde el agente SRVFSAGN.AG hacia el agente BNC2NTAGN.AG. En este ejemplo, los archivos que estén en "/opt/SRVFSAGN.AG/SALIDA/*" serán transferidos del Agente SRVFSAGN.AG hacia el agente BNC2NTAGN.AG en la carpeta "/opt/BNC2NTAGN.AG/ENTRADA/"::


	$ fteCreateTransfer -sa SRVFSAGN.AG -sm SRVFSAGN  -da BNC2NTAGN.AG  -dm BNC2NTAGN -de overwrite -dd /opt/BNC2NTAGN.AG/ENTRADA/ /opt/SRVFSAGN.AG/SALIDA/*

Esta es la salida del comando ejecutado::

	$ fteCreateTransfer -sa SRVFSAGN.AG -sm SRVFSAGN  -da BNC2NTAGN.AG  -dm BNC2NTAGN -de overwrite -dd /opt/BNC2NTAGN.AG/ENTRADA/ /opt/SRVFSAGN.AG/SALIDA/*
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	BFGCL0035I: Transfer request issued.  The request ID is: 414d51204352433031434d4d20202020e9e5186307b8da24
	BFGCL0182I: The request is now waiting to be processed by the agent.


Esto es lo que se ve en el LOG luego de hacer la transferencia::

	2022-09-07T21:07:17;414d51204352433031434d4d20202020e9e5186307b8da24;[TSTR];   ;SRVFSAGN.AG;SRVFSAGN;STANDARD;BNC2NTAGN.AG;BNC2NTAGN;mqm;;;com.ibm.wmqfte.SourceAgent=SRVFSAGN.AG, com.ibm.wmqfte.DestinationAgent=BNC2NTAGN.AG, com.ibm.wmqfte.MqmdUser=usrmq, com.ibm.wmqfte.OriginatingUser=mqm, com.ibm.wmqfte.OriginatingHost=192.168.1.10, com.ibm.wmqfte.TransferId=414d51204352433031434d4d20202020e9e5186307b8da24, com.ibm.wmqfte.Priority=0;
	2022-09-07T21:07:17;414d51204352433031434d4d20202020e9e5186307b8da24;[TPRO];0  ;/opt/SRVFSAGN.AG/SALIDA/SRVFSAGN.to.BNC2NTAGN;0;file;leave ;;;;;;/opt/BNC2NTAGN.AG/ENTRADA/SRVFSAGN.to.BNC2NTAGN;0;file;overwrite;;;;;;;;
	2022-09-07T21:07:17;414d51204352433031434d4d20202020e9e5186307b8da24;[TCOM];0  ;SRVFSAGN.AG;SRVFSAGN;STANDARD;BNC2NTAGN.AG;BNC2NTAGN;STANDARD;mqm;;BFGRP0032I: The file transfer request has successfully completed.;com.ibm.wmqfte.SourceAgent=SRVFSAGN.AG, com.ibm.wmqfte.DestinationAgent=BNC2NTAGN.AG, com.ibm.wmqfte.MqmdUser=usrmq, com.ibm.wmqfte.OriginatingUser=mqm, com.ibm.wmqfte.OriginatingHost=192.168.1.10, com.ibm.wmqfte.TransferId=414d51204352433031434d4d20202020e9e5186307b8da24, com.ibm.wmqfte.Priority=0;


Otro ejemplo: El archivo que está en "/opt/SRVFSAGN.AG/SALIDA/SRVFSAGN.to.BNC2NTAGN" será transferido del Agente SRVFSAGN.AG hacia el agente BNC2NTAGN.AG en la carpeta y se renombrara "/opt/BNC2NTAGN.AG/ENTRADA/PROCESAR.TXT"::

	$ fteCreateTransfer -sa SRVFSAGN.AG -sm SRVFSAGN  -da BNC2NTAGN.AG  -dm BNC2NTAGN -de overwrite -df /opt/BNC2NTAGN.AG/ENTRADA/PROCESAR.TXT /opt/SRVFSAGN.AG/SALIDA/SRVFSAGN.to.BNC2NTAGN

Esta es la salida del comando ejecutado::

	$ fteCreateTransfer -sa SRVFSAGN.AG -sm SRVFSAGN  -da BNC2NTAGN.AG  -dm BNC2NTAGN -de overwrite -df /opt/BNC2NTAGN.AG/ENTRADA/PROCESAR.TXT /opt/SRVFSAGN.AG/SALIDA/SRVFSAGN.to.BNC2NTAGN
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	BFGCL0035I: Transfer request issued.  The request ID is: 414d51204352433031434d4d20202020e9e5186303bcda24
	BFGCL0182I: The request is now waiting to be processed by the agent.


Esto es lo que se ve en el LOG luego de hacer la transferencia::

	2022-09-07T21:21:17;414d51204352433031434d4d20202020e9e5186303bcda24;[TSTR];   ;SRVFSAGN.AG;SRVFSAGN;STANDARD;BNC2NTAGN.AG;BNC2NTAGN;mqm;;;com.ibm.wmqfte.SourceAgent=SRVFSAGN.AG, com.ibm.wmqfte.DestinationAgent=BNC2NTAGN.AG, com.ibm.wmqfte.MqmdUser=usrmq, com.ibm.wmqfte.OriginatingUser=mqm, com.ibm.wmqfte.OriginatingHost=192.168.1.10, com.ibm.wmqfte.TransferId=414d51204352433031434d4d20202020e9e5186303bcda24, com.ibm.wmqfte.Priority=0;
	2022-09-07T21:21:17;414d51204352433031434d4d20202020e9e5186303bcda24;[TPRO];0  ;/opt/SRVFSAGN.AG/SALIDA/SRVFSAGN.to.BNC2NTAGN;0;file;leave ;;;;;;/opt/BNC2NTAGN.AG/ENTRADA/PROCESAR.TXT;0;file;overwrite;;;;;;;;
	2022-09-07T21:21:17;414d51204352433031434d4d20202020e9e5186303bcda24;[TCOM];0  ;SRVFSAGN.AG;SRVFSAGN;STANDARD;BNC2NTAGN.AG;BNC2NTAGN;STANDARD;mqm;;BFGRP0032I: The file transfer request has successfully completed.;com.ibm.wmqfte.SourceAgent=SRVFSAGN.AG, com.ibm.wmqfte.DestinationAgent=BNC2NTAGN.AG, com.ibm.wmqfte.MqmdUser=usrmq, com.ibm.wmqfte.OriginatingUser=mqm, com.ibm.wmqfte.OriginatingHost=192.168.1.10, com.ibm.wmqfte.TransferId=414d51204352433031434d4d20202020e9e5186303bcda24, com.ibm.wmqfte.Priority=0;

