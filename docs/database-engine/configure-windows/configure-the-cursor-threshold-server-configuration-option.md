---
title: "配置“游标阈值”服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: cursor threshold option
ms.assetid: 189f2067-c6c4-48bd-9bd9-65f6b2021c12
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a6695ff7007a9a3b3145f88362f0ae201c75fd8f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="configure-the-cursor-threshold-server-configuration-option"></a>配置 cursor threshold 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题说明如何使用 **或** 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中配置 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cursor threshold [!INCLUDE[tsql](../../includes/tsql-md.md)]服务器配置选项。 **cursor threshold** 选项指定游标集中的行数，超过此行数，将异步生成游标键集。 当游标为结果集生成键集时，查询优化器会估算将为该结果集返回的行数。 如果查询优化器估算出的返回行数大于此阈值，则将异步生成游标，使用户能够在继续填充游标的同时从该游标中提取行。 否则，同步生成游标，查询将一直等待到返回所有行。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **配置 cursor threshold 选项，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：**  [在配置游标阙值选项之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持异步生成由键集驱动的或静态的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标操作（如 OPEN 或 FETCH）均为批处理，所以无需异步生成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 由于每个游标操作都需要进行客户端往返，因此继续支持异步的由键集驱动的或静态的应用程序编程接口 (API) 服务器游标，对于这些游标，OPEN 实现低延迟时间很重要。  
  
-   查询优化器估计键集中行数的准确性取决于游标中每个表统计信息的当前值。  
  
###  <a name="Recommendations"></a> 建议  
  
-   此选项是一个高级选项，仅应由有经验的数据库管理员或认证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术人员更改。  
  
-   如果将 **游标阙值** 设置为 -1，则所有游标键集将同步生成，这对于小游标集很有用。 如果将 **cursor threshold** 设置为 0，则所有游标键集将异步生成。 如果 **cursor threshold**为其他值，则查询优化器将比较该值与游标集中的所需行数，如果后者大于前者，则将异步生成键集。 不要将 **cursor threshold** 的值设置得过低，因为最好以同步方式创建小结果集。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要执行带两个参数的 **sp_configure** 以更改配置选项或运行 RECONFIGURE 语句，则用户必须具备 ALTER SETTINGS 服务器级别的权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>配置 cursor threshold 选项  
  
1.  在对象资源管理器中，右键单击“服务器”并选择“属性”。  
  
2.  单击 **“高级”** 节点。  
  
3.  在 **“杂项”**下，将 **“游标阈值”** 选项更改为所需的值。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>配置 cursor threshold 选项  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此示例说明如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 将 `cursor threshold` 选项设置为 `0` ，以便异步生成游标键集。  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cursor threshold', 0 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)服务器配置选项。  
  
##  <a name="FollowUp"></a> 跟进：在配置 cursor threshold 选项之后  
 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>另请参阅  
 [@@CURSOR_ROWS (Transact-SQL)](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [更新统计信息 (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
