---
title: 通知事件数据列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Notification Events event category
ms.assetid: 0ecf06da-1586-415a-9da8-60d4c634f030
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 012eed425161fdf6697fcddc5d1098f5069fcb39
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178597"
---
# <a name="notification-events-data-columns"></a>通知事件数据列
  通知事件指不是由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]用户直接引发的事件。 例如，由于用户更新基础表以便进行主动缓存而发生通知。  
  
 “通知事件”事件类别具有以下事件类：  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|39|通知|通知事件。|  
|40|用户定义|用户定义事件。|  
  
 下表列出了事件类的数据列。  
  
## <a name="notification"></a>通知  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。 以下是有效的子类 Id/子类名称对：<br /><br /> 0：主动缓存开始<br />1：主动缓存结束<br />2：网络流量记录器已启动<br />3：网络流量记录器已停止<br />4：配置属性已更新<br />5：SQL 跟踪<br />6：对象已创建<br />7：对象已删除<br />8：对象已更改<br />9：主动缓存轮询开始<br />10：主动缓存轮询结束<br />11：网络流量记录器快照开始<br />12：网络流量记录器快照结束<br />13：主动缓存：可通知对象已更新<br />14：迟缓处理：开始处理<br />15：迟缓处理：处理完成<br />16：SessionOpened 事件开始<br />17：SessionOpened 事件结束<br />18：SessionClosing 事件开始<br />19：SessionClosing 事件结束<br />20：CubeOpened 事件开始<br />21：CubeOpened 事件结束<br />22：CubeClosing 事件开始<br />23：CubeClosing 事件结束<br />24：已请求事务中止|  
|CurrentTime|2|5|包含通知事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|包含事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|包含事件占用的时间量（毫秒）。|  
|IntegerData|10|1|包含与通知事件相关联的整数数据。 EventSubclass 列为 8 时，取值为：<br /><br /> 1 = 已创建<br /><br /> 2 = 已删除<br /><br /> 3 = 已更改对象的属性<br /><br /> 4 = 已更改对象的子级的属性<br /><br /> 6 = 已添加子级<br /><br /> 7 = 已删除子级<br /><br /> 8 = 完全处理对象<br /><br /> 9 = 部分处理对象<br /><br /> 10 = 未处理对象<br /><br /> 11 = 完全优化对象<br /><br /> 12 = 部分优化对象<br /><br /> 13 = 未优化对象|  
|ObjectID|11|8|包含为其发出此通知的对象 ID；这是一个字符串值。|  
|ObjectType|12|1|包含与通知事件相关联的对象类型。|  
|ObjectName|13|8|包含与通知事件相关联的对象名称。|  
|ObjectPath|14|8|包含与通知事件相关联的对象路径。 路径作为以逗号分隔的父级列表（以该对象的父级开头）返回。|  
|ObjectReference|15|8|包含进度报告结束事件的对象引用。 对象引用由所有父级编码为 XML，方法是使用标记说明对象。|  
|ConnectionID|25|1|包含与通知事件相关联的唯一连接 ID。|  
|DatabaseName|28|8|包含在其中发生通知事件的数据库的名称。|  
|NTUserName|32|8|包含与通知事件相关联的 Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|SessionID|39|8|包含与通知事件相关联的会话 ID。|  
|NTCanonicalUserName|40|8|包含与通知事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一地标识与通知事件相关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与通知事件相关联的文本数据。|  
|ServerName|43|8|包含在其上发生通知事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
|RequestProperties|45|9|包含 XMLA 请求的属性。|  
  
## <a name="user-defined"></a>用户定义  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|提供有关每个事件类的附加信息的特定用户子类。|  
|CurrentTime|2|5|包含通知事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|IntegerData|10|1|特定的用户定义事件信息。|  
|ConnectionID|25|1|包含与通知事件相关联的唯一连接 ID。|  
|DatabaseName|28|8|包含在其中发生通知事件的数据库的名称。|  
|NTUserName|32|8|包含与通知事件相关联的 Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|SessionID|39|8|包含与通知事件相关联的会话 ID。|  
|NTCanonicalUserName|40|8|包含与通知事件相关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一地标识与通知事件相关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XMLA 所使用的会话 GUID。|  
|TextData|42|9|包含与通知事件相关联的文本数据。|  
|ServerName|43|8|包含在其上发生通知事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
  
## <a name="see-also"></a>请参阅  
 [“通知事件”事件类别](notification-events-event-category.md)  
  
  
