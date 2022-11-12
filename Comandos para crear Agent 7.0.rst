1) Instalar el producto MQ FTE Agent
2) Crear el agente previa configuración del Qmanager (D:\IBM\WMQFTE\bin):
fteCreateAgent -agentName CTK01AGN.AG -agentQMgr CTK01AGN -agentQMgrHost 10.136.0.106 -agentQMgrPort 1445 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "CESTA TICKET"

3) Verificar que se hay creado la carpeta de la configuración o metadata del agente. (D:\IBM\WMQFTE\config\CRC01CRD\agents)
4) Iniciar el agente:
fteStartAgent CTK01AGN.AG

5) Verificar en el MQ Explorer que aparezca activo el agente.
6) en el MQ Explorer darle click derecho sobre el agente y probar conectividad.
7) Desde el MQFTE Server hacer un netstat para certificar la conexión.

>fteStopAgent.cmd CTK01AGN.AG #detener un agente

>fteDeleteAgent.cmd CTK01AGN.AG #borrar un agente
