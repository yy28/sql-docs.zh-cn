---
title: 单个表快速配置文件窗体（数据事件探查任务）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataprofilingtask.quickprofile.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: d2fac9ce-730e-474e-961a-69406b633778
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5cd76f42424836114bc5b8ed32862d5e1d84869e
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379138"
---
# <a name="single-table-quick-profile-form-data-profiling-task"></a>单个表快速配置文件窗体（数据事件探查任务）
  可以使用 **“单个表快速配置文件窗体”** 快速配置数据事件探查任务，以便使用默认配置对单个表或视图进行事件探查。  
  
 有关如何使用数据事件探查任务的详细信息，请参阅 [设置数据事件探查任务](data-profiling-task.md)。 有关如何使用数据配置文件查看器分析数据事件探查任务输出的详细信息，请参阅 [数据配置文件查看器](data-profile-viewer.md)。  
  
## <a name="options"></a>选项  
 **“连接”**  
 选择使用 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) 的现有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接管理器连接到包含要进行探查的表或视图的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。  
  
 **“表或视图”**  
 选择所选连接管理器连接到的数据库中的现有的表或视图。  
  
 **Compute**  
 选择要计算的配置文件  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**列 Null 比率配置文件**|使用选定表或视图中所有适用列的默认配置来计算列 Null 比率配置文件。<br /><br /> 此配置文件报告选定列中 null 值的百分比。 此配置文件可以帮助您识别数据中的问题，例如，列中 null 值的比率以外偏高。 有关此配置文件设置的详细信息，请参阅[列 Null 比率配置文件请求选项（数据事件探查任务）](column-null-ratio-profile-request-options-data-profiling-task.md)。|  
|**列统计信息配置文件**|使用选定表或视图中所有适用列的默认设置来计算列统计信息配置文件。<br /><br /> 此配置文件报告的统计信息包括：数值列的最小值、最大值、平均值和标准偏差以及 `datetime` 列的最小值和最大值。 此配置文件可以帮助您识别数据中的问题，如无效日期。 有关此配置文件设置的详细信息，请参阅[列统计信息配置文件请求选项（数据事件探查任务）](column-statistics-profile-request-options-data-profiling-task.md)。|  
|**列值分布配置文件**|使用选定表或视图中所有适用列的默认设置来计算列值分布配置文件。<br /><br /> 此配置文件报告选定列中所有的非重复值以及每个值所表示的表中的行的百分比。 还可以报告一些表示该表中的行超过指定百分比的值。 此配置文件可帮助您识别数据中的问题，例如，列中非重复值的数目不正确。 有关此配置文件的详细信息，请参阅[列值分布配置文件请求选项（数据事件探查任务）](column-value-distribution-profile-request-options-data-profiling-task.md)。|  
|**列长度分布配置文件**|使用选定表或视图中所有适用列的默认设置来计算列长度分布配置文件。<br /><br /> 此配置文件报告所选列中字符串值的所有不同长度，以及每个长度表示的表中行的百分比。 此配置文件可以帮助您识别数据中的问题，例如值无效。 有关此配置文件设置的详细信息，请参阅[列长度分布配置文件请求选项（数据事件探查任务）](column-length-distribution-profile-request-options-data-profiling-task.md)。|  
|**列模式配置文件**|使用选定表或视图中所有适用列的默认设置来计算列模式配置文件。<br /><br /> 此配置文件报告涵盖字符串列中值的一组正则表达式。 它还可以帮助您识别数据中的问题，如字符串无效。 它还可以建议可用于以后验证新值的正则表达式。 有关此配置文件设置的详细信息，请参阅[列模式配置文件请求选项（数据事件探查任务）](column-pattern-profile-request-options-data-profiling-task.md)。|  
|**候选键配置文件**|计算列组合的候选键配置文件，该列组合包含的最大列数为 **“最高为 N 列键”** 中指定的列数。<br /><br /> 此配置文件报告某个列或列集是否适于用作选定表的键。 此配置文件还可以帮助您识别数据中的问题，如可能的键列中的重复值。 有关此配置文件设置的详细信息，请参阅[候选键配置文件请求选项（数据事件探查任务）](candidate-key-profile-request-options-data-profiling-task.md)。|  
|**“最高为 N 列键”**|选择最大列数，以可能的组合作为表或视图的键进行测试。 默认值为 1。 最大值为 1000。 例如，选择 3 测试一列、两列以及三列键组合。|  
|**函数依赖关系配置文件**|计算决定列组合的函数依赖关系配置文件，决定列组合包括的最大列数为 **“与决定列一样最多 N 列”** 中指定的列数。<br /><br /> 此配置文件报告某列（依赖列）中的值依赖另一列或列集（决定列）中的值的程度。 此配置文件还可以帮助您识别数据中的问题，如无效值。 有关此配置文件设置的详细信息，请参阅[函数依赖关系配置文件请求选项（数据事件探查任务）](functional-dependency-profile-request-options-data-profiling-task.md)。|  
|**“与决定列一样最多 N 列”**|选择最大列数，以可能的组合作为决定列进行测试。 默认值为 1。 最大值为 1000。 例如，选择 2 可对具有以下特点的组合进行测试：单个列或两个列组合为另一个（依赖）列的决定列。|  
  
> [!NOTE]  
>  值包含配置文件类型在“单个表快速配置文件窗体”中不可用。  
  
## <a name="see-also"></a>请参阅  
 [数据事件探查任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)   
 [数据事件探查任务编辑器（“配置文件请求”页）](data-profiling-task-editor-profile-requests-page.md)  
  
  
