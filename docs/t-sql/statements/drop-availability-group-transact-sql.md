---
title: DROP AVAILABILITY GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
caps.latest.revision: 44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d217c227333a15664773dc02285b7458d48c1517
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  删除指定的可用性组或其所有副本。 如果在删除某一可用性组时承载可用性副本之一的服务器实例处于脱机状态，则在联机后，该服务器实例将删除本地可用性副本。 删除可用性组时，还会删除关联的可用性组侦听器（如果有）。  
  
> [!IMPORTANT]  
>  如果可能，请仅在连接到承载主副本的服务器实例时删除此可用性组。 从主副本中删除此可用性组时，允许对以前的主数据库进行更改（不具有高可用性保护）。 从辅助副本中删除可用性组会使主副本处于 **RESTORING** 状态，且不允许对此数据库进行更改。  
  
 有关删除可用性组的其他方法的信息，请参阅[删除可用性组 (SQL Server)](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 group_name  
 指定要删除的可用性组的名称。  
  
## <a name="limitations-and-recommendations"></a>限制和建议  
  
-   执行 **DROP AVAILABILITY GROUP** 需要在服务器实例上启用 Always On 可用性组功能。 有关详细信息，请参阅[启用和禁用 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)。  
  
-   **DROP AVAILABILITY GROUP** 不能作为批处理的一部分执行，也不能在事务内执行。 此外，不支持表达式和变量。  
  
-   您可以从拥有某一可用性组的正确安全凭据的任何 Windows Server 故障转移群集 (WSFC) 节点删除该可用性组。 因此，在某一可用性组未保留任何可用性副本时，您可以删除该可用性组。  
  
    > [!IMPORTANT]  
    >  如果 Windows Server 故障转移群集 (WSFC) 群集没有仲裁，则避免删除可用性组。 如果在群集缺少仲裁时必须删除可用性组，则不删除群集中存储的元数据可用性组。 在群集重新获得仲裁后，将需要再次删除此可用性组以便将其从 WSFC 群集中删除。  
  
-   在辅助副本上，**DROP AVAILABILITY GROUP** 应仅用于紧急情况。 这是因为删除可用性组会使该可用性组脱机。 如果从辅助副本中删除该可用性组，则主副本无法确定出现 **OFFLINE** 状态是因为仲裁丢失、强制故障转移还是 **DROP AVAILABILITY GROUP** 命令。 主副本将转换为 **RESTORING** 状态以避免出现可能的裂脑情况。 有关详细信息，请参阅 [工作方式：DROP AVAILABILITY GROUP 行为](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) （CSS SQL Server 工程师博客）。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 对可用性组要求 **ALTER AVAILABILITY GROUP** 权限、**CONTROL AVAILABILITY GROUP** 权限、**ALTER ANY AVAILABILITY GROUP** 权限或 **CONTROL SERVER** 权限。 若要删除并非由本地服务器实例承载的某一可用性组，需要针对该可用性组的 **CONTROL SERVER** 权限或 **CONTROL** 权限。  
  
## <a name="examples"></a>示例  
 下面的示例删除了 `AccountsAG` 可用性组。  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [工作方式：DROP AVAILABILITY GROUP 行为](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) （CSS SQL Server 工程师博客）  
  
## <a name="see-also"></a>另请参阅  
 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [删除可用性组 (SQL Server)](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
