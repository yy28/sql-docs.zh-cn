---
title: "配置 index create memory 服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: index create memory option
ms.assetid: 3d722d9b-bada-4bf5-a9d7-bfc556bb4915
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2bb4dddd24def2a1e442b7dded3b1054729b587f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-index-create-memory-server-configuration-option"></a>配置 index create memory 服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本主题说明如何使用 **或** 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中配置 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] index create memory [!INCLUDE[tsql](../../includes/tsql-md.md)]服务器配置选项。 **index create memory** 选项控制最初为创建索引分配的最大内存量。 此选项的默认值为 0（自动配置）。 如果随后创建索引时需要更多内存，而且有内存可供使用，服务器将使用可用的内存，从而超出此选项的设置。 如果没有内存可供使用，则继续使用已分配的内存来创建索引。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **配置 index create memory 选项，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：**[在配置 index create memory 选项之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   **min memory per query** 选项的设置优先于 **index create memory** 选项的设置。 如果更改这些选项，使 **index create memory** 小于 **min memory per query**，则会收到警告消息，但设置的值仍会生效。 而且，在查询执行过程中，您还会收到类似的警告。  
  
-   使用已分区表和已分区索引时，如果出现非对齐的已分区索引且并行度很高，则创建索引时的最低内存要求将显著提高。 此选项控制在单一索引创建操作中为所有索引分区分配的初始内存总量。 如果此选项设置的内存量小于运行查询所需的最小内存，查询将终止并显示错误消息。  
  
-   此选项的运行值不会超过用于运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的操作系统和硬件平台的实际内存量。  
  
###  <a name="Recommendations"></a> 建议  
  
-   此选项是一个高级选项，仅应由有经验的数据库管理员或认证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术人员更改。  
  
-   **index create memory** 选项是自行配置的，通常不需要调整即可工作。 但如果在创建索引时遇到困难，可以考虑提高此选项的运行值。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要执行带两个参数的 **sp_configure** 以更改配置选项或运行 RECONFIGURE 语句，则用户必须具备 ALTER SETTINGS 服务器级别的权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-index-create-memory-option"></a>配置 index create memory 选项  
  
1.  在对象资源管理器中，右键单击“服务器”并选择“属性”。  
  
2.  单击 **“内存”** 节点。  
  
3.  在 **“创建索引占用的内存”**下，为 index create memory 选项键入或选择所需的值。  
  
     **index create memory** 选项用于控制索引创建排序时所需的内存量。 **index create memory** 选项是自配置选项，在大多数情况下不需调整即可正常工作。 但如果在创建索引时遇到困难，可以考虑提高此选项的运行值。 查询排序由 **min memory per query** 选项控制。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-index-create-memory-option"></a>配置 index create memory 选项  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此示例说明如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 将 `index create memory` 选项的值设置为 `4096`。  
  
```tsql  
USE AdventureWorks2012 ;  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
EXEC sp_configure 'index create memory', 4096  
GO  
RECONFIGURE;  
GO  
```  
  
 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)服务器配置选项。  
  
##  <a name="FollowUp"></a> 跟进：在配置 index create memory 选项之后  
 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>另请参阅  
 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
