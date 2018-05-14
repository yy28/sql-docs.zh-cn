---
title: DISCOVER_SESSIONS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 986fe462d5582f86fab56a28751b48475cbeb74e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="discoversessions-rowset"></a>DISCOVER_SESSIONS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供在服务器上当前打开的会话的资源使用情况和活动信息。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_SESSIONS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SESSION_COMMAND_COUNT**|**DBTYPE_I4**||自会话开始后开始执行的命令数。|  
|**SESSION_CONNECTION_ID**|**DBTYPE_I4**||会话的连接标识符。|  
|**SESSION_CPU_TIME_MS**|**DBTYPE_UI8**||自会话开始后所有请求占用的 CPU 时间（毫秒）。|  
|**SESSION_CURRENT_DATABASE**|**DBTYPE_WSTR**||当前命令执行正在使用的数据库的名称，或执行的上一个命令使用的数据库的名称。|  
|**SESSION_ELAPSED_TIME_MS**|**DBTYPE_UI8**||自会话开始起经过的时间（毫秒）。|  
|**SESSION_ID**|**DBTYPE_WSTR**||会话的唯一标识符，以 GUID 形式表示。|  
|**SESSION_IDLE_TIME_MS**|**DBTYPE_UI8**||自会话开始后的空闲时间（毫秒）。|  
|**SESSION_LAST_COMMAND**|**DBTYPE_WSTR**||当前正在执行的命令或上次执行的命令的文本。|  
|**SESSION_LAST_COMMAND_CPU_TIME_MS**|**DBTYPE_UI8**||CPU 时间，以毫秒为单位，供**SESSION_LAST_COMMAND**。|  
|**SESSION_LAST_COMMAND_ELAPSED_TIME_MS**|**DBTYPE_UI8**||经过的时间，以毫秒为单位，自启动以来**SESSION_LAST_COMMAND**。|  
|**SESSION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||上次命令执行结束时的 UTC 服务器时间。|  
|**SESSION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||上次命令开始执行时的 UTC 服务器时间。|  
|**SESSION_PROPERTIES**|**DBTYPE_WSTR**||保留供将来使用。|  
|**SESSION_READ_KB**|**DBTYPE_UI8**||自会话开始后从磁盘读取的数据的累计值 (KB)。|  
|**SESSION_READS**|**DBTYPE_UI8**||自会话开始后的累计磁盘读取次数。|  
|**SESSION_SPID**|**DBTYPE_I4**||会话 ID。|  
|**SESSION_START_TIME**|**DBTYPE_DBTIMESTAMP**||会话的启动日期和时间，以服务器上的 UTC 时间表示。|  
|**SESSION_STATUS**|**DBTYPE_I4**||会话的活动状态。<br /><br /> 0 表示“空闲”：当前没有活动正在进行。<br /><br /> 1 表示“活动”：会话正在执行某个请求的任务。<br /><br /> 2 表示“阻塞”：会话正在等待某些资源，以便继续执行挂起的任务。<br /><br /> 3 表示"已取消": 会话已因为取消标记。|  
|**SESSION_USED_MEMORY**|**DBTYPE_I4**||会话当前使用的内存大小 (KB)。 报告的值为按 SPID 划分的 RAM 使用情况，其中可收缩和不可收缩的内存之间没有区别。 与报告有关内存使用情况的其他 DMVS 不同，DISCOVER_SESSIONS 不按类别细分内存使用情况。<br /><br /> 请注意，SESSION_USED_MEMORY 倾向于过低报告实际内存使用情况，因为它不包括多个会话间共享的对象。  只有那些对会话唯一的对象才会在内存计算中出现。|  
|**SESSION_USER_NAME**|**DBTYPE_WSTR**||会话的用户名。|  
|**SESSION_WRITE_KB**|**DBTYPE_UI8**||自会话开始后写入磁盘的数据的累计值 (KB)。|  
|**SESSION_WRITES**|**DBTYPE_UI8**||自会话开始后的累计磁盘写入次数。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_SESSIONS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|SESSION_ID|DBTYPE_WSTR|選擇性。|  
|SESSION_SPID|DBTYPE_I4|選擇性。|  
|SESSION_CONNECTION_ID|DBTYPE_I4|選擇性。|  
|SESSION_USER_NAME|DBTYPE_WSTR|選擇性。|  
|SESSION_CURRENT_DATABASE|DBTYPE_WSTR|選擇性。|  
|SESSION_ELAPSED_TIME_MS|DBTYPE_UI8|選擇性。|  
|SESSION_CPU_TIME_MS|DBTYPE_UI8|選擇性。|  
|SESSION_IDLE_TIME_MS|DBTYPE_UI8|選擇性。|  
|SESSION_STATUS|DBTYPE_I4|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
