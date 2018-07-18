---
title: 进度报告的数据列 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e71e2e2973d633a6524c8d965b1eaa41c1dac55b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045601"
---
# <a name="progress-reports-data-columns"></a>进度报告数据列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “进度报告”事件类别有以下事件类：  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|5|进度报告开始|进度报告开始。|  
|6|进度报告结束|进度报告结束。|  
|7|进度报告当前状态|进度报告正在运行。|  
|8|进度报告错误|进度报告出错。|  
  
 下表列出了其中每个事件类的数据列。  
  
## <a name="progress-report-begindata-columns"></a>进度报告开始–数据列  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。 下面是有效的“ **子类 ID**: **子类名** ”对：<br /><br /> 1: **Process**<br /><br /> 2: **Merge**<br /><br /> 3: **Delete**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Rebuild**<br /><br /> 6: **Commit**<br /><br /> 7: **Rollback**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transaction**<br /><br /> 12: **Initialize**<br /><br /> 13: **Discretize**<br /><br /> 14: **Query**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Aggregate**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Connecting**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restore**<br /><br /> 39: **Synchronize**<br /><br /> 40: **Build Processing Schedule**<br /><br /> 41: **Detach**<br /><br /> 42: **Attach**<br /><br /> 43: **Analyze\Encode Data**<br /><br /> 44: **Compress Segment**<br /><br /> 45: **Write Table Column**<br /><br /> 46: **Relationship Build Prepare**<br /><br /> 47: **Build Relationship Segment**<br /><br /> 48: **Load**<br /><br /> 49: **Metadata Load**<br /><br /> 50: **Data Load**<br /><br /> 51: **Post Load**<br /><br /> 52: **Metadata traversal during Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Hierarchy processing**<br /><br /> 55: **Switching dictionary**|  
|CurrentTime|2|5|包含所报告事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|作业 ID|7|1|包含与所报告事件关联的作业 ID。|  
|SessionType|8|8|包含与所报告事件关联的会话类型（引起该事件的实体）。 对于正在处理的事件，值可为：<br /><br /> 1= 用户<br /><br /> 2= 主动缓存<br /><br /> 3= 迟缓处理|  
|ObjectID|11|8|包含与所报告事件关联的对象 ID（字符串）。|  
|ObjectType|12|1|包含对象类型。|  
|ObjectName|13|8|包含与所报告事件关联的对象的名称。|  
|ObjectPath|14|8|包含与所报告事件关联的对象的对象路径，形式为以该对象的父级开始的逗号分隔的父级列表。|  
|ObjectReference|15|8|包含所报告事件的对象引用，该引用对于所有父级都以 XML 形式进行编码，并使用标记来描述对象。|  
|ConnectionID|25|1|包含与所报告事件关联的唯一连接 ID。|  
|DatabaseName|28|8|包含发生所报告事件的数据库的名称。|  
|NTUserName|32|8|包含与所报告事件关联的 Windows 用户帐户。|  
|NTDomainName|33|8|包含与所报告事件关联的 Windows 域帐户。|  
|SessionID|39|8|包含与所报告事件关联的会话 ID。|  
|NTCanonicalUserName|40|8|采用规范格式的用户名。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|包含唯一地标识与所报告事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XML for Analysis (XMLA) 所使用的会话 GUID。|  
|TextData|42|9|包含与所报告事件关联的文本数据。|  
|ServerName|43|8|包含其上发生所报告事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
  
