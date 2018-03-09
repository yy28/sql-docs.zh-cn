---
title: "将目标服务器与主服务器脱离 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d1dbca0c49ac22ad09037a63d780a0ece0c0e7ce
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="defect-a-target-server-from-a-master-server"></a>将目标服务器从主服务器脱离
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主题说明如何通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、[!INCLUDE[tsql](../../includes/tsql_md.md)] 或 SQL Server 管理对象 (SMO) 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中将目标服务器从主服务器脱离。 从目标服务器运行此过程。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要脱离目标服务器，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SMO](#PowerShellProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
若要执行此存储过程，用户必须为 **sysadmin** 固定服务器角色的成员。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>将目标服务器从主服务器脱离  
  
1.  在 **对象资源管理器**中，展开配置为目标服务器的服务器。  
  
2.  右键单击 **“SQL Server 代理”**，指向 **“多服务器管理”**，然后单击 **“脱离”**。  
  
3.  单击 **“是”** 确认要从主服务器脱离此目标服务器。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>将目标服务器从主服务器脱离  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde_md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
```  
sp_msx_defect ;  
```  
  
有关详细信息，请参阅 [sp_msx_defect (Transact-SQL)](http://msdn.microsoft.com/en-us/0dfd963a-3bc5-4b58-94f7-aec976da2883)。  
  
## <a name="PowerShellProcedure"></a>使用 SQL Server 管理对象 (SMO)  
使用 **MsxDefect 方法**。  
  
## <a name="see-also"></a>另请参阅  
[创建多服务器环境](../../ssms/agent/create-a-multiserver-environment.md)  
[企业范围的自动化管理](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[使多台目标服务器脱离主服务器](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  
