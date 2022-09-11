Iniciar Canales
===============

Primero debe los canales del Qmanager::

	$ dspmq

	$ echo "display channel(*)" | runmqsc CRC01CRD

	$ echo "display channel(*)" | runmqsc CRC06AGN


Detener los canales::

	echo "START CHANNEL(CRC06AGN.A.CRC01CMM)" | runmqsc CRC06AGN
	echo "START CHANNEL(CRC06AGN.A.CRC01CRD)" | runmqsc CRC06AGN
	echo "START CHANNEL(CRC06AGN.A.SRVFSAGN)" | runmqsc CRC06AGN
