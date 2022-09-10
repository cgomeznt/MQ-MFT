Eliminar Supervisores
=========================

Help::

	fteDeleteScheduledTransfer [-p <configurationOptions>] [-m <queueManager>]
		                       [-mquserid <user>] [-mqpassword <password>]
		                       -agentName <agentName> ScheduleID


Debe conocer el Schedule Identifier y eso se obtiene con fteListSchedulerTransfer::

	Schedule Identifier:        1

Este es el comando::

	$ fteDeleteScheduledTransfer 1


Cuando se elimine se vera en el log::

	2022-09-09T22:16:14;414d51204352433031434d4d20202020489f1b6303561022;[MACT];0  ;SETTLEMENT_TDD_MAESTRO_0105;SRVFSAGN.AG;SRVFSAGN;stop;
	2022-09-09T22:16:14;414d51204352433031434d4d20202020489f1b6303561022;[MACT];0  ;SETTLEMENT_TDD_MAESTRO_0105;SRVFSAGN.AG;SRVFSAGN;delete;


**NOTA** para poder eliminar un Scheduler el Agente debe estar en On Line.
