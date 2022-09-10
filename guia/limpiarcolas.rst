Limpiar Colas
==============

Este es un script complejo que navega en cada una de las colas y la depura


	#!/bin/bash
	FILE_AGENTSQMANAGER="/tmp/AgentesMQ/listasAgents.txt"
	RUTA_TMP="/tmp/TranferMQ"
	TMPQLOCAL_CRD="/tmp/QLOCALCRD"
	TMPQLOCAL_CMM="/tmp/QLOCALCMM"
	TMPQLOCAL_AS400="/tmp/QLOCALAS400"

	function ListAgents {
		> $FILE_AGENTSQMANAGER
		for i in $(fteListAgents | awk '{print $1 "_" $2}' | tail -n +4) ; do echo $i ; done > $FILE_AGENTSQMANAGER
	}



	function DetallesTransfAgents {
		rm -f $RUTA_TMP/*
		for i in $(cat $FILE_AGENTSQMANAGER) ; do fteShowAgentDetails -v $(echo $i | awk -F"_" '{print $1}') | awk '{print $1}' | sed 's/[a-z,A-Z]*//' | sed '/^$/d' | egrep -v ":|MFT" > $RUTA_TMP/$i; done
	}

	function CanceledTranfAgents {

		for i in $(ls $RUTA_TMP/)
		do
			for j in $(cat $RUTA_TMP/$i)
			do
				NOMBREAGENTS=$(echo $i | awk -F"_" '{print $1}')
				NOMBREQMANAGER=$(echo $i | awk -F"_" '{print $2}')
				fteCancelTransfer -a $NOMBREAGENTS  -m $NOMBREQMANAGER $j
			done
		done
	}


	function display_QLOCAL {
		echo "DISPLAY QLOCAL ( * )" | runmqsc CRC01CRD | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d' > $TMPQLOCAL_CRD
		sleep 2
		echo "DISPLAY QLOCAL ( * )" | runmqsc CRC01CMM | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d' > $TMPQLOCAL_CMM
		sleep 2
		echo "DISPLAY QLOCAL ( * )" | runmqsc CRC03AGN | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d' > $TMPQLOCAL_AS400
		sleep 2
	}

	function depurador_QLOCAL {
		for i in $(cat  $TMPQLOCAL_CRD) ; do echo "CLEAR QLOCAL ( $i )" | runmqsc CRC01CRD && sleep 1;done
			for i in $(cat  $TMPQLOCAL_CMM) ; do echo "CLEAR QLOCAL ( $i )" | runmqsc CRC01CMM && sleep 1;done
				for i in $(cat  $TMPQLOCAL_AS400) ; do echo "CLEAR QLOCAL ( $i )" | runmqsc CRC03AGN && sleep 1;done
	}	


	>cat  limpieza-transfer.sh 
	#!/bin/bash

	PATH=/usr/lib64/qt-3.3/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/opt/mqm/bin:/var/mqm/bin

	source /usr/local/bin/tools/funciones

	display_QLOCAL
	depurador_QLOCAL
	ListAgents
	DetallesTransfAgents
	#CanceledTranfAgents &> /dev/null	
	CanceledTranfAgents	
	exit 0


