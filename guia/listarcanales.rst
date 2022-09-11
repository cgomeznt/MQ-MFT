Listar Canales
===============

Como listar los canales de los Qmanager::

	$ dspmq

	$ echo "display channel(*)" | runmqsc CRC01CRD

	$ echo "display channel(*)" | runmqsc CRC01CMM

Listar los canales de todos los Qmanagers::

	$ for qmanagers in $(dspmq | awk '{print $1}' | awk -F"(" '{print $2}' | tr -d ')') ; do echo "COLA $qmanagers" && echo "display channel(*)" | runmqsc $qmanagers && echo " " ; done

