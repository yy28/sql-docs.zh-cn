---
title: 生成报告 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,generating reports
- Sybase Console,refresh-from-database report
- Sybase Console,synchronize-target report
ms.assetid: 19278f6a-6d58-4867-9d71-c6228040466e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bb377e36f73bad59da35fabc2f6e9189544230e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126290"
---
# <a name="generating-reports-sybasetosql"></a>生成报告 (SybaseToSQL)
在对象树中级别的 SSMA 控制台中生成使用命令来执行某些活动的报告。  
  
使用以下过程生成的报告：  
  
1.  指定**摘要-报表-向其写入**参数。 相关的报表，存储作为文件的名称 （如果指定） 或指定的文件夹中。 文件名称是系统预定义的下, 表中所述**&lt;n&gt;** 是唯一的文件数，以每次执行同一命令数字递增。  
  
    报表 vis 即命令是：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**Command**|**报表标题**|  
    |1|generate-assessment-report|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|migrate-data|DataMigrationReport&lt;n&gt;.XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;.XML|  
    |5|synchronize-target|TargetSynchronizationReport&lt;n&gt;.XML|  
    |6|refresh-from-database|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > 输出报告是不同的评估报告。 前者是对执行命令时的性能报表，后者是以编程方式使用的 XML 报表。  
  
    （从 Sl 输出报表命令选项。 否。 2-4 以上)，请参阅[执行 SSMA 控制台&#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)部分。  
  
2.  表示范围中使用的报表的详细级别设置的输出报表所需的详细信息：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**命令和参数**|**输出说明**|  
    |1|verbose="false"|生成活动的汇总的报告。|  
    |2|verbose="true"|生成的每个活动的摘要和详细状态报告。|  
  
    > [!NOTE]  
    > 上面指定的报表详细级别设置是适用于生成评估报告、 convert 架构、 迁移数据、 转换 sql 语句命令。  
  
3.  指示使用错误报告设置的错误报告中所需的详细信息的程度：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**命令和参数**|**输出说明**|  
    |1|report-errors="false"|没有错误的详细信息 / 警告 / 信息消息。|  
    |2|report-errors="true"|详细的错误 / 警告 / 信息消息。|  
  
    > [!NOTE]  
    > 上面指定的错误报告设置是适用于生成评估报告、 convert 架构、 迁移数据、 转换 sql 语句命令。  
  
```xml  
<generate-assessment-report  
  
    object-name="<object-name>"  
  
    object-type="<object-type>"  
  
    verbose="<true/false>"  
  
    report-erors="<true/false>"  
  
    write-summary-report-to="<file-name/folder-name>"  
  
    assessment-report-folder="<folder-name>"  
  
    assessment-report-overwrite="<true/false>"  
  
/>  
```  
  
### <a name="synchronize-target"></a>同步目标：  
该命令**同步目标**已**报表-到错误**参数，它指定为同步操作的错误报告的位置。 然后，按名称的文件**TargetSynchronizationReport&lt;n&gt;。XML**创建在指定的位置，其中**&lt;n&gt;** 是唯一的文件数，以每次执行同一命令数字递增。  
  
**注意：** 如果未指定文件夹路径，报表-错误-到参数将成为的命令同步的目标的可选属性。  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="<object-name>"  
  
    on-error="<object-type>"  
  
    report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**object-name:** 指定同步 （如果还没有单个对象名或组对象名称） 被视为对象。  
  
**错误：** 指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   fail-script  
  
### <a name="refresh-from-database"></a>刷新从数据库：  
该命令**从数据库刷新**已**报表-到错误**参数，它指定刷新操作的错误报告的位置。 然后，按名称的文件**SourceDBRefreshReport&lt;n&gt;。XML**创建在指定的位置，其中**&lt;n&gt;** 是唯一的文件数，以每次执行同一命令数字递增。  
  
**注意：** 如果未指定文件夹路径，报表-错误-到参数将成为的命令同步的目标的可选属性。  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="<object-name>"  
  
    object-type ="<object-type>"  
  
    on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
    report-errors-to="<file-name/folder-name> "  
  
/>  
```  
**object-name:** 指定用于刷新 （它还可以包含单个对象名或组对象名称） 被视为对象。  
  
**错误：** 指定是否为警告或错误指定刷新错误。 错误上的可用选项包括：  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   fail-script  
  
## <a name="see-also"></a>请参阅  
[执行 SSMA 控制台 (Sybase)](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
