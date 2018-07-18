---
title: 命令事件数据列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Command Events event category
ms.assetid: 7169f1e2-c6be-4d8c-b147-25719b84bc2c
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e38ee67b5d8e4f0926ff93c45985b6246d8693f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169528"
---
# <a name="command-events-data-columns"></a>命令事件数据列
  下表列出 **Command Events** 事件类别中的每个事件类的数据列。  
  
 **Command Events** 事件类别包含下列事件类：  
  
-   [Command Begin 类](#bkmk_1)  
  
-   [Command End 类](#bkmk_2)  
  
 下表列出了其中每个事件类的数据列。  
  
##  <a name="bkmk_1"></a> Command Begin 类 - 数据列  
  
|数据列|Description|  
|-----------------|-----------------|  
|ConnectionID|包含与命令事件相关联的唯一连接 ID。|  
|TextData|包含与命令事件相关联的文本数据。|  
|ServerName|包含出现命令事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
|CurrentTime|包含命令事件的当前时间。|  
|DatabaseName|包含正在运行命令的数据库的名称。|  
|EventSubclass|包含命令事件中的事件的类。 值为：<br /><br /> 0：创建<br />1：更改<br />2：删除<br />3：处理<br />4：DesignAggregations<br />5：WBInsert<br />6：WBUpdate<br />7：WBDelete<br />8：备份<br />9：还原<br />10：MergePartitions<br />11：订阅<br />12：批处理<br />13：BeginTransaction<br />14：CommitTransaction<br />15：RollbackTransaction<br />16：GetTransactionState<br />17：取消<br />18：同步<br />19：Import80MiningModels<br />20：附加<br />21：分离<br />22：SetAuthContext<br />23：ImageLoad<br />24：ImageSave<br />10000：其他|  
|NTUserName|包含与命令事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|RequestProperties|包含与命令事件关联的 XML for Analysis (XMLA) 请求属性。|  
|SPID|包含唯一标识与命令事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|StartTime|包含命令事件开始的时间（如果有）。|  
|SessionType|包含导致操作的实体。|  
|NTDomainName|包含与对象权限事件相关联的 Windows 域帐户。|  
|ClientProcessID|包含与命令事件相关联的唯一客户端进程 ID。|  
  
##  <a name="bkmk_2"></a> Command End 类 - 数据列  
  
|数据列|Description|  
|-----------------|-----------------|  
|ConnectionID|包含与命令事件相关联的唯一连接 ID。|  
|TextData|包含与命令事件相关联的文本数据。|  
|ServerName|包含出现命令事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
|CurrentTime|包含命令事件的当前时间。 对于筛选，格式应为 YYYY-MM-DD 和 YYYY-MM-DD HH:MM:SS。|  
|DatabaseName|包含正在运行命令的数据库的名称。|  
|Duration|包含命令开始事件和命令结束事件之间的大概时间。|  
|EndTime|包含命令事件结束的时间。 对于筛选，格式应为 YYYY-MM-DD 和 YYYY-MM-DD HH:MM:SS。|  
|EventSubclass|包含命令事件中的事件的类。 值为：<br /><br /> 0：创建<br />1：更改<br />2：删除<br />3：处理<br />4：DesignAggregations<br />5：WBInsert<br />6：WBUpdate<br />7：WBDelete<br />8：备份<br />9：还原<br />10：MergePartitions<br />11：订阅<br />12：批处理<br />13：BeginTransaction<br />14：CommitTransaction<br />15：RollbackTransaction<br />16：GetTransactionState<br />17：取消<br />18：同步<br />19：Import80MiningModels<br />20：附加<br />21：分离<br />22：SetAuthContext<br />23：ImageLoad<br />24：ImageSave<br />10000：其他|  
|NTCanonicalUserName|包含与命令事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|NTUserName|包含与命令事件关联的 Windows 用户帐户。|  
|SPID|包含唯一标识与命令事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|StartTime|包含命令结束事件开始的时间（如果有）。|  
|CPUTime|包含在命令开始事件与命令结束事件之间的这段时间进程所用的 CPU 时间（毫秒）。|  
|错误|包含与命令事件关联的任意错误的错误号。|  
|Severity|包含与命令事件关联的异常错误的严重级别。 值为：<br /><br /> 0 = 成功<br /><br /> 1 = 信息<br /><br /> 2 = 警告<br /><br /> 3 = 错误|  
|成功|包含命令事件的成功或失败。 值为：<br /><br /> 0 = 失败<br /><br /> 1 = 成功|  
|SessionType|包含导致与命令结束事件关联的操作的实体。|  
|NTDomainName|包含与命令事件关联的 Windows 域帐户。|  
|ClientProcessID|包含与命令事件相关联的唯一客户端进程 ID。|  
  
## <a name="see-also"></a>请参阅  
 [“命令事件”事件类别](command-events-event-category.md)  
  
  
