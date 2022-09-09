Listar el detalle de un agente
============================

Para listar el detalle de los agentes con el comando fteShowAgentDetails::


	$ fteShowAgentDetails CRC06AGN.AG
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to IBM MQ. Therefore, the assumption is that IBM MQ authentication has been disabled.
	Agent Information:
	    Name:                             CRC06AGN.AG
	    Type:                             Standard
	    Description:                      Agent de Prueba para el Qmanager CRC06AGN.QM
	    Operating System:                 Linux
	    Time Zone:                        Eastern Standard Time

	Agent Controller Information:
	    Controller Type:                  MQMFT Process Controller
	    Status:                           STARTED
	    Status Details:                   The agent process controller has started 
		                              the agent process.
	    Agent Restarts within Interval:   0
	    Total Agent Restart Count:        0

	Agent Availability Information:
	    Status:                           READY
	    Status Age:                       0:01:56
	    Status Details:                   The agent is running and is publishing 
		                              its status at regular intervals. The last
		                              update was received within the expected 
		                              time period. The agent is ready to 
		                              process transfers, but none are currently
		                              in progress.
	    Start Time:                       2022-09-08T21:22:34Z

	Queue Manager Information:
	    Name:                             CRC06AGN
	    Transport:                        Client
	    Host:                             192.168.1.110
	    Port:                             1424
	    Channel:                          SYSTEM.DEF.SVRCONN
	    Last Status Reported:             UNKNOWN
	    Status Details:                   Information about the queue manager is 
		                              not available because the agent has a 
		                              client connection to the queue  manager.