## <a name="progress-report-enddata-columns"></a>进度报告结束–数据列  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。 下面是有效的“ **子类 ID**: **子类名** ”对：<br /><br /> 1: **Process**<br /><br /> 2: **Merge**<br /><br /> 3: **Delete**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Rebuild**<br /><br /> 6: **Commit**<br /><br /> 7: **Rollback**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transaction**<br /><br /> 12: **Initialize**<br /><br /> 13: **Discretize**<br /><br /> 14: **Query**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Aggregate**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Connecting**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restore**<br /><br /> 39: **Synchronize**<br /><br /> 40: **Build Processing Schedule**<br /><br /> 41: **Detach**<br /><br /> 42: **Attach**<br /><br /> 43: **Analyze\Encode Data**<br /><br /> 44: **Compress Segment**<br /><br /> 45: **Write Table Column**<br /><br /> 46: **Relationship Build Prepare**<br /><br /> 47: **Build Relationship Segment**<br /><br /> 48: **Load**<br /><br /> 49: **Metadata Load**<br /><br /> 50: **Data Load**<br /><br /> 51: **Post Load**<br /><br /> 52: **Metadata traversal during Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Hierarchy processing**<br /><br /> 55: **Switching dictionary**|  
|CurrentTime|2|5|包含所报告事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|包含事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|包含事件占用的时间量（毫秒）。|  
|CPUTime|6|2|包含事件使用的 CPU 时间量（毫秒）。|  
|作业 ID|7|1|包含与所报告事件关联的作业 ID。|  
|SessionType|8|8|包含与所报告事件关联的会话类型（引起该事件的实体）。 对于正在处理的事件，值可为：<br /><br /> 1= 用户<br /><br /> 2= 主动缓存<br /><br /> 3= 迟缓处理|  
|ProgressTotal|9|1|包含所报告事件的总进度。|  
|IntegerData|10|1|包含与所报告事件关联的整数数据，如正在处理的事件的已处理行数的当前计数。|  
|ObjectID|11|8|包含与所报告事件关联的对象 ID（字符串）。|  
|ObjectType|12|1|包含对象类型。|  
|ObjectName|13|8|包含与所报告事件关联的对象的名称。|  
|ObjectPath|14|8|包含与所报告事件关联的对象的对象路径，形式为以该对象的父级开始的逗号分隔的父级列表。|  
|ObjectReference|15|8|包含所报告事件的对象引用，该引用对于所有父级都以 XML 形式进行编码，并使用标记来描述对象。|  
|Severity|22|1|包含与所报告事件关联的异常的严重级别。 值为：<br /><br /> 0 = 成功<br /><br /> 1 = 信息<br /><br /> 2 = 警告<br /><br /> 3 = 错误|  
|成功|23|1|包含服务器报告事件的成功或失败。 值为：<br /><br /> 0 = 失败<br /><br /> 1 = 成功|  
|错误|24|1|包含给定事件的错误号。|  
|ConnectionID|25|1|包含与所报告事件关联的唯一连接 ID。|  
|DatabaseName|28|8|包含发生所报告事件的数据库的名称。|  
|NTUserName|32|8|包含与所报告事件关联的 Windows 用户帐户。|  
|NTDomainName|33|8|包含与所报告事件关联的 Windows 域帐户。|  
|SessionID|39|8|包含与所报告事件关联的会话 ID。|  
|NTCanonicalUserName|40|8|包含与所报告事件关联的 Windows 用户名。 用户名采用规范格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含唯一地标识与所报告事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XML for Analysis (XMLA) 所使用的会话 GUID。|  
|TextData|42|9|包含与所报告事件关联的文本数据。|  
|ServerName|43|8|包含其上发生所报告事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
  
## <a name="progress-report-currentdata-columns"></a>进度报告当前–数据列  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。 下面是有效的“ **子类 ID**: **子类名** ”对：<br /><br /> 1: **Process**<br /><br /> 2: **Merge**<br /><br /> 3: **Delete**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Rebuild**<br /><br /> 6: **Commit**<br /><br /> 7: **Rollback**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transaction**<br /><br /> 12: **Initialize**<br /><br /> 13: **Discretize**<br /><br /> 14: **Query**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Aggregate**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Connecting**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restore**<br /><br /> 39: **Synchronize**<br /><br /> 40: **Build Processing Schedule**<br /><br /> 41: **Detach**<br /><br /> 42: **Attach**<br /><br /> 43: **Analyze\Encode Data**<br /><br /> 44: **Compress Segment**<br /><br /> 45: **Write Table Column**<br /><br /> 46: **Relationship Build Prepare**<br /><br /> 47: **Build Relationship Segment**<br /><br /> 48: **Load**<br /><br /> 49: **Metadata Load**<br /><br /> 50: **Data Load**<br /><br /> 51: **Post Load**<br /><br /> 52: **Metadata traversal during Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Hierarchy processing**<br /><br /> 55: **Switching dictionary**|  
|CurrentTime|2|5|包含所报告事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|作业 ID|7|1|包含与所报告事件关联的作业 ID。|  
|SessionType|8|8|包含与所报告事件关联的会话类型（引起该事件的实体）。 对于正在处理的事件，值可为：<br /><br /> 1= 用户<br /><br /> 2= 主动缓存<br /><br /> 3= 迟缓处理|  
|ProgressTotal|9|1|包含所报告事件的总进度。|  
|IntegerData|10|1|包含与所报告事件关联的整数数据，如正在处理的事件的已处理行数的当前计数。|  
|ObjectID|11|8|包含与所报告事件关联的对象 ID（字符串）。|  
|ObjectType|12|1|包含对象类型。|  
|ObjectName|13|8|包含与所报告事件关联的对象的名称。|  
|ObjectPath|14|8|包含与所报告事件关联的对象的对象路径，形式为以该对象的父级开始的逗号分隔的父级列表。|  
|ObjectReference|15|8|包含所报告事件的对象引用，该引用对于所有父级都以 XML 形式进行编码，并使用标记来描述对象。|  
|ConnectionID|25|1|包含与所报告事件关联的唯一连接 ID。|  
|DatabaseName|28|8|包含发生所报告事件的数据库的名称。|  
|SessionID|39|8|包含与所报告事件关联的会话 ID。|  
|SPID|41|1|包含唯一地标识与所报告事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XML for Analysis (XMLA) 所使用的会话 GUID。|  
|TextData|42|9|包含与所报告事件关联的文本数据。|  
|ServerName|43|8|包含其上发生所报告事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
  
