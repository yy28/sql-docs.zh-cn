---
title: 查询处理事件的数据列 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 81a522bd-440d-406c-a524-3af44a3af101
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 117cab8b57631b1a95dea9baa0e86e918cabf81f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="query-processing-events-data-columns"></a>查询处理事件数据列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “查询处理事件”事件类别具有以下事件类：  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|70|查询多维数据集开始|查询多维数据集开始。|  
|71|查询多维数据集结束|查询多维数据集结束。|  
|72|计算非空开始|计算非空开始。|  
|73|计算非空当前|计算非空当前。|  
|74|计算非空结束|计算非空结束。|  
|75|序列化结果开始|序列化结果开始。|  
|76|序列化结果当前|序列化结果当前。|  
|77|序列化结果结束|序列化结果结束。|  
|78|执行 MDX 脚本开始|执行 MDX 脚本开始。|  
|79|执行 MDX 脚本当前|执行 MDX 脚本当前。 不推荐使用。|  
|80|执行 MDX 脚本结束|执行 MDX 脚本结束。|  
|81|查询维度|查询维度。|  
|11|查询子多维数据集|查询子多维数据集，用于基于使用情况的优化。|  
|12|查询子多维数据集详情|查询子多维数据集的详细信息。 此事件在启用时可能会对性能产生负面影响。|  
|60|从聚合获取数据|通过从聚合获取数据答复查询。 此事件在启用时可能会对性能产生负面影响。|  
|61|从缓存获取数据|通过从某个缓存获取数据答复查询。 此事件在启用时可能会对性能产生负面影响。|  
|82|VertiPaq SE 查询开始|VertiPaq SE 查询|  
|83|VertiPaq SE 查询结束|VertiPaq SE 查询|  
|84|资源使用情况|在命令和查询结束后报告读取、写入和 cpu 使用情况。|  
|85|VertiPaq SE 查询缓存匹配|VertiPaq SE 查询缓存使用|  
|98|直接查询开始|直接查询开始。|  
|99|直接查询结束|直接查询结束。|  
  
 下表列出了其中每个事件类的数据列。  
  
## <a name="query-cube-begin"></a>查询多维数据集开始  
  
|||||  
|-|-|-|-|  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="query-cube-end"></a>查询多维数据集结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="calculate-non-empty-begin"></a>计算非空开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="calculate-non-empty-current"></a>计算非空当前  
  
|||||  
|-|-|-|-|  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1：获取数据<br /><br /> 2：处理计算成员<br /><br /> 3：开机自检顺序|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="calculate-non-empty-end"></a>计算非空结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="serialize-results-begin"></a>序列化结果开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="serialize-results-current"></a>序列化结果当前  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。<br /><br /> 1：序列化轴<br /><br /> 2：序列化单元<br /><br /> 3：序列化 SQL 行集<br /><br /> 4：序列化平展行集|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="serialize-results-end"></a>序列化结果结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="execute-mdx-script-begin"></a>执行 MDX 脚本开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1：MDX 脚本<br /><br /> 2：MDX 脚本命令|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="execute-mdx-script-current"></a>执行 MDX 脚本当前  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="execute-mdx-script-end"></a>执行 MDX 脚本结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1：MDX 脚本<br /><br /> 2：MDX 脚本命令|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="query-dimension"></a>查询维度  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。<br /><br /> 1：缓存数据<br /><br /> 2：非缓存数据|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
|ObjectType|12|1|对象类型。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="query-subcube"></a>查询子多维数据集  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 1：缓存数据<br /><br /> 2：非缓存数据<br /><br /> 3：内部数据<br /><br /> 4：SQL 数据<br /><br /> 11：度量值组结构变化<br /><br /> 12：度量值组删除|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="query-subcube-verbose"></a>查询子多维数据集详情  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 21：缓存数据<br /><br /> 22：非缓存数据<br /><br /> 23：内部数据<br /><br /> 24：SQL 数据|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="get-data-from-aggregation"></a>从聚合获取数据  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="get-data-from-cache"></a>从缓存获取数据  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。<br /><br /> 1：从度量值组缓存中获取数据<br /><br /> 2：从平面缓存中获取数据<br /><br /> 3：从计算缓存中获取数据<br /><br /> 4：从持久缓存中获取数据|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="vertipaq-se-query-begin"></a>VertiPaq SE 查询开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 0：VertiPaq 扫描<br /><br /> 1：表格查询<br /><br /> 2：用户层次结构处理查询<br /><br /> 10：内部 VertiPaq 扫描<br /><br /> 11：内部表格查询<br /><br /> 12：内部用户层次结构处理查询|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ObjectReference|15|8|对象引用。 作为所有父级的 XML 编码，并且使用标记来描述对象。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="vertipaq-se-query-end"></a>VertiPaq SE 查询结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。<br /><br /> 0：VertiPaq 扫描<br /><br /> 1：表格查询<br /><br /> 10：内部 VertiPaq 扫描<br /><br /> 11：内部表格查询|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|ProgressTotal|9|1|总进度。|  
|IntegerData|10|1|整型数据。|  
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
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="resource-usage"></a>资源使用情况  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|ClientProcessID|36|1|客户端应用程序的进程 ID。|  
|ApplicationName|37|8|创建了到服务器连接的客户端应用程序的名称。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="vertipaq-se-query-cache-match"></a>VertiPaq SE 查询缓存匹配  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息：<br /><br /> 0：VertiPaq 缓存精确匹配|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|作业 ID|7|1|进度的作业 ID。|  
|SessionType|8|8|会话类型（导致了操作的实体）。|  
|ObjectID|11|8|对象 ID（请注意这是一个字符串）。|  
|ObjectType|12|1|对象类型。|  
|ObjectName|13|8|对象名。|  
|ObjectPath|14|8|对象路径。 逗号分隔的父级列表，以对象的父级开头。|  
|ObjectReference|15|8|对象引用。 作为所有父级的 XML 编码，并且使用标记来描述对象。|  
|ConnectionID|25|1|唯一的连接 ID。|  
|DatabaseName|28|8|正在运行用户语句的数据库的名称。|  
|NTUserName|32|8|Windows 用户名。|  
|NTDomainName|33|8|用户所属的 Windows 域。|  
|SessionID|39|8|会话 GUID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="direct-query-begin"></a>直接查询开始  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
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
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="direct-query-end"></a>直接查询结束  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|CurrentTime|2|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|事件开始的时间（如果可用）。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|事件占用的时间（毫秒）。|  
|CPUTime|6|2|事件所用的 CPU 时间（毫秒）。|  
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
|SPID|41|1|服务器进程 ID。 该 ID 将唯一标识一个用户会话， 并且直接于 XML/A 使用的会话 GUID 相对应。|  
|TextData|42|9|与事件关联的文本数据。|  
|ServerName|43|8|生成事件的服务器的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [查询处理事件类别](../../analysis-services/trace-events/query-processing-events-category.md)  
  
  
