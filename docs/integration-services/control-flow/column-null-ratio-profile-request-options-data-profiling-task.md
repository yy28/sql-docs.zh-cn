---
title: "列 Null 比率配置文件请求选项 （数据事件探查任务） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 157ef8e4-fd23-4f81-8194-eebf74e9fd86
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f0cfbec0b81d1a80a813d8fc2c7e7212b33b77a4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="column-null-ratio-profile-request-options-data-profiling-task"></a>列 Null 比率配置文件请求选项（数据事件探查任务）
  可以使用 **“配置文件请求”** 页的 **“请求属性”** 窗格，为请求窗格中选定的 **“列 Null 比率请求”** 设置选项。 列 Null 比率配置文件报告选定列中 null 值的百分比。 此配置文件可以帮助您识别数据中的问题，例如，列中 null 值的比率以外偏高。 例如，列 Null 比率配置文件对邮政编码列进行事件探查时发现，该列中缺少邮政编码的行所占的比例超出允许的范围。  
  
> [!NOTE]  
>  本主题中介绍的选项显示在 **“数据事件探查任务编辑器”** 的 **“配置文件请求”**页中。 有关此编辑器页的详细信息，请参阅[数据事件探查任务编辑器（“配置文件请求”页）](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 有关如何使用数据事件探查任务的详细信息，请参阅[设置数据事件探查任务](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 有关如何使用数据配置文件查看器分析数据事件探查任务输出的详细信息，请参阅 [数据配置文件查看器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="request-properties-options"></a>请求属性选项  
 对于 **“列 Null 比率请求”**， **“请求属性”** 窗格显示下面的选项组：  
  
-   **Data**，它包含 **TableOrView** 选项和 **Column** 选项  
  
-   **常规**  
  
### <a name="data-options"></a>Data 选项  
 **ConnectionManager**  
 选择使用 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) 的现有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接管理器来连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，其中包含要进行事件探查的表或视图。  
  
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
 此选项不适用于列 Null 比率配置文件。  
  
### <a name="general-options"></a>常规选项  
 **RequestID**  
 键入一个标识此配置文件请求的描述性名称。 通常无需更改自动生成的值。  
  
## <a name="see-also"></a>另请参阅  
 [数据事件探查任务编辑器 &#40;常规页 &#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [单个表快速配置文件窗体 &#40; 数据事件探查任务 &#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  

