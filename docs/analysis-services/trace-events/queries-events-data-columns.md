---
title: 查询事件数据列 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf039252c6a2f76a1d4e38af6766ebf811ac33d1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="queries-events-data-columns"></a>查询事件数据列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “查询事件”事件类别具有以下事件类：  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|9|查询开始|查询开始。|  
|10|查询结束|查询结束。|  
  
 下表列出了其中每个事件类的数据列。  
  
## <a name="query-begin-classdata-columns"></a>查询开始类 — 数据列  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|包含事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|ConnectionID|25|1|包含与查询事件相关联的唯一连接 ID。|  
|DatabaseName|28|8|包含正在运行查询的数据库的名称。|  
|NTUserName|32|8|包含与查询事件相关联的 Windows 用户名。|  
|NTDomainName|33|8|包含与查询事件相关联的 Windows 域帐户。|  
|ClientProcessID|36|1|包含客户端应用程序的进程 ID。|  
|ApplicationName|37|8|包含创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|包含 XMLA 请求的会话唯一 ID。|  
|NTCanonicalUserName|40|8|包含与查询事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一地标识与查询事件相关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与查询事件相关联的文本数据。|  
|ServerName|43|8|包含其上发生查询事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
|RequestParameters|44|9|包含与查询事件相关联的参数化查询和命令的参数。|  
|RequestProperties|45|9|包含 XMLA 请求的属性。|  
  
## <a name="query-end-classdata-columns"></a>查询结束类 — 数据列  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|包含事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|包含事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|包含事件所用的时间（毫秒）。|  
|CPUTime|6|2|包含事件使用的 CPU 时间量（毫秒）。|  
|Severity|22|1|包含与查询事件相关联的异常的严重级别。 值为：<br /><br /> 0 = 成功<br /><br /> 1 = 信息<br /><br /> 2 = 警告<br /><br /> 3 = 错误|  
|成功|23|1|包含查询事件的成功或失败。 值为：<br /><br /> 0 = 失败<br /><br /> 1 = 成功|  
|错误|24|1|包含与查询事件相关联的任何错误的错误号。|  
|ConnectionID|25|1|包含与查询事件相关联的唯一连接 ID。|  
|DatabaseName|28|8|包含正在运行查询的数据库的名称。|  
|NTUserName|32|8|包含与查询事件相关联的 Windows 用户名。|  
|NTDomainName|33|8|包含与查询事件相关联的 Windows 域帐户。|  
|ClientProcessID|36|1|包含客户端应用程序的进程 ID。|  
|ApplicationName|37|8|包含创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|包含 XMLA 请求的会话唯一 ID。|  
|NTCanonicalUserName|40|8|包含与查询事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一地标识与查询事件相关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与查询事件相关联的文本数据。|  
|ServerName|43|8|包含其上发生查询事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [查询事件类别](../../analysis-services/trace-events/queries-events-category.md)  
  
  
