Status del Logger
====================

Iniciar, Estatus y detener el Logger



Iniciar::

	$ fteStartLogger filelogger1
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCL0287I: The request to start the logger on this machine has been submitted.
	BFGCL0526I: Logger log files located at: /var/mqm/mqft/logs/CRC01CRD/loggers/FILELOGGER1/logs

Estatus::

	$ fteShowLoggerDetails filelogger1
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	Logger Controller Information:
	    Controller Type:                   MQMFT Process Controller
	    Status:                            STARTED
	    Status Details:                    The logger process controller has 
		                               started the logger process.
	    Logger Restarts within Interval:   0
	    Total Logger Restart Count:        0

	Logger Availability Information:
	    Status:                            AVAILABLE
	    Status Details:                    The logger is running and available on 
		                               the local system.

	BFGUT0002E: An internal error has occurred. Product failure data was captured in file "FFDC.FTE.20220909162515974.log".
	BFGUB0038E: Internal error: The property name 'wmqfte.queue.manager.port' has an invalid or missing string value

Detener::

	$ fteStopLogger filelogger1
	5724-H72 Copyright IBM Corp.  2008, 2018.  ALL RIGHTS RESERVED
	BFGCL0528I: Issuing stop request to logger 'FILELOGGER1'. The command will wait for the logger to stop.
	BFGCL0529I: Logger 'FILELOGGER1' has been stopped.