## <a name="progress-report-errordata-columns"></a>进度报告错误–数据列  
  
|**列名**|**列 ID**|**列类型**|**列说明**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件类用于将事件分类。|  
|EventSubclass|1|1|事件子类提供有关每个事件类的附加信息。 下面是有效的“ **子类 ID**: **子类名** ”对：<br /><br /> 1: **Process**<br /><br /> 2: **Merge**<br /><br /> 3: **Delete**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Rebuild**<br /><br /> 6: **Commit**<br /><br /> 7: **Rollback**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transaction**<br /><br /> 12: **Initialize**<br /><br /> 13: **Discretize**<br /><br /> 14: **Query**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Aggregate**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Connecting**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restore**<br /><br /> 39: **Synchronize**<br /><br /> 40: **Build Processing Schedule**<br /><br /> 41: **Detach**<br /><br /> 42: **Attach**<br /><br /> 43: **Analyze\Encode Data**<br /><br /> 44: **Compress Segment**<br /><br /> 45: **Write Table Column**<br /><br /> 46: **Relationship Build Prepare**<br /><br /> 47: **Build Relationship Segment**<br /><br /> 48: **Load**<br /><br /> 49: **Metadata Load**<br /><br /> 50: **Data Load**<br /><br /> 51: **Post Load**<br /><br /> 52: **Metadata traversal during Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Hierarchy processing**<br /><br /> 55: **Switching dictionary**|  
|CurrentTime|2|5|包含所报告事件（如果有）的当前时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|3|5|包含事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|4|5|包含事件结束的时间。 对指示事件开始的事件类（例如 SQL:BatchStarting 或 SP:Starting）将不填充此列。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|Duration|5|2|包含事件占用的时间量（毫秒）。|  
|作业 ID|7|1|包含与所报告事件关联的作业 ID。|  
|SessionType|8|8|包含与所报告事件关联的会话类型（引起该事件的实体）。 对于正在处理的事件，值可为：<br /><br /> 1= 用户<br /><br /> 2= 主动缓存<br /><br /> 3= 迟缓处理|  
|ProgressTotal|9|1|包含所报告事件的总进度。|  
|IntegerData|10|1|包含与所报告事件关联的整数数据，如正在处理的事件的已处理行数的当前计数。|  
|ObjectID|11|8|包含与所报告事件关联的对象 ID（字符串）。|  
|ObjectType|12|1|包含对象类型。|  
|ObjectName|13|8|包含与所报告事件关联的对象的名称。|  
|ObjectPath|14|8|包含与所报告事件关联的对象的对象路径，形式为以该对象的父级开始的逗号分隔的父级列表。|  
|ObjectReference|15|8|包含所报告事件的对象引用，该引用对于所有父级都以 XML 形式进行编码，并使用标记来描述对象。|  
|Severity|22|1|包含与所报告事件关联的异常的严重级别。 值为：<br /><br /> 0 = 成功<br /><br /> 1 = 信息<br /><br /> 2 = 警告<br /><br /> 3 = 错误|  
|错误|24|1|包含给定事件的错误号。|  
|ConnectionID|25|1|包含与所报告事件关联的唯一连接 ID。|  
|DatabaseName|28|8|包含发生所报告事件的数据库的名称。|  
|SessionID|39|8|包含与所报告事件关联的会话 ID。|  
|SPID|41|1|包含唯一地标识与所报告事件关联的用户会话的服务器进程 ID (SPID)。 SPID 直接对应于 XML for Analysis (XMLA) 所使用的会话 GUID。|  
|TextData|42|9|包含与所报告事件关联的文本数据。|  
|ServerName|43|8|包含其上发生所报告事件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [进度报告事件类别](../../analysis-services/trace-events/progress-reports-event-category.md)  
  
  
