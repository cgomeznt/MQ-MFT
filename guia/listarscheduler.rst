Listar Scheduler
============================

Este es un pequeño help::

	fteListScheduledTransfers [-p <configurationOptions>] [Pattern]
		                      [-mquserid <user>] [-mqpassword <password>]

Como utilizarlo y esto crea un archivo en formato xml::

	fteListScheduledTransfers 

Salida del comando fteListScheduledTransfers ::

	$ fteListScheduledTransfers 
	5655-MFT, 5724-H72 Copyright IBM Corp.  2008, 2014.  ALL RIGHTS RESERVED
	BFGPR0127W: No credentials file has been specified to connect to WebSphere MQ. Therefore, the assumption is that WebSphere MQ authentication has been disabled.
	Schedule Identifier:        1
	Job Name:                   EMBOCED_BANCARIBE
	Source Agent Name:          BCRB02AGN.AG
	Source File Name:           F:\Intercambio_BC_CC\FOR*
	Conversion Type:            binary
	Destination File Name:      /301/DCLIBR/Entrada/
	Destination Agent Name:     CRC03AGN1.AG
	Schedule Start Time:        2020-08-17T11:00-0400
	Next Transfer:              2022-09-09T22:30-0400
	Schedule Time Base:         admin
	Repeat Interval:            minutes
	Repeat Frequency:           30

Esta el script::

	$ /usr/local/bin/get_all_Sheduler.sh

