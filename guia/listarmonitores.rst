Listar Supervisores o Monitores
============================

Este es un pequeño help::

    fteListMonitors [-p <configurationOptions>]
                    [-ma <agentName>]
                    [-mn <monitorName>]
                    [-v] [-ox <filename>]
                    [-mquserid <user>] [-mqpassword <password>]

Como utilizarlo y esto crea un archivo en formato xml::

	fteListMonitors -ma BACT01AGN.AG -mn TARJETA_PREPAGADA_ACTIVO_CCR_1 -ox NOMBRE_del_ARCHIVO.xml

Este es el script get_all_Monitors.sh::

	#!/bin/bash

	FOLDER_OUT="/usr/local/bin/TranferFiles"
	FECHA=$(date +%d%m%Y_%H%M)
	mkdir -p $FOLDER_OUT/Supervisores_$FECHA
	cd $FOLDER_OUT/Supervisores_$FECHA
	fteListMonitors | awk '{print "fteListMonitors -ma "$1" -mn "$2" -ox "$2".txt"}' | egrep -v "MFT|BFG|BFG|Agent" | /bin/bash
	exit 0


	#MERNTAGN:MERCANTIL_NAIGUATA:6304:MERNTAGN.AG
