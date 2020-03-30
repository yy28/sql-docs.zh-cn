---
title: 将目标服务器从主服务器脱离
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e61c18fc2312fc3b04569f6a6d536ce077c4c35e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252130"
---
# <a name="defect-a-target-server-from-a-master-server"></a>将目标服务器从主服务器脱离
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题说明如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server 管理对象 (SMO) 从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的主服务器脱离目标服务器。 从目标服务器运行此过程。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>开始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
若要执行此存储过程，用户必须为 **sysadmin** 固定服务器角色的成员。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>将目标服务器从主服务器脱离  
  
1.  在 **对象资源管理器**中，展开配置为目标服务器的服务器。  
  
2.  右键单击 **“SQL Server 代理”** ，指向 **“多服务器管理”** ，然后单击 **“脱离”** 。  
  
3.  单击 **“是”** 确认要从主服务器脱离此目标服务器。  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>将目标服务器从主服务器脱离  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
```  
sp_msx_defect ;  
```  
  
有关详细信息，请参阅 [sp_msx_defect (Transact-SQL)](https://msdn.microsoft.com/0dfd963a-3bc5-4b58-94f7-aec976da2883)。  
  
## <a name="using-sql-server-management-objects-smo"></a><a name="PowerShellProcedure"></a>使用 SQL Server 管理对象 (SMO)  
使用 **MsxDefect 方法**。  
  
## <a name="see-also"></a>另请参阅  
[创建多服务器环境](../../ssms/agent/create-a-multiserver-environment.md)  
[企业范围的自动化管理](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[将多台目标服务器从主服务器脱离](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  
