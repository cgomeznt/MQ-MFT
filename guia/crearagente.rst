Crear un Agente
=================


Ejecutamos el siguiente comando para crear el Coordinator::

	$ fteSetupCoordination -coordinationQMgr CRC01CRD -coordinationQMgrHost 192.168.1.110 -coordinationQMgrPort 1414 -coordinationQMgrChannel SYSTEM.DEF.SVRCONN

Ejecutamos el siguiente comando para crear el Commander::

	$ fteSetupCommands -connectionQMgr CRC01CMM -connectionQMgrHost 192.168.1.110 -connectionQMgrPort 1416 -connectionQMgrChannel SYSTEM.DEF.SVRCONNcrearagente.rst


Ejecutamos el siguiente comando para crear el agente:: 

	$ fteCreateAgent -agentName CRC06AGN.AG -agentQMgr CRC06AGN.QM -agentQMgrHost 192.168.1.110 -agentQMgrPort 1424 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "Agent de Prueba para el Qmanager CRC06AGN.QM"

Comandos para Iniciar, Detener o Eliminar un agente::

	fteStartAgent CRC06AGN.AG

	fteStopAgent CRC06AGN.AG

	fteDeleteAgent CRC06AGN.AG


Comandos ejecutados y sus salidas
+++++++

::

	$ fteSetupCoordination -coordinationQMgr CRC01CRD -coordinationQMgrHost 192.168.1.110 -coordinationQMgrPort 1414 -coordinationQMgrChannel SYSTEM.DEF.SVRCONN
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


$ fteSetupCommands -connectionQMgr CRC01CMM -connectionQMgrHost 192.168.1.110 -connectionQMgrPort 1416 -connectionQMgrChannel SYSTEM.DEF.SVRCONN
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCL0245I: The file '/var/mqm/mqft/config/CRC01CRD/command.properties' has been created successfully.




	$ fteCreateAgent -agentName CRC06AGN.AG -agentQMgr CRC06AGN.QM -agentQMgrHost 192.168.1.110 -agentQMgrPort 1424 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "Agent de Prueba para el Qmanager CRC06AGN.QM"
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCM0238I: Direct the following MQSC definitions for agent 'CRC06AGN.AG' to queue manager 'CRC06AGN.QM'.

	DEFINE QLOCAL(SYSTEM.FTE.COMMAND.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(5000) +
	 MAXMSGL(4194304) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.DATA.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(5000) +
	 MAXMSGL(4194304) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.REPLY.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(5000) +
	 MAXMSGL(4194304) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.STATE.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(5000) +
	 MAXMSGL(4194304) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.EVENT.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(5000) +
	 MAXMSGL(4194304) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.AUTHAGT1.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(0) +
	 MAXMSGL(0) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.AUTHTRN1.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(0) +
	 MAXMSGL(0) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.AUTHOPS1.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(0) +
	 MAXMSGL(0) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.AUTHSCH1.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(0) +
	 MAXMSGL(0) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.AUTHMON1.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(0) +
	 MAXMSGL(0) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE
	DEFINE QLOCAL(SYSTEM.FTE.AUTHADM1.CRC06AGN.AG) +
	 DEFPRTY(0) +
	 DEFSOPT(SHARED) +
	 GET(ENABLED) +
	 MAXDEPTH(0) +
	 MAXMSGL(0) +
	 MSGDLVSQ(PRIORITY) +
	 PUT(ENABLED) +
	 RETINTVL(999999999) +
	 SHARE +
	 NOTRIGGER +
	 USAGE(NORMAL) +
	 REPLACE


	BFGCM0239I: A file has been created containing the MQSC definitions to define the agent CRC06AGN.AG. The file can be found here: '/var/mqm/mqft/config/CRC01CRD/agents/CRC06AGN.AG/CRC06AGN.AG_create.mqsc'.
	BFGCM0241I: A file has been created containing the MQSC definitions to delete the agent CRC06AGN.AG. The file can be found here: '/var/mqm/mqft/config/CRC01CRD/agents/CRC06AGN.AG/CRC06AGN.AG_delete.mqsc'.
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	BFGMQ1041E:  An attempt to connect to queue manager 'CRC06AGN.QM' with user ID 'mqm' has been rejected because of invalid authentication details. Valid user ID and password details must be supplied in the credentials file.
	BFGCL0254I: Agent configured successfully. The agent has not been registered with the coordination queue manager.



	$ fteStartAgent CRC06AGN.AG
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCL0030I: The request to start agent 'CRC06AGN.AG' on this machine has been submitted.
	BFGCL0031I: Agent log files located at: /var/mqm/mqft/logs/CRC01CRD/agents/CRC06AGN.AG/logs


	$ fteStopAgent CRC06AGN.AG
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	BFGCL0468I: Issuing stop request to agent 'SRVFSAGN.AG'. The command will wait for the agent to stop. The agent will stop only when all current transfers have completed.
	BFGCL0553I: The agent has processed the stop request and will end when all current transfers have completed.



	$ fteDeleteAgent CRC06AGN.AG
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	BFGCL0092I: Use the following MQSC commands to clear and delete the agent's queues on queue manager 'CRC06AGN.QM'.
	CLEAR QLOCAL(SYSTEM.FTE.COMMAND.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.COMMAND.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.DATA.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.DATA.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.REPLY.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.REPLY.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.STATE.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.STATE.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.EVENT.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.EVENT.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.AUTHAGT1.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.AUTHAGT1.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.AUTHTRN1.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.AUTHTRN1.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.AUTHOPS1.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.AUTHOPS1.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.AUTHSCH1.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.AUTHSCH1.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.AUTHMON1.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.AUTHMON1.CRC06AGN.AG)
	CLEAR QLOCAL(SYSTEM.FTE.AUTHADM1.CRC06AGN.AG)
	DELETE QLOCAL(SYSTEM.FTE.AUTHADM1.CRC06AGN.AG)
	BFGCL0061E: There was a problem connecting to IBM MQ. The reason code was: '2035'.




