---
title: DISCOVER_JOBS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e9d0d836d8fe44041aa541d71d86be327647dab9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供有关在服务器上执行的活动作业的信息。 作业是命令的一部分，代表命令执行特定任务。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_JOBS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**JOB_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||创建作业时的服务器 UTC 日期和时间。|  
|**JOB_DESCRIPTION**|**DBTYPE_WSTR**||服务器服务指定的作业说明。|  
|**JOB_EXECUTION_TIME_MS**|**DBTYPE_I8**||作业处于活动状态的时间（毫秒）。|  
|**JOB_ID**|**DBTYPE_I4**||作业的唯一标识符。|  
|**JOB_START_TIME**|**DBTYPE_DBTIMESTAMP**||作业开始时的服务器 UTC 日期和时间。|  
|**JOB_THREADPOOL_ID**|**DBTYPE_I4**||从中启动当前作业的线程池。|  
|**JOB_TOTAL_TIME_MS**|**DBTYPE_I8**||自作业开始起的时间（毫秒）。|  
|**SPID**|**DBTYPE_I4**||会话 ID。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_JOBS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|選擇性。|  
|JOB_ID|DBTYPE_I4|選擇性。|  
|JOB_DESCRIPTION|DBTYPE_WSTR|選擇性。|  
|JOB_THREADPOOL_ID|DBTYPE_I4|選擇性。|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
