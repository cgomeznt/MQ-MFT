Limpiar Colas
==============

Se debe primero listar todas COLAS de un Qmanager, Por ejemplo el Qmanager del Coordinator "COORDINATOR=CRC01CRD" tiene todas estas colas::
	
	BNC2NTAGN
	CRC01CMM
	CRC01CRD.DQ
	CRC06AGN
	MERNTAGN
	SRVFSAGN

El "COMMANDER=CRC01CM" tiene todas estas colas::

	BNC2NTAGN
	CRC01CMM.DQ
	CRC01CRD
	CRC06AGN
	MERNTAGN
	SRVFSAGN

El "SRVFS_CLIENT=SRVFSAGN" tiene todas estas colas::

	BNC2NTAGN
	CRC01CMM
	CRC01CRD
	CRC06AGN
	MERNTAGN
	SRVFSAGN.DQ

Y por dar un ejemplo de un Qmanger que corresponde a un agente que no es el principal MERNTAGN::

	CRC01CMM
	CRC01CRD
	MERNTAGN.DQ
	SRVFSAGN

Recordemos que tenemos en el ENV estas variables definidas en el .profile o .bashrh::

	COORDINATOR=CRC01CRD
	COMMANDER=CRC01CMM
	SRVFS_CLIENT=SRVFSAGN

Como listar todas los colas del COORDINATOR , COMMANDER y del SRVFS_CLIENT::


	echo "DISPLAY QLOCAL ( * )" | runmqsc $COORDINATOR | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d'


	echo "DISPLAY QLOCAL ( * )" | runmqsc $COMMANDER | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d' 


	echo "DISPLAY QLOCAL ( * )" | runmqsc $SRVFS_CLIENT | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d' 


Ahora que ya tenemos las COLAS podemos hacer un CLEAR QLOCAL en cada una de ellas, el $i debemos ir colocando todas las colas que listamos::

	echo "CLEAR QLOCAL ( $i )" | runmqsc $COORDINATOR
	echo "CLEAR QLOCAL ( $i )" | runmqsc $COMMANDER
	echo "CLEAR QLOCAL ( $i )" | runmqsc $SRVFS_CLIENT

Solo vamos hacer la del $COORDINATOR para dar un ejemplo y no cargar visualmente el documento y ver su salida::

	$ echo "CLEAR QLOCAL ( BNC2NTAGN )" | runmqsc $COORDINATOR
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : CLEAR QLOCAL ( BNC2NTAGN )
	AMQ8022I: IBM MQ queue cleared.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	[mqm@mq-server tools]$ echo "CLEAR QLOCAL ( CRC01CMM )" | runmqsc $COORDINATOR
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : CLEAR QLOCAL ( CRC01CMM )
	AMQ8148E: IBM MQ object in use.
	One MQSC command read.
	No commands have a syntax error.
	One valid MQSC command could not be processed.
	[mqm@mq-server tools]$ echo "CLEAR QLOCAL ( CRC01CRD.DQ )" | runmqsc $COORDINATOR
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : CLEAR QLOCAL ( CRC01CRD.DQ )
	AMQ8022I: IBM MQ queue cleared.
	One MQSC command read.
	No commands have a syntax error.
	All valid MQSC commands were processed.
	[mqm@mq-server tools]$ echo "CLEAR QLOCAL ( SRVFSAGN )" | runmqsc $COORDINATOR
	5724-H72 (C) Copyright IBM Corp. 1994, 2018.
	Starting MQSC for queue manager CRC01CRD.


	     1 : CLEAR QLOCAL ( SRVFSAGN )
	AMQ8148E: IBM MQ object in use.
	One MQSC command read.
	No commands have a syntax error.
	One valid MQSC command could not be processed.




Como lo hacemos automatico::


	COLAS_COORDINATOR=$(echo "DISPLAY QLOCAL ( * )" | runmqsc $COORDINATOR | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d')


	COLAS_COMMANDER=$(echo "DISPLAY QLOCAL ( * )" | runmqsc $COMMANDER | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d')


	COLAS_SRVFS_CLIENT=$(echo "DISPLAY QLOCAL ( * )" | runmqsc $SRVFS_CLIENT | egrep -v "AMQ8409|SYSTEM" | awk '{print $1}' | egrep -v "TYPE|5724-H72|Starting|AMQ.MQEXPLORER|One|No|All" | awk -F'(' '{print $2}' | tr -d ")" | sed '/^ *$/d')


	for i in $(echo  $COLAS_COORDINATOR) ; do echo "CLEAR QLOCAL ( $i )" | runmqsc $COORDINATOR && sleep 1;done


	for i in $(echo  $COLAS_COMMANDER) ; do echo "CLEAR QLOCAL ( $i )" | runmqsc $COMMANDER && sleep 1;done


	for i in $(echo  $COLAS_SRVFS_CLIENT) ; do echo "CLEAR QLOCAL ( $i )" | runmqsc $SRVFS_CLIENT && sleep 1;done





