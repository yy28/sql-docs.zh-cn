---
title: Security Audit Data Columns |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e9d7673479d9c536d85d98ea26cef08fc01acd96
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="security-audit-data-columns"></a>安全审核数据列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “安全审核”事件类别具有以下事件类：  
  
||||  
|-|-|-|  
|**事件 ID**|**事件名称**|**事件说明**|  
|1|审核登录|收集从开始跟踪之后发生的所有新连接事件，如客户端请求与正在运行 SQL Server 实例的服务器进行连接。|  
|2|审核注销|收集从开始跟踪之后发生的所有新断开连接事件，如客户端发出一个断开连接命令即属于一个断开连接事件。|  
|4|审核服务器启动和停止|记录服务关闭、启动和暂停活动。|  
|18|审核对象权限事件|记录对象权限更改。|  
|19|审核管理操作事件|记录服务器备份/还原/同步/附加/分离/图像加载/图像保存。|  
  
 下表列出了其中每个事件类的数据列。  
  
## <a name="audit-login"></a>审核登录  
  
|||||  
|-|-|-|-|  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Severity|22|1|异常的严重级别。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|错误|24|1|给定事件的错误号。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|ClientHostName|35|8|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|ApplicationName|37|8|创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="audit-logout"></a>审核注销  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|ClientHostName|35|8|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|ApplicationName|37|8|创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="audit-server-starts-and-stops"></a>审核服务器启动和停止  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1：实例已关闭<br /><br /> 2：实例已启动<br /><br /> 3：实例已暂停<br /><br /> 4：实例已继续|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Severity|22|1|异常的严重级别。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|错误|24|1|给定事件的错误号。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="audit-object-permission-event"></a>审核对象权限事件  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ObjectReference|15|8|对象引用。 作为所有父级的 XML 编码，并且使用标记来描述对象。|  
|Severity|22|1|异常的严重级别。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|错误|24|1|给定事件的错误号。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
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
  
## <a name="audit-admin-operations-event"></a>审核管理操作事件  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1： **备份**<br /><br /> 2： **还原**<br /><br /> 3： **同步**<br /><br /> 4： **分离**<br /><br /> 5： **附加**<br /><br /> 6： **ImageLoad**<br /><br /> 7： **ImageSave**|  
|Severity|22|1|异常的严重级别。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|错误|24|1|给定事件的错误号。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
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
 [“安全审核”事件类别](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  
