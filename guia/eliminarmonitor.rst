Eliminar Supervisores
=========================

Help::

	Syntax:
	    fteDeleteMonitor   [-p <configurationOptions>] [-mm <queueManager>]
		               [-mquserid <user>] [-mqpassword <password>]
		               -ma <agentName>
		               -mn <monitorName>

Este es el comando::

	$ fteDeleteMonitor -mm SRVFSAGN -ma SRVFSAGN.AG -mn SRVFSAGN -mn SETTLEMENT_TDD_MAESTRO_0105


::

	$ fteDeleteMonitor -mm SRVFSAGN -ma SRVFSAGN.AG -mn SRVFSAGN -mn SETTLEMENT_TDD_MAESTRO_0105
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	BFGCL0192I: A request to delete monitor SETTLEMENT_TDD_MAESTRO_0105 has been issued.
	BFGCL0251I: The request has successfully completed.


Cuando se elimine se vera en el log::

	2022-09-09T22:16:14;414d51204352433031434d4d20202020489f1b6303561022;[MACT];0  ;SETTLEMENT_TDD_MAESTRO_0105;SRVFSAGN.AG;SRVFSAGN;stop;
	2022-09-09T22:16:14;414d51204352433031434d4d20202020489f1b6303561022;[MACT];0  ;SETTLEMENT_TDD_MAESTRO_0105;SRVFSAGN.AG;SRVFSAGN;delete;


**NOTA** para poder eliminar un Supervisor o Monitor el Agente debe estar en On Line.
