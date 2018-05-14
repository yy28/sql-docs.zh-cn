---
title: 发现服务器状态事件数据列 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: af00bfd3d38f7014efaa04037ffdd0754165e232
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="discover-server-state-events-data-columns"></a>发现服务器状态事件数据列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “发现服务器状态”事件类别具有以下事件类：  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|33|服务器状态发现开始|服务器状态发现的开始。|  
|34|服务器状态发现数据|服务器状态发现响应的内容。|  
|35|服务器状态发现结束|服务器状态发现的结束。|  
  
 下表列出了其中每个事件类的数据列。  
  
## <a name="server-state-discover-begin-classdata-columns"></a>服务器状态发现开始类 - 数据列  
  
|||||  
|-|-|-|-|  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1： **DISCOVER_CONNECTIONS**<br /><br /> 2： **DISCOVER_SESSIONS**<br /><br /> 3： **DISCOVER_TRANSACTIONS**<br /><br /> 6： **DISCOVER_DB_CONNECTIONS**<br /><br /> 7： **DISCOVER_JOBS**<br /><br /> 8： **DISCOVER_LOCKS**<br /><br /> 12： **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13： **DISCOVER_MEMORYUSAGE**<br /><br /> 14： **DISCOVER_JOB_PROGRESS**<br /><br /> 15： **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|包含服务器状态发现事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|ConnectionID|25|1|包含与服务器状态发现事件关联的唯一连接 ID。|  
|NTUserName|32|8|包含与服务器状态发现事件关联的 Windows 用户帐户。|  
|NTDomainName|33|8|包含与服务器状态发现事件关联的 Windows 域帐户。|  
|ClientProcessID|36|1|包含创建了到服务器连接的客户端应用程序的进程 ID。|  
|ApplicationName|37|8|包含创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|包含与服务器状态发现事件关联的会话 ID。|  
|NTCanonicalUserName|40|8|包含与服务器状态发现事件关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一地标识与服务器状态发现事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与事件关联的文本数据。|  
|ServerName|43|8|包含发生服务器状态发现事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
|RequestProperties|45|9|包含当前 XMLA 请求的属性。|  
  
## <a name="server-state-discover-data-classdata-columns"></a>服务器状态发现数据类 - 数据列  
  
|||||  
|-|-|-|-|  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1： **DISCOVER_CONNECTIONS**<br /><br /> 2： **DISCOVER_SESSIONS**<br /><br /> 3： **DISCOVER_TRANSACTIONS**<br /><br /> 6： **DISCOVER_DB_CONNECTIONS**<br /><br /> 7： **DISCOVER_JOBS**<br /><br /> 8： **DISCOVER_LOCKS**<br /><br /> 12： **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13： **DISCOVER_MEMORYUSAGE**<br /><br /> 14： **DISCOVER_JOB_PROGRESS**<br /><br /> 15： **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|包含服务器状态发现事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|ConnectionID|25|1|包含与服务器状态发现事件关联的唯一连接 ID。|  
|SessionID|39|8|包含与服务器状态发现事件关联的会话 ID。|  
|SPID|41|1|包含唯一地标识与服务器状态发现事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与服务器对发现请求的响应关联的文本数据。|  
|ServerName|43|8|包含发生服务器状态发现事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
  
## <a name="server-state-discover-end-classdata-columns"></a>服务器状态发现结束类 - 数据列  
  
|||||  
|-|-|-|-|  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1： **DISCOVER_CONNECTIONS**<br /><br /> 2： **DISCOVER_SESSIONS**<br /><br /> 3： **DISCOVER_TRANSACTIONS**<br /><br /> 6： **DISCOVER_DB_CONNECTIONS**<br /><br /> 7： **DISCOVER_JOBS**<br /><br /> 8： **DISCOVER_LOCKS**<br /><br /> 12： **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13： **DISCOVER_MEMORYUSAGE**<br /><br /> 14： **DISCOVER_JOB_PROGRESS**<br /><br /> 15： **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|包含服务器状态发现事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|包含事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|包含事件占用的时间量（毫秒）。|  
|CPUTime|6|2|包含服务器状态发现事件所使用的 CPU 时间量（毫秒）。|  
|ConnectionID|25|1|包含与服务器状态发现事件关联的唯一连接 ID。|  
|NTUserName|32|8|包含与服务器状态发现事件关联的 Windows 用户帐户。|  
|NTDomainName|33|8|包含与服务器状态发现事件关联的 Windows 域帐户。|  
|ClientProcessID|36|1|包含启动了 XMLA 请求的客户端应用程序的进程 ID。|  
|ApplicationName|37|8|包含创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|包含与服务器状态发现事件关联的 Windows 域帐户。|  
|NTCanonicalUserName|40|8|包含与服务器状态发现事件关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一地标识与服务器状态发现事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与服务器对发现请求的响应关联的文本数据。|  
|ServerName|43|8|包含发生服务器状态发现事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [发现服务器状态事件类别](../../analysis-services/trace-events/discover-server-state-event-category.md)  
  
  
