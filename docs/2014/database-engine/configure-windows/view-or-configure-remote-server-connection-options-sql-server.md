---
title: 查看或配置远程服务器连接选项 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- remote servers [SQL Server], connection options
- servers [SQL Server], remote
- connections [SQL Server], remote servers
ms.assetid: 356d3e6b-8514-4bd2-a683-9de147949b2b
caps.latest.revision: 24
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6307492a6014c7e789b283cbff80226e17fd23d7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123466"
---
# <a name="view-or-configure-remote-server-connection-options-sql-server"></a>查看或配置远程服务器连接选项 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中在服务器级别查看或配置远程服务器连接选项。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要查看或配置远程服务器连接选项，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：**[在配置远程服务器连接选项之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 执行 **sp_serveroption** 要求服务器上的 ALTER ANY LINKED SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-configure-remote-server-connection-options"></a>查看或配置远程服务器连接选项  
  
1.  在“对象资源管理器”中，右键单击服务器，再单击“属性” 。  
  
2.  在“SQL Server 属性 - \<server_name>”**** 对话框中，单击“连接”。  
  
3.  在 **“连接”** 页上，查看 **“远程服务器连接”** 设置，并根据需要进行修改。  
  
4.  在远程服务器对的另一台服务器上重复步骤 1 到 3。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-remote-server-connection-options"></a>查看远程服务器连接选项  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例使用 [sp_helpserver](/sql/relational-databases/system-stored-procedures/sp-helpserver-transact-sql) 返回有关所有远程服务器的信息。  
  
```tsql  
USE master;  
GO  
EXEC sp_helpserver ;  
```  
  
#### <a name="to-configure-remote-server-connection-options"></a>配置远程服务器连接选项  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 本示例显示如何使用 [sp_serveroption](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql) 配置远程服务器。 该示例配置与另一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例（即 `SEATTLE3`）相对应的远程服务器，使其排序规则与本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例兼容。  
  
```tsql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
##  <a name="FollowUp"></a> 跟进：在配置远程服务器连接选项之后  
 必须停止后再重新启动远程服务器，设置才会生效。  
  
## <a name="see-also"></a>请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [远程服务器](remote-servers.md)   
 [链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_linkedservers (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-linkedservers-transact-sql)   
 [sp_helpserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpserver-transact-sql)   
 [sp_serveroption (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql)  
  
  
