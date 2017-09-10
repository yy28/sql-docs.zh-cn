---
title: "锁定 Events Data Columns |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c223157f-41a0-405c-bc1a-41c999506936
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9a211ed540b3bddb11c5d84cf0db65ef3dade1ad
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lock-events-data-columns"></a>锁事件数据列
  “锁”事件类别具有以下事件类：  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|50|死锁|有关处于死锁状态的当前锁的信息。|  
|51|锁超时|有关最近超时的锁的信息|  
|52|已获取锁|有关最近获取的锁的信息|  
|53|已释放锁|有关最近释放的锁的信息|  
|54|正在等待的锁|有关正在等待其他锁的锁的信息|  
  
 下表列出了此事件类的数据列。  
  
## <a name="deadlock"></a>死锁  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="lock-timeout"></a>锁超时  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="lock-acquired"></a>已获取锁  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|ClientHostName|35|8|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|ApplicationName|37|8|创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="lock-released"></a>已释放锁  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|ClientHostName|35|8|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|ApplicationName|37|8|创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="lock-waiting"></a>正在等待的锁  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|ClientHostName|35|8|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|ApplicationName|37|8|创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [“锁定事件”类别](../../analysis-services/trace-events/lock-events-category.md)  
  
  
