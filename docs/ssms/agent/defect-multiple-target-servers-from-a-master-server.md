---
title: 将多个目标服务器与主服务器脱离 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 95170cd480a6efa4a3b37282f65b623c2548d9ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65096725"
---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>Defect Multiple Target Servers from a Master Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使多台目标服务器脱离多服务器管理配置。 从主服务器运行此过程。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>使多台目标服务器脱离主服务器  
  
1.  在对象资源管理器中，展开配置为主服务器的服务器。   
  
2.  右键单击“SQL Server 代理”  ，指向“多服务器管理”  ，再单击“管理目标服务器”  。  
  
3.  单击 **“发布指令”** ，然后在 **“指令类型”** 列表中选择 **“脱离”** 。  
  
4.  在 **“收件人”** 下，执行以下操作之一：  
  
    -   单击 **“所有目标服务器”** ，脱离此主服务器的所有目标服务器。 如果要完全卸载当前多服务器管理配置，则使用此选项。  
  
    -   单击 **“以下目标服务器”** ，再单击相应的 **“选择”** 框，脱离此主服务器的部分（而不是全部）目标服务器。  
  
## <a name="see-also"></a>另请参阅  
[创建多服务器环境](../../ssms/agent/create-a-multiserver-environment.md)  
[企业范围的自动化管理](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Defect a Target Server from a Master Server](../../ssms/agent/defect-a-target-server-from-a-master-server.md)  
  
