---
title: 列值分布配置文件请求选项（数据事件探查任务）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c1e5f5de-04f5-4d00-a9f0-55817186bdf9
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 28489dd837b9b7c3c93928e98cebb8335079a155
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="column-value-distribution-profile-request-options-data-profiling-task"></a>列值分布配置文件请求选项（数据事件探查任务）
  可以使用 **“配置文件请求”** 页的 **“请求属性”** 窗格，为请求窗格中选定的 **“列值分布配置文件请求”** 设置选项。 列值分布配置文件将报告选定列中的所有非重复值以及表中每个值表示的行的百分比。 该配置文件还可以报告其表示内容超过表中指定的行百分比的值。 此配置文件可帮助您识别数据中的问题，例如，列中非重复值的数目不正确。 例如，对表示美国州的列进行事件探查，发现有 50 多个非重复值。  
  
> [!NOTE]  
>  本主题中介绍的选项显示在 **“数据事件探查任务编辑器”** 的 **“配置文件请求”**页中。 有关此编辑器页的详细信息，请参阅[数据事件探查任务编辑器（“配置文件请求”页）](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 有关如何使用数据事件探查任务的详细信息，请参阅[设置数据事件探查任务](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 有关如何使用数据配置文件查看器分析数据事件探查任务输出的详细信息，请参阅 [数据配置文件查看器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="request-properties-options"></a>请求属性选项  
 对于 **“列值分布配置文件请求”**， **“请求属性”** 窗格显示下列选项组：  
  
-   **Data**，它包含 **TableOrView** 选项和 **Column** 选项  
  
-   **常规**  
  
-   **Options**  
  
### <a name="data-options"></a>Data 选项  
 **ConnectionManager**  
 选择使用 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) 的现有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接管理器连接到包含要进行事件探查的表或视图的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。  
  
 **TableOrView**  
 选择包含要进行事件探查的列的现有表或视图。  
  
 有关详细信息，请参阅本主题中的“TableorView 选项”部分。  
  
 **Column**  
 选择要进行事件探查的现有列。 选择 **(\*)** 可对所有列进行事件探查。  
  
 有关详细信息，请参阅本主题中的“Column 选项”部分。  
  
#### <a name="tableorview-options"></a>TableOrView 选项  
 **架构**  
 指定选定表所属的架构。 此选项是只读的。  
  
 **表**  
 显示所选表的名称。 此选项是只读的。  
  
#### <a name="column-options"></a>Column 选项  
 **IsWildCard**  
 指定是否已选择通配符 **(\*)**。 如果已选择 **(\*)** 来对所有列进行事件探查，则此选项设置为 **True**。 如果您已选择要对单独列进行事件探查，则为 **False** 。 此选项是只读的。  
  
 **ColumnName**  
 显示所选列的名称。 如果已选择 **(\*)** 来对所有列进行事件探查，则此选项空白。 此选项是只读的。  
  
 **StringCompareOptions**  
 选择用于比较字符串值的选项。 此属性具有下表所列的选项。 此选项的默认值为 **Default**。  
  
> [!NOTE]  
>  如果将 **(\*)** 通配符用于 **ColumnName**，则 **CompareOptions** 为只读并设置为 **Default** 设置。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**Default**|根据源表中列的排序规则对数据进行排序和比较。|  
|**BinarySort**|根据为每个字符所定义的位模式对数据进行排序和比较。 二进制排序顺序既区分大小写，也区分重音。 二进制排序顺序的速度也最快。|  
|**DictionarySort**|根据关联语言或文字字典中定义的排序和比较规则对数据进行排序和比较。|  
  
 如果选择 **DictionarySort**，还可以选择下表中列出的任意选项组合。 默认情况下，不会选择这些附加选项中的任何一个。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**IgnoreCase**|指定比较是否区分大小写字母。 如果设置了此选项，字符串比较会忽略大小写。 例如，"ABC" 和 "abc" 没有区别。|  
|**IgnoreNonSpace**|指定比较是否区分空格字符和标注字符。 如果设置了此选项，则比较会忽略标注字符。 例如，"å" 与 "a" 相同。|  
|**IgnoreKanaType**|指定比较是否区分日语的两种假名字符类型：平假名和片假名。 如果设置了此选项，字符串比较会忽略假名类型。|  
|**IgnoreWidth**|指定比较是否区分字符的单字节形式和该字符的双字节形式。 如果设置了此选项，字符串比较将把同一字符的单字节形式和双字节形式视为相同。|  
  
### <a name="general-options"></a>常规选项  
 **RequestID**  
 键入一个标识此配置文件请求的描述性名称。 通常无需更改自动生成的值。  
  
### <a name="options"></a>“常规”  
 **ValueDistributionOption**  
 指定是否计算所有列值的分布。 此选项的默认值为 **FrequentValues**。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**AllValues**|计算所有列值的分布。|  
|**FrequentValues**|仅计算其频率超出 **FrequentValueThreshold**中指定的最小值的值的分布。 输出报告中将不包括未满足 **FrequentValueThreshold** 的值。|  
  
 **FrequentValueThreshold**  
 使用 0 到 1 之间的值指定阈值，超过该阈值将报告列值。 当选择 **AllValues** 作为 **ValueDistributionOption**时，将禁用此选项。 此选项的默认值为 0.001。  
  
## <a name="see-also"></a>另请参阅  
 [数据事件探查任务编辑器（“常规”页）](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [单个表快速配置文件窗体（数据事件探查任务）](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
