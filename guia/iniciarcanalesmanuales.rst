
Iniciar los Canales del QManager creado Manual
=====================================

::

	QMANAGER="CRC06AGN"

::

	echo "display channel(*)" | runmqsc CRC06AGN | grep -v SYST | grep "CHLTYPE(SDR)" | awk {'print $1'} | awk -F\( {'print $2'} | sed s/\)//g

	CRC06AGN.A.CRC01CMM
	CRC06AGN.A.CRC01CRD
	CRC06AGN.A.SRVFSAGN

Iniciar los canales::

	echo "START CHANNEL(CRC06AGN.A.CRC01CMM)" | runmqsc CRC06AGN
	echo "START CHANNEL(CRC06AGN.A.CRC01CRD)" | runmqsc CRC06AGN
	echo "START CHANNEL(CRC06AGN.A.SRVFSAGN)" | runmqsc CRC06AGN

Estatus los canales::

	echo "DISPLAY CHSTATUS(CRC06AGN.A.CRC01CMM)" | runmqsc CRC06AGN 
	echo "DISPLAY CHSTATUS(CRC06AGN.A.CRC01CRD)" | runmqsc CRC06AGN 
	echo "DISPLAY CHSTATUS(CRC06AGN.A.SRVFSAGN)" | runmqsc CRC06AGN 


Detener los canales::

	echo "STOP CHANNEL(CRC06AGN.A.CRC01CMM)" | runmqsc CRC06AGN
	echo "STOP CHANNEL(CRC06AGN.A.CRC01CRD)" | runmqsc CRC06AGN
	echo "STOP CHANNEL(CRC06AGN.A.SRVFSAGN)" | runmqsc CRC06AGN


Esta es la forma automatica gracias al script start-channel.sh::

$ for i in $(dspmq | awk '{print $1}' | awk -F"(" '{print $2}' | tr -d ')') ; do ./start-channel.sh $i ; done


