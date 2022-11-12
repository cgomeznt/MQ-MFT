Comandos MQ para crear los dos Agentes de BDV y BNC.

BANCO DE VENEZUELA
==============

PRODUCCION

fteSetupCoordination -coordinationQMgr CRC01CRD -coordinationQMgrHost 10.134.8.16 -coordinationQMgrPort 2414 -coordinationQMgrChannel SYSTEM.DEF.SVRCONN

fteSetupCommands.cmd -connectionQMgr CR01CMM -connectionQMgrHost 10.134.8.16 -connectionQMgrPort 2416 -connectionQMgrChannel SYSTEM.DEV.SVRCONN

fteCreateAgent -agentName BDVNTAGN.AG -agentQMgr BDVNTAGN -agentQMgrHost 10.134.8.16 -agentQMgrPort 8704 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "AGENT_BDV_NTA_PRD"

------------------------
CALIDAD

fteSetupCoordination -coordinationQMgr CRC01CRD -coordinationQMgrHost 10.134.3.129 -coordinationQMgrPort 2414 -coordinationQMgrChannel SYSTEM.DEF.SVRCONN

fteSetupCommands.cmd -connectionQMgr CR01CMM -connectionQMgrHost 10.134.3.129 -connectionQMgrPort 2416 -connectionQMgrChannel SYSTEM.DEV.SVRCONN

fteCreateAgent -agentName BDVNTAGN.AG -agentQMgr BDVNTAGN -agentQMgrHost 10.134.3.129 -agentQMgrPort 8704 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "AGENT_BDV_NTA_QA"

-----------------------
DESARROLLO

fteSetupCoordination -coordinationQMgr CRC01CRD -coordinationQMgrHost 10.134.3.139 -coordinationQMgrPort 2414 -coordinationQMgrChannel SYSTEM.DEF.SVRCONN

fteSetupCommands.cmd -connectionQMgr CR01CMM -connectionQMgrHost 10.134.3.139 -connectionQMgrPort 2416 -connectionQMgrChannel SYSTEM.DEV.SVRCONN

fteCreateAgent -agentName BDVNTAGN.AG -agentQMgr BDVNTAGN -agentQMgrHost 10.134.3.139 -agentQMgrPort 6704 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "AGENT_BDV_NTA_DES"

---------------------

BANCO NACIONAL DE CREDITO
===========================

PRODUCCION

fteSetupCoordination -coordinationQMgr CRC01CRD -coordinationQMgrHost 10.134.8.16 -coordinationQMgrPort 2414 -coordinationQMgrChannel SYSTEM.DEF.SVRCONN

fteSetupCommands.cmd -connectionQMgr CR01CMM -connectionQMgrHost 10.134.8.16 -connectionQMgrPort 2416 -connectionQMgrChannel SYSTEM.DEV.SVRCONN

fteCreateAgent -agentName BNCNTAGN.AG -agentQMgr BNCNTAGN -agentQMgrHost 10.134.8.16 -agentQMgrPort 8504 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "AGENT_BNC_NTA_PRD"

------------------------
CALIDAD

fteSetupCoordination -coordinationQMgr CRC01CRD -coordinationQMgrHost 10.134.3.129 -coordinationQMgrPort 2414 -coordinationQMgrChannel SYSTEM.DEF.SVRCONN

fteSetupCommands.cmd -connectionQMgr CR01CMM -connectionQMgrHost 10.134.3.129 -connectionQMgrPort 2416 -connectionQMgrChannel SYSTEM.DEV.SVRCONN

fteCreateAgent -agentName BNCNTAGN.AG -agentQMgr BNCNTAGN -agentQMgrHost 10.134.3.129 -agentQMgrPort 8504 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "AGENT_BNC_NTA_QA"

-----------------------
DESARROLLO

fteSetupCoordination -coordinationQMgr CRC01CRD -coordinationQMgrHost 10.134.3.139 -coordinationQMgrPort 2414 -coordinationQMgrChannel SYSTEM.DEF.SVRCONN

fteSetupCommands.cmd -connectionQMgr CR01CMM -connectionQMgrHost 10.134.3.139 -connectionQMgrPort 2416 -connectionQMgrChannel SYSTEM.DEV.SVRCONN

fteCreateAgent -agentName BNCNTAGN.AG -agentQMgr BNCNTAGN -agentQMgrHost 10.134.3.139 -agentQMgrPort 6504 -agentQMgrChannel SYSTEM.DEF.SVRCONN -agentDesc "AGENT_BNC_NTA_DES"

