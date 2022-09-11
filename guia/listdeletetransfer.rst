Listar y Limpiar las transferencias acumuladas
======================================


Primero se debe identificar en el Agente cuales son las transferencias que tiene acumuladas::



	$ fteShowAgentDetails -v SRVFSAGN.AG
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	Agent Information:
	    Name:                             SRVFSAGN.AG
	    Type:                             Standard
	    Description:                      Agent Principal SRVFSAGN
	    Operating System:                 Linux
	    Host Name:                        srvfsagn
	    Time Zone:                        Eastern Standard Time
	    Product Version:                  9.1.0.0
	    Build Level:                      p910-L180705
	    Trace Level:                      No trace specified
	    Trace FFDC:                       No FFDC specified

	Agent Controller Information:
	    Controller Type:                  MQMFT Process Controller
	    Status:                           UNKNOWN
	    Status Details:                   Information about the agent controller is
		                              not available. Possible reasons are: (1) 
		                              the agent is not running  (2) the agent 
		                              is running on a different system. (3) the
		                              agent is started by a different user.
	    Agent Restarts within Interval:   0
	    Total Agent Restart Count:        0

	Agent Availability Information:
	    Status:                           ACTIVE
	    Status Age:                       0:00:23
	    Status Details:                   The agent is running and is publishing 
		                              its status at regular intervals. The last
		                              update was received within the expected 
		                              time period. The agent is currently 
		                              processing one or more transfers.
	    Start Time:                       2022-09-10T17:55:35Z

	Queue Manager Information:
	    Name:                             SRVFSAGN
	    Transport:                        Client
	    Host:                             192.168.1.110
	    Port:                             1418
	    Channel:                          SYSTEM.DEF.SVRCONN
	    Last Status Reported:             UNKNOWN
	    Status Details:                   Information about the queue manager is 
		                              not available because the agent has a 
		                              client connection to the queue  manager.

	Maximum Number of Running Source Transfers: 25
	Maximum Number of Queued Source Transfers: 1000
	Source Transfer States:
	    TransferId                                          State
	    414d5120535256465341474e202020204bcf1c6303ac7023    started

	Maximum Number of Running Destination Transfers: 25
	Destination Transfer States:
	    No current transfers


AL ver cuales son los ID de las transferencias pendientes en Source Transfer State, las podemos cancelar::

	$ fteCancelTransfer -m SRVFSAGN -a SRVFSAGN.AG 414d5120535256465341474e202020204bcf1c6303ac7023
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	BFGCL0137I: The request to cancel transfer '414D5120535256465341474E202020204BCF1C6303AC7023' issued to agent 'SRVFSAGN.AG'.
	BFGCL0196I: The transfer was successfully cancelled.

En el log se debe visualizar que se cancelo::

	2022-09-10T21:41:32;414d5120535256465341474e202020204bcf1c6303ac7023;[TSTR];;SRVFSAGN.AG;SRVFSAGN;STANDARD;MERNTAGN.AG;MERNTAGN;cgomeznt;;;com.ibm.wmqfte.SourceAgent=SRVFSAGN.AG, com.ibm.wmqfte.DestinationAgent=MERNTAGN.AG, com.ibm.wmqfte.MqmdUser=usrmq, com.ibm.wmqfte.OriginatingUser=cgomeznt, com.ibm.wmqfte.OriginatingHost=192.168.1.5, com.ibm.wmqfte.TransferId=414d5120535256465341474e202020204bcf1c6303ac7023, com.ibm.wmqfte.Priority=5;
	2022-09-10T21:44:36;414d5120535256465341474e202020204bcf1c6303ac7023;[TCAN]; ;SRVFSAGN.AG;SRVFSAGN;STANDARD;MERNTAGN.AG;MERNTAGN;;mqm;;;


Listamos y veremos que esta cancelada y luedo de un rato desaparece::


	$ fteShowAgentDetails -v SRVFSAGN.AG
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	Agent Information:
	    Name:                             SRVFSAGN.AG
	    Type:                             Standard
	    Description:                      Agent Principal SRVFSAGN
	    Operating System:                 Linux
	    Host Name:                        srvfsagn
	    Time Zone:                        Eastern Standard Time
	    Product Version:                  9.1.0.0
	    Build Level:                      p910-L180705
	    Trace Level:                      No trace specified
	    Trace FFDC:                       No FFDC specified

	Agent Controller Information:
	    Controller Type:                  MQMFT Process Controller
	    Status:                           UNKNOWN
	    Status Details:                   Information about the agent controller is
		                              not available. Possible reasons are: (1) 
		                              the agent is not running  (2) the agent 
		                              is running on a different system. (3) the
		                              agent is started by a different user.
	    Agent Restarts within Interval:   0
	    Total Agent Restart Count:        0

	Agent Availability Information:
	    Status:                           ACTIVE
	    Status Age:                       0:00:28
	    Status Details:                   The agent is running and is publishing 
		                              its status at regular intervals. The last
		                              update was received within the expected 
		                              time period. The agent is currently 
		                              processing one or more transfers.
	    Start Time:                       2022-09-10T17:55:35Z

	Queue Manager Information:
	    Name:                             SRVFSAGN
	    Transport:                        Client
	    Host:                             192.168.1.110
	    Port:                             1418
	    Channel:                          SYSTEM.DEF.SVRCONN
	    Last Status Reported:             UNKNOWN
	    Status Details:                   Information about the queue manager is 
		                              not available because the agent has a 
		                              client connection to the queue  manager.

	Maximum Number of Running Source Transfers: 25
	Maximum Number of Queued Source Transfers: 1000
	Source Transfer States:
	    TransferId                                          State
	    414d51204352433031434d4d202020204acf1c630391ea20    started
	    414d5120535256465341474e202020204bcf1c6303ac7023    cancelled




