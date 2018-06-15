---
title: 删除数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database removal [SQL Server], SQL Server Management Studio
- removing databases
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- database removal [SQL Server]
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8394b03046617af819f851441fe439eaf850b4b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32926602"
---
# <a name="delete-a-database"></a>删除数据库
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [!INCLUDE[tsql](../../includes/tsql-md.md)]中删除用户定义的数据库。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
     [建议](#Recommendations)  
  
     [Security](#Security)  
  
-   **删除数据库，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：**  [在删除数据库之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   不能删除系统数据库。  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   删除数据库中的所有数据库快照。 有关详细信息，请参阅[删除数据库快照 (Transact SQL)](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)。  
  
-   如果日志传送涉及数据库，请删除日志传送。  
  
-   如果为事务复制发布了数据库，或将数据库发布或订阅到合并复制，请从数据库中删除复制。  
  
###  <a name="Recommendations"></a> 建议  
  
-   考虑对数据库进行完整备份。 只有通过还原备份才能重新创建已删除的数据库。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要执行 DROP DATABASE 操作，用户必须至少对数据库具有 CONTROL 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-database"></a>删除数据库  
  
1.  在 **对象资源管理器**中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  展开 **“数据库”**，右键单击要删除的数据库，再单击 **“删除”**。  
  
3.  确认选择了正确数据库，然后单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-database"></a>删除数据库  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例删除 `Sales` 和 `NewSales` 数据库。  
  
```sql  
USE master ;  
GO  
DROP DATABASE Sales, NewSales ;  
GO  
```  
  
##  <a name="FollowUp"></a> 跟进：在删除数据库之后  
 备份 **master** 数据库。 如果必须还原 **master** ，则自上次备份 **master** 之后删除的所有数据库都将仍在系统目录视图中具有引用，并且可能会导致出现错误消息。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
