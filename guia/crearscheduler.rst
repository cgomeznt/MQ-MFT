Crear Supervisores
=====================

Help::

	fteCreateTransfer  [-p ConfigurationOptions] [-w [timeout]]
		               -sa AgentName [-sm QueueManager]
		               -da AgentName [-dm QueueManager]
		               [-td TransferDefinitionFile]
		               [-gt XMLOutputFile]
		               ([-ss startSchedule] [-tb timeBase]
		               [-oi occurrenceInterval] [-of occurrenceFrequency]
		               [-oc occurrenceCount] | [-es endSchedule])
		               ([-tr triggerSpec ] [-tl])
		               [-jn jobName] [-md metaData] [-cs ChecksumMethod]
		               [-pr <priority>]
		               [-sce <encoding>] [-dce <encoding>] [-dle <line-ending>]
		               [-dtr]
		               [-qmp <true/false>] [-qi]
		               [-presrc <preSourceCall>] [-predst <preDestinationCall>]
		               [-postsrc <postSourceCall>]
		               [-postdst <postDestinationCall>]
		               ([-df File] | [-dd Directory] |
		               [-ds SequentialDataset] | [-dp PartitionedDataset] |
		               [-dq Queue[@QueueManager]] | [-du fileSpaceName])
		               ([-qs <size>] | [-dqdb <delimiter>] | [-dqdt <pattern>])
		               [-dqdp <prefix/postfix>] [-dfa <attributes>]
		               [-de <action>] [-t TransferMode] [-dqp <true/false>]
		               [-sd <disposition>] [-r]
		               [-sq] [-sqgi] [-sqwt]
		               ([-sqdb <delimiter>] | [-sqdt <string>])
		               [-sqdp <prefix/postfix>]
		               [-srdb <delimiter> [-srdp <prefix/postfix>]]
		               [-skeep]
		               [-mquserid <user>] [-mqpassword <password>]
		               [-rt <transfer recovery timeout>]
		               SourceFileSpec...

Esta es la forma de crear un Scheduler desde un archivo en formato xml que ya tenga la información, es decir, previo con fteListSchedulerTranfer se crearon estos archivos::


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

