Listar Colas
===============

Como listar las colas de los Qmanager::

	$ dspmq

	$ echo "DISPLAY QLOCAL ( * )" | runmqsc CRC01CRD

	$ echo "DISPLAY QLOCAL ( * )" | runmqsc CRC01CMM

Listar las colas de todos los Qmanagers::

	$ for qmanagers in $(dspmq | awk '{print $1}' | awk -F"(" '{print $2}' | tr -d ')') ; do echo "COLA $qmanagers" && echo "DISPLAY QLOCAL ( * )" | runmqsc $qmanagers && echo " " ; done

