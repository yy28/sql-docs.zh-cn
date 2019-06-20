---
title: 列统计信息配置文件请求选项（数据事件探查任务）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 87205984-507a-49f3-b27c-36a0075c234d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e07bd6ead9ce0dfc20249f5db50a8b0b78ba242a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832715"
---
# <a name="column-statistics-profile-request-options-data-profiling-task"></a>列统计信息配置文件请求选项（数据事件探查任务）
  可以使用 **“配置文件请求”** 页的 **“请求属性”** 窗格，为请求窗格中选择的 **“列统计信息配置文件请求”** 设置选项。 列统计信息配置文件报告以下统计信息：数值列的最小值、最大值、平均值和标准偏差以及 `datetime` 列的最小值和最大值。 此配置文件可以帮助您识别数据中的问题，如无效日期。 例如，您对历史日期列进行事件探查，却发现最近的日期是一个将来的日期。  
  
> [!NOTE]  
>  本主题中介绍的选项显示在 **“数据事件探查任务编辑器”** 的 **“配置文件请求”** 页中。 有关此编辑器页的详细信息，请参阅[数据事件探查任务编辑器（“配置文件请求”页）](data-profiling-task-editor-profile-requests-page.md)。  
  
 有关如何使用数据事件探查任务的详细信息，请参阅[设置数据事件探查任务](data-profiling-task.md)。 有关如何使用数据配置文件查看器分析数据事件探查任务输出的详细信息，请参阅 [数据配置文件查看器](data-profile-viewer.md)。  
  
## <a name="request-properties-options"></a>请求属性选项  
 对于 **“列统计信息配置文件请求”**， **“请求属性”** 窗格显示下面的选项组：  
  
-   **Data**，它包含 **TableOrView** 选项和 **Column** 选项  
  
-   **常规**  
  
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
 此选项不适用于列统计信息配置文件。  
  
### <a name="general-options"></a>常规选项  
 **RequestID**  
 键入一个标识此配置文件请求的描述性名称。 通常无需更改自动生成的值。  
  
## <a name="see-also"></a>请参阅  
 [数据事件探查任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)   
 [单个表快速配置文件窗体（数据事件探查任务）](single-table-quick-profile-form-data-profiling-task.md)  
  
  
