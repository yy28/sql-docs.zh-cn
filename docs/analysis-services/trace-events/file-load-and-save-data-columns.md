---
title: "文件加载和保存的数据列 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 0101e809-d6ea-4d0c-95ec-65dd77acf665
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2e711c51d3a6d8cae4fc437c9b9f6f0bc758c899
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="file-load-and-save-data-columns"></a>文件加载和保存数据列
  “文件加载和保存”事件类别具有以下事件类：  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|90|文件加载开始|文件加载开始。|  
|91|文件加载结束|文件加载结束。|  
|92|文件保存开始|文件保存开始。|  
|93|文件保存结束|文件保存结束|  
|94|PageOut 开始|PageOut 开始。|  
|95|PageOut 结束|PageOut 结束|  
|96|PageIn 开始|PageIn 开始。|  
|97|PageIn 结束|PageIn 结束|  
  
 下表列出了此事件类的数据列。  
  
## <a name="file-load-begin"></a>文件加载开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|SessionID|39|8|会话 GUID。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="file-load-end"></a>文件加载结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|IntegerData|10|1|整型数据。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|Severity|22|1|异常的严重级别。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|错误|24|1|给定事件的错误号。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|SessionID|39|8|会话 GUID。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="file-save-begin"></a>文件保存开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|SessionID|39|8|会话 GUID。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="file-save-end"></a>文件保存结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|IntegerData|10|1|整型数据。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|Severity|22|1|异常的严重级别。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|错误|24|1|给定事件的错误号。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|SessionID|39|8|会话 GUID。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="pageout-begin"></a>PageOut 开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|SessionID|39|8|会话 GUID。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="pageout-end"></a>PageOut 结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|IntegerData|10|1|整型数据。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|Severity|22|1|异常的严重级别。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|错误|24|1|给定事件的错误号。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|SessionID|39|8|会话 GUID。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="pagein-begin"></a>PageIn 开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|SessionID|39|8|会话 GUID。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="pagein-end"></a>PageIn 结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|IntegerData|10|1|整型数据。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|Severity|22|1|异常的严重级别。|  
|成功|23|1|1 = 成功。 0 = 失败（例如，1 表示权限检查成功，0 表示该检查失败）。|  
|错误|24|1|给定事件的错误号。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|SessionID|39|8|会话 GUID。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [“文件加载和保存事件”类别](../../analysis-services/trace-events/file-load-and-save-event-category.md)  
  
  
