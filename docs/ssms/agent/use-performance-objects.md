---
title: 使用性能对象
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ee697990c729a28872f8562241cd5dbfdc3225b2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75257823"
---
# <a name="use-performance-objects"></a>使用性能对象
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理包括用于监视服务执行情况的性能对象和计数器。 这些性能对象使您可以使用性能监视器（一个 Windows 工具）来识别 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务在后台的运行情况。 例如，您可以通过识别 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务当前运行的活动作业数量来找出那些锁定的作业。  
  
计算机上安装的每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例都拥有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务性能对象和计数器。 性能对象是根据每个对象所代表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例来命名的。  
  
下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务性能对象的命名方式：  
  
|实例类型|对象名称|  
|-----------------|---------------|  
|默认|**SQLAgent：** 对象  ：计数器 |  
|已命名|**SQLAgent$**<br /> **&#42;instance_name&#42; ：** 对象  ：计数器 |  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的下列性能对象。  
  
|对象名称|说明|  
|---------------|---------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|已启动作业的相关性能信息、成功率和当前状态|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|作业步骤的相关状态信息|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|警报和通知数的相关信息|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|常规性能信息|  
  
## <a name="see-also"></a>另请参阅  
[监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
[如何启动系统监视器 (Windows)](https://msdn.microsoft.com/5e51bb79-5737-470b-9c47-fac330c001c5)  
  
