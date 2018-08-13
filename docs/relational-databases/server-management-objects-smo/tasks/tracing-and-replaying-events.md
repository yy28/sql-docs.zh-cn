---
title: 跟踪和重播事件 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 03086e17c8d104792187b801b10abf15204f3643
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39543577"
---
# <a name="tracing-and-replaying-events"></a>跟踪和重播事件
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 SMO 中，**跟踪**并**重播**中的对象<xref:Microsoft.SqlServer.Management.Trace>命名空间提供以编程方式访问[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]功能，用于监视实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 您可以捕获有关每个事件的数据并将其保存到文件或表中供以后分析。 例如，可以监视生产环境，了解哪些过程由于执行速度太慢影响了性能。  
  
 **跟踪**并**重播**对象提供了一组可用于创建跟踪的实例上的对象[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 可以在您自己的应用程序中使用这些对象为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 手动创建跟踪。 此外，SMO**跟踪**对象可以用于读取 SQL 跟踪文件和表创建的监视[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，或 DTS 日志记录。  
  
 SMO**跟踪**对象，只需执行以下功能：  
  
-   创建跟踪。  
  
-   设置跟踪筛选器。  
  
-   设置正在跟踪的事件。  
  
-   停止或启动跟踪。  
  
-   读取跟踪文件和跟踪表。  
  
-   获取有关跟踪中的事件的信息。  
  
-   获取有关跟踪中的筛选器的信息。  
  
-   以编程方式操作跟踪数据。  
  
-   写入跟踪表和跟踪文件。  
  
-   重播跟踪文件或跟踪表。  
  
 中的跟踪数据**跟踪**并**重播**对象可以由 SMO 应用程序，或者可以通过使用手动检查[SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)。 跟踪数据也是与兼容[SQL 跟踪](../../../relational-databases/sql-trace/sql-trace.md)存储同样提供跟踪功能的过程。  
  
 SMO 跟踪对象驻留在 <xref:Microsoft.SqlServer.Management.Trace> 命名空间中，该命名空间要求引用 Microsoft.SQLServer.ConnectionInfo.dll 文件。  
  
 **跟踪**并**重播**对象需要[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>要使用的实例建立连接对象[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)对象驻留在[Microsoft.SqlServer.Management.Common](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common)命名空间，这要求引用 Microsoft.SQLServer.ConnectionInfo.dll 文件。  
  
> [!NOTE]  
>  **跟踪**并**重播**64 位平台上不支持对象。  
  
  
