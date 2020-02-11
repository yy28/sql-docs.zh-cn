---
title: 列 Null 比率配置文件请求选项（数据事件探查任务）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 157ef8e4-fd23-4f81-8194-eebf74e9fd86
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 72b426c504532f9c112eaaa1222b0349f3e5d814
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62832588"
---
# <a name="column-null-ratio-profile-request-options-data-profiling-task"></a>列 Null 比率配置文件请求选项（数据事件探查任务）
  可以使用 **“配置文件请求”** 页的 **“请求属性”** 窗格，为请求窗格中选定的 **“列 Null 比率请求”** 设置选项。 列 Null 比率配置文件报告选定列中 null 值的百分比。 此配置文件可以帮助您识别数据中的问题，例如，列中 null 值的比率以外偏高。 例如，列 Null 比率配置文件对邮政编码列进行事件探查时发现，该列中缺少邮政编码的行所占的比例超出允许的范围。  
  
> [!NOTE]  
>  本主题中介绍的选项显示在 **“数据事件探查任务编辑器”** 的 **“配置文件请求”** 页中。 有关此编辑器页的详细信息，请参阅[数据事件探查任务编辑器（“配置文件请求”页）](data-profiling-task-editor-profile-requests-page.md)。  
  
 有关如何使用数据事件探查任务的详细信息，请参阅 [设置数据事件探查任务](data-profiling-task.md)。 有关如何使用数据配置文件查看器分析数据事件探查任务输出的详细信息，请参阅 [数据配置文件查看器](data-profile-viewer.md)。  
  
## <a name="request-properties-options"></a>请求属性选项  
 对于 **“列 Null 比率请求”** ， **“请求属性”** 窗格显示下面的选项组：  
  
-   **Data**，它包含 **TableOrView** 选项和 **Column** 选项  
  
-   **常规**  
  
### <a name="data-options"></a>Data 选项  
 **ConnectionManager**  
 选择使用 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) 的现有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接管理器来连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，其中包含要进行事件探查的表或视图。  
  
 **TableOrView**  
 选择包含要进行事件探查的列的现有表或视图。  
  
 有关详细信息，请参阅本主题中的“TableorView 选项”部分。  
  
 **列**  
 选择要进行事件探查的现有列。 选择 **(\*)** 可对所有列进行事件探查。  
  
 有关详细信息，请参阅本主题中的“Column 选项”部分。  
  
#### <a name="tableorview-options"></a>TableOrView 选项  
 **架构**  
 指定选定表所属的架构。 此选项是只读的。  
  
 **表**  
 显示所选表的名称。 此选项是只读的。  
  
#### <a name="column-options"></a>Column 选项  
 **IsWildCard**  
 指定是否已选择通配符 **(\*)** 。 如果已选择 **(** ) **来对所有列进行事件探查，则此选项设置为 \*True**。 如果您已选择要对单独列进行事件探查，则为 **False** 。 此选项是只读的。  
  
 **ColumnName**  
 显示所选列的名称。 如果已选择 **(\*)** 来对所有列进行事件探查，则此选项空白。 此选项是只读的。  
  
 **StringCompareOptions**  
 此选项不适用于列 Null 比率配置文件。  
  
### <a name="general-options"></a>常规选项  
 **RequestID**  
 键入一个标识此配置文件请求的描述性名称。 通常无需更改自动生成的值。  
  
## <a name="see-also"></a>另请参阅  
 [数据事件探查任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)   
 [单个表快速配置文件窗体（数据事件探查任务）](single-table-quick-profile-form-data-profiling-task.md)  
  
  
