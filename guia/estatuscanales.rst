Estatus de los  Canales
===============

Primero debe los canales del Qmanager::

	$ dspmq

	$ echo "display channel(*)" | runmqsc CRC01CRD

	$ echo "display channel(*)" | runmqsc CRC01CMM


Luego de saber cuales son sus canales ahí si puede saber el estatus::

	$ echo -n "display chstatus(CRC01CRD.A.CRC01CMM)" | runmqsc CRC01CRD
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : display chstatus(CRC01CRD.A.CRC01CMM)
	AMQ8417I: Display Channel Status details.
	   CHANNEL(CRC01CRD.A.CRC01CMM)            CHLTYPE(SDR)
	   CONNAME(192.168.1.110(1416))            CURRENT
	   RQMNAME(CRC01CMM)                       STATUS(RUNNING)
	   SUBSTATE(MQGET)                         XMITQ(CRC01CMM)
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.


Listar un Qmanager para saber cuales son sus canales::

	$ echo "display channel(*)" | runmqsc CRC01CRD | grep -v SYST | grep CHLTYPE | awk {'print $1'} | awk -F\( {'print $2'} | sed s/\)//g

Listar todos los canales de un Qmanager::

	 for i in $(echo "display channel(*)" | runmqsc CRC01CRD | grep -v SYST | grep CHLTYPE | awk {'print $1'} | awk -F\( {'print $2'} | sed s/\)//g); do echo -n "display chstatus($i)" | runmqsc CRC01CRD ; done

Listar todos los canales y solo ver el STATUS de un Qmanager::

	$ for i in $(echo "display channel(*)" | runmqsc CRC01CRD | grep -v SYST | grep CHLTYPE | awk {'print $1'} | awk -F\( {'print $2'} | sed s/\)//g); do echo -n "display chstatus($i)" | runmqsc CRC01CRD | grep STATUS ; done
Listar los canales de los Qmanager y conocer su Estatus::


