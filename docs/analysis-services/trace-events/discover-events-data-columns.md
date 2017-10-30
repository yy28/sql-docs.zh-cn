---
title: "发现事件数据列 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Discover Events event category
ms.assetid: 10ec598e-5b51-4767-b4f7-42e261d96a40
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1d4275dc8ed85c907a458c5772a57153dc88fa0e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="discover-events-data-columns"></a>发现事件数据列
  “发现事件”类别具有以下事件类：  
  
-   发现开始类  
  
-   发现结束类  
  
 下表列出了其中每个事件类的数据列。  
  
## <a name="discover-begin-classdata-columns"></a>发现开始类 — 数据列  
  
|||||  
|-|-|-|-|  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。  下面是有效的 **子类 ID**/**子类名** 值对：<br /><br /> 0: DBSCHEMA_CATALOGS<br /><br /> 1: DBSCHEMA_TABLES<br /><br /> 2: DBSCHEMA_COLUMNS<br /><br /> 3: DBSCHEMA_PROVIDER_TYPES<br /><br /> 4: MDSCHEMA_CUBES<br /><br /> 5: MDSCHEMA_DIMENSIONS<br /><br /> 6: MDSCHEMA_HIERARCHIES<br /><br /> 7: MDSCHEMA_LEVELS<br /><br /> 8: MDSCHEMA_MEASURES<br /><br /> 9: MDSCHEMA_PROPERTIES<br /><br /> 10: MDSCHEMA_MEMBERS<br /><br /> 11: MDSCHEMA_FUNCTIONS<br /><br /> 12: MDSCHEMA_ACTIONS<br /><br /> 13: MDSCHEMA_SETS<br /><br /> 14: DISCOVER_INSTANCES<br /><br /> 15: MDSCHEMA_KPIS<br /><br /> 16: MDSCHEMA_MEASUREGROUPS<br /><br /> 17: MDSCHEMA_COMMANDS<br /><br /> 18: DMSCHEMA_MINING_SERVICES<br /><br /> 19: DMSCHEMA_MINING_SERVICE_PARAMETERS<br /><br /> 20: DMSCHEMA_MINING_FUNCTIONS<br /><br /> 21: DMSCHEMA_MINING_MODEL_CONTENT<br /><br /> 22: DMSCHEMA_MINING_MODEL_XML<br /><br /> 23: DMSCHEMA_MINING_MODELS<br /><br /> 24: DMSCHEMA_MINING_COLUMNS<br /><br /> 25: DISCOVER_DATASOURCES<br /><br /> 26: DISCOVER_PROPERTIES<br /><br /> 27: DISCOVER_SCHEMA_ROWSETS<br /><br /> 28: DISCOVER_ENUMERATORS<br /><br /> 29: DISCOVER_KEYWORDS<br /><br /> 30: DISCOVER_LITERALS<br /><br /> 31: DISCOVER_XML_METADATA<br /><br /> 32: DISCOVER_TRACES<br /><br /> 33: DISCOVER_TRACE_DEFINITION_PROVIDERINFO<br /><br /> 34: DISCOVER_TRACE_COLUMNS<br /><br /> 35: DISCOVER_TRACE_EVENT_CATEGORIES<br /><br /> 36: DMSCHEMA_MINING_STRUCTURES<br /><br /> 37: DMSCHEMA_MINING_STRUCTURE_COLUMNS<br /><br /> 38: DISCOVER_MASTER_KEY<br /><br /> 39: MDSCHEMA_INPUT_DATASOURCES<br /><br /> 40: DISCOVER_LOCATIONS<br /><br /> 41: DISCOVER_PARTITION_DIMENSION_STAT<br /><br /> 42: DISCOVER_PARTITION_STAT<br /><br /> 43: DISCOVER_DIMENSION_STAT<br /><br /> 44: MDSCHEMA_MEASUREGROUP_DIMENSIONS<br /><br /> 49: DISCOVER_XEVENT_TRACE_DEFINITION|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|ConnectionID|25|1|包含与发现事件相关联的唯一连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTUserName|32|8|包含与发现事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|NTDomainName|33|8|包含与发现事件相关联的 Windows 域。|  
|ClientProcessID|36|1|包含客户端应用程序的进程 ID。|  
|ApplicationName|37|8|创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|包含与发现事件相关联的会话 ID。|  
|NTCanonicalUserName|40|8|包含与发现事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一标识与发现事件相关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与事件关联的文本数据。|  
|ServerName|43|8|包含在其上发生发现事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
|RequestProperties|45|9|包含与发现事件相关联的 XML for Analysis (XMLA) 请求属性。|  
  
## <a name="discover-end-classdata-columns"></a>发现结束类 — 数据列  
  
|||||  
|-|-|-|-|  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|EventClass|0|1|包含事件类；事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。 下面是有效的 **子类 ID**/**子类名** 值对：<br /><br /> 0: DBSCHEMA_CATALOGS<br /><br /> 1: DBSCHEMA_TABLES<br /><br /> 2: DBSCHEMA_COLUMNS<br /><br /> 3: DBSCHEMA_PROVIDER_TYPES<br /><br /> 4: MDSCHEMA_CUBES<br /><br /> 5: MDSCHEMA_DIMENSIONS<br /><br /> 6: MDSCHEMA_HIERARCHIES<br /><br /> 7: MDSCHEMA_LEVELS<br /><br /> 8: MDSCHEMA_MEASURES<br /><br /> 9: MDSCHEMA_PROPERTIES<br /><br /> 10: MDSCHEMA_MEMBERS<br /><br /> 11: MDSCHEMA_FUNCTIONS<br /><br /> 12: MDSCHEMA_ACTIONS<br /><br /> 13: MDSCHEMA_SETS<br /><br /> 14: DISCOVER_INSTANCES<br /><br /> 15: MDSCHEMA_KPIS<br /><br /> 16: MDSCHEMA_MEASUREGROUPS<br /><br /> 17: MDSCHEMA_COMMANDS<br /><br /> 18: DMSCHEMA_MINING_SERVICES<br /><br /> 19: DMSCHEMA_MINING_SERVICE_PARAMETERS<br /><br /> 20: DMSCHEMA_MINING_FUNCTIONS<br /><br /> 21: DMSCHEMA_MINING_MODEL_CONTENT<br /><br /> 22: DMSCHEMA_MINING_MODEL_XML<br /><br /> 23: DMSCHEMA_MINING_MODELS<br /><br /> 24: DMSCHEMA_MINING_COLUMNS<br /><br /> 25: DISCOVER_DATASOURCES<br /><br /> 26: DISCOVER_PROPERTIES<br /><br /> 27: DISCOVER_SCHEMA_ROWSETS<br /><br /> 28: DISCOVER_ENUMERATORS<br /><br /> 29: DISCOVER_KEYWORDS<br /><br /> 30: DISCOVER_LITERALS<br /><br /> 31: DISCOVER_XML_METADATA<br /><br /> 32: DISCOVER_TRACES<br /><br /> 33: DISCOVER_TRACE_DEFINITION_PROVIDERINFO<br /><br /> 34: DISCOVER_TRACE_COLUMNS<br /><br /> 35: DISCOVER_TRACE_EVENT_CATEGORIES<br /><br /> 36: DMSCHEMA_MINING_STRUCTURES<br /><br /> 37: DMSCHEMA_MINING_STRUCTURE_COLUMNS<br /><br /> 38: DISCOVER_MASTER_KEY<br /><br /> 39: MDSCHEMA_INPUT_DATASOURCES<br /><br /> 40: DISCOVER_LOCATIONS<br /><br /> 41: DISCOVER_PARTITION_DIMENSION_STAT<br /><br /> 42: DISCOVER_PARTITION_STAT<br /><br /> 43: DISCOVER_DIMENSION_STAT<br /><br /> 44: MDSCHEMA_MEASUREGROUP_DIMENSIONS<br /><br /> 49: DISCOVER_XEVENT_TRACE_DEFINITION|  
|CurrentTime|2|5|包含发现事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含发现结束事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|包含事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|包含发现事件占用的时间量的近似值（毫秒）。|  
|CPUTime|6|2|包含事件使用的 CPU 时间量（毫秒）。|  
|Severity|22|1|包含异常的严重级别。|  
|成功|23|1|包含发现事件的成功或失败。 值为：<br /><br /> 0 = 失败<br /><br /> 1 = 成功|  
|错误|24|1|包含与发现事件相关联的任何错误的错误号。|  
|ConnectionID|25|1|包含与发现事件相关联的唯一连接 ID。|  
|DatabaseName|28|8|包含发生发现事件的数据库的名称。|  
|NTUserName|32|8|包含与对象权限事件相关联的 Windows 用户名。|  
|NTDomainName|33|8|包含与发现事件相关联的 Windows 域帐户。|  
|ClientProcessID|36|1|包含启动了事件的应用程序的客户端进程 ID。|  
|ApplicationName|37|8|包含创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|包含与发现事件相关联的会话 ID。|  
|NTCanonicalUserName|40|8|包含与对象权限事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一标识与发现结束事件相关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与事件关联的文本数据。|  
|ServerName|43|8|包含在其上发生发现事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
|RequestProperties|45|9|包含 XMLA 请求的属性。|  
  
## <a name="see-also"></a>另请参阅  
 [Discover Events Event Category](../../analysis-services/trace-events/discover-events-event-category.md)  
  
  

