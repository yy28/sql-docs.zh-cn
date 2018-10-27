---
title: Profiler 跟踪为重播创建 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- replaying queries
- replaying discovers
- events [Analysis Services]
- replaying commands
- Profiler [SQL Server Profiler], Analysis Services
- performance [Analysis Services], replays
- traces [Analysis Services]
ms.assetid: 93b2fc46-7cfb-4ab5-abeb-1475a7d6f0f2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3522ec98cb4a4c6260de48f500e9b331594eb53
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145032"
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>为重播创建事件探查器跟踪 (Analysis Services)
  若要重播用户提交到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 必须收集所需的事件。 为了启动这些事件的集合，必须在 **“跟踪属性”** 对话框的 **“事件选择”** 选项卡中选择相应的事件类。 例如，如果选择了 Query Begin 事件类，则将收集包含查询的事件，并将其用于重播。 此外，跟踪文件还包含足够的信息，以支持在分布式环境中以原始顺序重播服务器事务。  
  
## <a name="replay-for-queries"></a>重播查询  
 若要重播查询， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 必须捕获下列事件：  
  
-   Audit Login 事件类及其所有数据列。 此事件类提供有关登录的用户以及会话设置的信息。 服务器进程 ID (SPID) 提供对用户会话的引用。 有关详细信息，请参阅 [Security Audit Data Columns](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns)。  
  
-   Query Begin 事件类及其所有数据列。 此事件类提供有关提交给 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的查询的信息。 事件子类列提供有关查询类型的信息。 TextData 列提供查询的实际文本。 RequestParameters 列提供参数化查询的参数，RequestProperties 列提供 XML for Analysis (XMLA) 请求的属性。 有关详细信息，请参阅 [Queries Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns)。  
  
-   Query End 事件类及其所有数据列。 此事件类验证查询执行的状态。 有关详细信息，请参阅 [Queries Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns)。  
  
## <a name="replay-for-discovers"></a>重播发现  
 若要重播发现， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 必须捕获下列事件：  
  
-   Audit Login 事件类及其所有数据列。 此事件类提供有关登录的用户以及会话设置的信息。 SPID 提供对用户会话的引用。 有关详细信息，请参阅 [Security Audit Data Columns](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns)。  
  
-   Discover Begin 事件类及其所有数据列。 TextData 列提供\<RequestType > 部分 discover 请求和 RequestProperties 列提供\<属性 > 发现请求的部分。 EventSubclass 列提供发现类型。 有关详细信息，请参阅 [Discover Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns)。  
  
-   Discover End 事件类及其所有数据列。 此事件类验证发现请求的状态。 有关详细信息，请参阅 [Discover Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns)。  
  
## <a name="replay-for-commands"></a>重播命令  
 若要重播命令， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 必须捕获下列事件：  
  
-   Command Begin 事件类及其所有数据列。 TextData 列提供有关命令的详细信息，如进程类型、数据库 ID 和多维数据集 ID。 RequestParameters 列提供参数化命令的参数，RequestProperties 列提供 XMLA 请求的属性。 有关详细信息，请参阅 [Command Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns)。  
  
-   Command End 事件类及其所有数据列。 此事件类验证命令的状态。 有关详细信息，请参阅 [Command Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns)。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 跟踪事件](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [通过 SQL Server Profiler 监视 Analysis Services 简介](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
