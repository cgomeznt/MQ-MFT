Crear Supervisores
=====================

Help::

	Syntax:
	    fteCreateMonitor  [-p <configurationOptions>]
		               -ma <agentName> [-mm <agentQueueManager>]
		              (-md <directory> | -mq <queue>)
		               -mn <monitorName>
		               -mt <taskFileName>
		              [-pi <pollInterval>]
		              [-pt wildcard|regex]
		              [-pu <pollUnits>]
		              [-rl <recursionevel>]
		              [-bs <maximumBatchSize>]
		              [-tr <triggerCondition>]
		              [-tc] [-tcr <pattern>] [-tcc srcDest|destSrc]
		              [-x  <excludePattern>]
		              [-mmd <monitor metaData>]
		              [-dv <substitutionVariableDefaultValues>]
		              [-ix <filename>] [-ox <filename>]
		              [-mquserid <user>] [-mqpassword <password>]
		              [-f] [-c]

Esta es la forma de crear un supervisor desde un archivo en formato xml que ya tenga la información, es decir, previo con fteListMonitor se crearon estos archivos::


	$ fteCreateMonitor -ma SRVFSAGN.AG -mm SRVFSAGN -ix SETTLEMENT_TDD_MAESTRO_0105.txt


Consultamos::

	$ fteListMonitors 
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	Agent Name:     Monitor Name:                   Resource Type:    
	SRVFSAGN.AG     SETTLEMENT_TDD_MAESTRO_0105     Directory        


Cuando se cree el Supervisor o Monitor se debe ver en el LOG::

	2022-09-09T22:07:05;414d51204352433031434d4d20202020489f1b6303551022;[MCRT];SETTLEMENT_TDD_MAESTRO_0105;SRVFSAGN.AG;SRVFSAGN;create;
	2022-09-09T22:07:05;414d51204352433031434d4d20202020489f1b6303551022;[MACT];0  ;SETTLEMENT_TDD_MAESTRO_0105;SRVFSAGN.AG;SRVFSAGN;start;

