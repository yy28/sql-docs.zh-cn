---
title: AlwaysOn 可用性组（SQL Server）的 Transact-sql 语句概述 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: 184d0a81-2259-4db9-9d0d-01aac0b502c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f635faa05d7d77a50d31491b1bab9b16875e728c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62813807"
---
# <a name="overview-of-transact-sql-statements-for-alwayson-availability-groups-sql-server"></a>AlwaysOn 可用性组的 Transact-SQL 语句概述 (SQL Server)
  本主题介绍支持部署 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 以及创建和管理指定的可用性组、可用性副本和可用性数据库的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 语句。  
  
  
##  <a name="CreateEndpoint"></a>创建终结点  
 [创建终结点 .。。对于 DATABASE_MIRRORING](/sql/t-sql/statements/create-endpoint-transact-sql)创建数据库镜像端点（如果服务器实例上不存在）。 要对其部署 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 或数据库镜像的每个服务器实例都需要一个数据库镜像端点。  
  
 在您对其创建端点的服务器实例上执行此语句。 仅能在给定的服务器实例上创建一个数据库镜像端点。 有关详细信息，请参阅 [数据库镜像终结点 (SQL Server)](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)。  
  
##  <a name="CreateAG"></a>创建可用性组  
 [创建可用性组](/sql/t-sql/statements/create-availability-group-transact-sql)将创建新的可用性组，还可以选择可用性组侦听器。 必须至少指定您的本地服务器实例，该实例将成为初始主副本。 还可以选择指定最多四个辅助副本。  
  
 在要承载新可用性组的初始主副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上执行 CREATE AVAILABILITY GROUP。 此服务器实例必须驻留在 Windows Server 故障转移群集（WSFC）的节点上（有关详细信息，请参阅[AlwaysOn 可用性组 &#40;SQL Server&#41;的先决条件、限制和建议](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
##  <a name="AlterAG"></a>更改可用性组  
 [ALTER AVAILABILITY group](/sql/t-sql/statements/alter-availability-group-transact-sql)支持更改现有可用性组或可用性组侦听器，并支持对可用性组进行故障转移。  
  
 在承载当前主副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上执行 ALTER AVAILABILITY GROUP。  
  
##  <a name="AlterDb"></a>更改数据库 .。。设置 HADR .。。  
 使用 ALTER DATABASE 语句的 [SET HADR](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) 子句的选项，您可以将辅助数据库联接到相应主数据库的可用性组、删除已联接的数据库、在已联接的数据库上挂起数据同步以及继续数据同步。  
  
##  <a name="DropAG"></a>删除可用性组  
 [DROP AVAILABILITY group](/sql/t-sql/statements/drop-availability-group-transact-sql)删除指定的可用性组及其所有副本。 DROP AVAILABILITY GROUP 可以从 WSFC 故障转移群集的任何 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 节点上运行。  
  
##  <a name="Restrictions"></a>对可用性组 Transact-sql 语句的限制  
 CREATE AVAILABILITY GROUP、ALTER AVAILABILITY GROUP 和 DROP AVAILABILITY GROUP [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句具有以下限制：  
  
-   执行这些语句需要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例上启用 HADR 服务，但 DROP AVAILABILITY GROUP 除外。 有关详细信息，请参阅[启用和禁用 AlwaysOn 可用性组 (SQL Server)](enable-and-disable-always-on-availability-groups-sql-server.md)。  
  
-   这些语句不能在事务或批处理中执行。  
  
-   尽管这些语句可以最大程度地在失败后进行清除，但不能保证出现故障时回滚所有更改。 但是，系统应该能够完全处理并忽略部分故障。  
  
-   这些语句不支持表达式或变量。  
  
-   如果当另一个可用性组操作或恢复正在执行时执行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，则该语句返回错误。 等待该操作或恢复完成，然后重试该语句（根据需要）。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
