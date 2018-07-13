---
title: 跟踪和重播事件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eb1d3f67ef90dcadfeb0dc976672af615b4efbba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230687"
---
# <a name="tracing-and-replaying-events"></a>跟踪和重播事件
  在 SMO 中，<xref:Microsoft.SqlServer.Management.Trace> 命名空间中的 `Trace` 和 `Replay` 对象提供对 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 功能（用于监视 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的实例）的编程访问。 您可以捕获有关每个事件的数据并将其保存到文件或表中供以后分析。 例如，可以监视生产环境，了解哪些过程由于执行速度太慢影响了性能。  
  
 `Trace` 和 `Replay` 对象提供一组对象，可用于针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例创建跟踪。 可以在您自己的应用程序中使用这些对象为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 手动创建跟踪。 此外，可以使用 SMO `Trace` 对象读取 SQL 跟踪文件和表，这些文件和表是通过监视 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 或 DTS 日志记录而创建的。  
  
 SMO `Trace` 对象支持您执行以下功能：  
  
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
  
 中的跟踪数据`Trace`并`Replay`对象可以由 SMO 应用程序，或者可以通过使用手动检查[SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)。 跟踪数据也是与兼容[SQL 跟踪](../../sql-trace/sql-trace.md)存储同样提供跟踪功能的过程。  
  
 SMO 跟踪对象驻留在 <xref:Microsoft.SqlServer.Management.Trace> 命名空间中，该命名空间要求引用 Microsoft.SQLServer.ConnectionInfo.dll 文件。  
  
 `Trace`并`Replay`对象要求<xref:Microsoft.SqlServer.Management.Common.ServerConnection><xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>对象，若要使用的实例建立连接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象驻留在 <xref:Microsoft.SqlServer.Management.Common> 命名空间中，该命名空间要求引用 Microsoft.SQLServer.ConnectionInfo.dll 文件。  
  
> [!NOTE]  
>  64 位平台不支持 `Trace` 和 `Replay` 对象。  
  
  
