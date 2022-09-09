Crear una transferencia Manual
====================================

::
	# mkdir -p /opt/SRVFSAGN.AG/{ENTRADA,SALIDA}
	# mkdir -p /opt/CRC06AGN.AG/{ENTRADA,SALIDA}
	# touch /opt/BNC2NTAGN.AG/SALIDA/BNC2NTAGN.to.SRVFSAGN
	# touch /opt/CRC06AGN.AG/SALIDA/ARCHIVO_A_ENVIAR.txt
	# chown -R mqm. /opt/CRC06AGN.AG/
	# chown -R mqm. /opt/SRVFSAGN.AG/

::

	fteCreateTransfer -sa SRVFSAGN.AG -sm SRVFSAGN  -da CRC06AGN.AG  -dm CRC06AGN -de overwrite -dd /opt/CRC06AGN.AG/ENTRADA/ /opt/SRVFSAGN.AG/SALIDA/*

::

	fteCreateTransfer -sa CRC06AGN.AG -sm CRC06AGN  -da SRVFSAGN.AG  -dm SRVFSAGN -de overwrite -dd /opt/SRVFSAGN.AG/ENTRADA/ /opt/CRC06AGN.AG/SALIDA/*
