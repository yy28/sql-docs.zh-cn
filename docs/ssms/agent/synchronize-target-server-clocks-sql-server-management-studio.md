---
title: 同步目标服务器时钟 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c54856dcbbb5d3f372e4f7e785b7844f2b67387a
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2018
ms.locfileid: "42776174"
---
# <a name="synchronize-target-server-clocks-sql-server-management-studio"></a>Synchronize Target Server Clocks (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题介绍了如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中使目标服务器时钟与主服务器时钟同步。 同步这些系统时钟可以为实现您的作业计划提供支持。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要同步目标服务器的时钟，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>安全性  
  
#### <a name="Permissions"></a>Permissions  
要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-synchronize-target-server-clocks"></a>同步目标服务器的时钟  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要使目标服务器时钟与主服务器时钟同步的服务器。  
  
2.  右键单击“SQL Server 代理”，指向“多服务器管理”，然后选择“管理目标服务器”。  
  
3.  在 **“管理目标服务器”** 对话框中，单击 **“发布指令”**。  
  
4.  在 **“指令类型”** 列表中，选择 **“同步时钟”**。  
  
5.  在 **“收件人”** 下，执行以下操作之一：  
  
    -   单击 **“所有目标服务器”** 使所有目标服务器时钟与主服务器时钟同步。  
  
    -   单击 **“以下目标服务器”** 同步某些特定的服务器时钟，然后选择要使其时钟与主服务器时钟同步的每台目标服务器。  
  
6.  完成后，单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-synchronize-target-server-clocks"></a>同步目标服务器的时钟  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_resync_targetserver (Transact-SQL)](http://msdn.microsoft.com/40e44df7-d3e3-44ee-b149-08aba629a21f)。  
  
