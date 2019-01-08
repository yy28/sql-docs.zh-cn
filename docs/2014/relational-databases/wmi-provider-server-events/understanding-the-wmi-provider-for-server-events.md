---
title: 了解服务器事件 WMI 提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- architecture [WMI]
- SQL Server Agent [WMI]
- WMI Provider for Server Events, about WMI Provider for Server Events
ms.assetid: 8fd7bd18-76d0-4b28-8fee-8ad861441ab2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2deedb64e5c8995524978a19b02110a068bde08d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358209"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>了解 WMI Provider for Server Events
  使用服务器事件的 WMI 提供程序，可以使用 Windows Management Instrumentation (WMI) 监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的事件。 该提供程序的运行方式是将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 转换为托管的 WMI 对象。 通过使用该提供程序，WMI 可以利用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中生成事件通知的任何事件。 另外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作为与 WMI 交互的管理应用程序，可以对这些事件做出响应，从而使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理所覆盖的事件范围超过了以前的版本。  
  
 通过发出 WMI 查询语言 (WQL) 语句，诸如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理这样的管理应用程序可以使用 WMI Provider for Server Events 来访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 WQL 是结构化查询语言 (SQL) 的简化子集，它还包含一些特定于 WMI 的扩展。 在使用 WQL 时，应用程序将针对特定数据库或数据库对象来检索事件类型。 WMI Provider for Server Events 会将查询转换成事件通知，实际上就是在目标数据库中创建事件通知。 有关事件通知中的工作原理的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[WMI Provider for Server Events 的概念](https://technet.microsoft.com/library/ms180560.aspx)。 中列出了可以查询事件[WMI Provider for Server Events 类和属性](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)。  
  
 事件发生时触发事件通知将发送一条消息，消息将转到中的预定义的目标服务**msdb**名为**SQL/Notifications/ProcessWMIEventProviderNotification/v1.0**. 该服务将事件放入队列中的预定义**msdb**名为**WMIEventProviderNotificationQueue**。 （上述服务和队列均由提供程序在第一次连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时动态创建。）然后，提供程序从该队列中读取事件数据，并在将它返回到应用程序之前将它转换为托管对象格式 (MOF)。 下图显示了这一过程。  
  
 ![WMI Provider for Server Events 的流程图](../../../2014/database-engine/dev-guide/media/wmi-provider-functional-spec.gif "WMI Provider for Server Events 的流程图")  
  
 例如，请考虑下列 WQL 查询：  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS  
WHERE DatabaseName = 'AdventureWorks'  
```  
  
 在响应该查询时，WMI Provider for Server Events 将在目标数据库中创建等效的事件通知：  
  
```  
USE AdventureWorks ;  
GO  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE  
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',   
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 在该示例中，`SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` 是由前缀 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 GUID 组成的 `SQLWEP_` 标识符。 `SQLWEP` 为每个标识符创建一个新的 GUID。 该值`A7E5521A-1CA6-4741-865D-826F804E5135`中`TO SERVICE`子句是标识中的 broker 实例的 GUID **msdb**数据库。  
  
 有关如何使用 WQL 的详细信息，请参阅[将 wql 与 WMI Provider for Server Events 结合](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)。  
  
 通过连接到由 WMI Provider for Server Events 定义的 WMI 命名空间，管理应用程序将该提供程序定向到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 Windows WMI 服务将此命名空间映射到提供程序 DLL Sqlwep.dll 并将其加载到内存。 提供商管理的 WMI 命名空间的服务器事件的每个实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，，其格式为： \\ \\。\\*根*\Microsoft\SqlServer\ServerEvents\\*instance_name*，其中*instance_name*默认为 MSSQLSERVER。 有关如何连接到的实例的 WMI 命名空间的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[将 wql 与 WMI Provider for Server Events 结合](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)。  
  
 提供程序 DLL Sqlwep.dll 仅会加载一次以载入到服务器操作系统的 WMI 主机服务中，而不管服务器上有多少个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
 有关的示例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理管理应用程序的使用 WMI Provider for Server Events，请参阅[示例：创建 SQL Server 代理警报使用 WMI Provider for Server Events](https://technet.microsoft.com/library/ms186385.aspx)。 有关使用 WMI Provider for Server Events 在托管代码中的管理应用程序示例，请参阅[示例：托管代码使用 WMI 事件提供程序中的](https://technet.microsoft.com/library/ms179315.aspx)。 详细信息，还提供有关中的 WMI [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。  
  
## <a name="see-also"></a>请参阅  
 [WMI Provider for Server Events 的概念](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
