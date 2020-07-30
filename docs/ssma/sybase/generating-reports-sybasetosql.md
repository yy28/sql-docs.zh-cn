---
title: 生成报告（SybaseToSQL） |Microsoft Docs
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
ms.openlocfilehash: 564385c15d9877454d30892f9cce54fbca6cf802
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396386"
---
# <a name="generating-reports-sybasetosql"></a>生成报告 (SybaseToSQL)
使用命令执行的某些活动的报告在对象树级别的 SSMA 控制台中生成。  
  
使用以下过程来生成报表：  
  
1.  指定**写入摘要-报表-报表-到**参数。 相关报表存储为文件名（如果已指定），或存储在指定的文件夹中。 文件名按下表中所述进行系统预定义，其中， ** &lt; n &gt; **是在每次执行同一命令时以数字递增的唯一文件号。  
  
    报告 vis-vis 命令包括：  
  
    |Sl. 不能。|命令|报表标题|  
    |-|-|-|  
    |1|生成-评估-报表|AssessmentReport &lt; n &gt; 。XML|  
    |2|转换-架构|SchemaConversionReport &lt; n &gt; 。XML|  
    |3|迁移-数据|DataMigrationReport &lt; n &gt; 。XML|  
    |4|convert-sql 语句|ConvertSQLReport &lt; n &gt; 。XML|  
    |5|同步-目标|TargetSynchronizationReport &lt; n &gt; 。XML|  
    |6|从数据库刷新|SourceDBRefreshReport &lt; n &gt; 。XML|  
  
    > [!IMPORTANT]  
    > 输出报告不同于评估报告。 前者是有关执行的命令的性能报告，后者是用于编程的 XML 报告。  
  
    对于输出报表的命令选项（从 Sl 开始）。 不能。 2-4），请参阅[执行 SSMA 控制台 &#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)部分。  
  
2.  使用报表详细级别设置指示输出报表中所需的详细信息的范围：  
  
    |Sl. 不能。|命令和参数|输出描述|  
    |-|-|-|  
    |1|verbose = "false"|生成活动的汇总报表。|  
    |2|verbose = "true"|为每个活动生成汇总且详细的状态报告。|  
  
    > [!NOTE]  
    > 上面指定的报表详细级别设置适用于 "生成-评估-报表"、"转换架构"、"迁移数据"、"转换-sql 语句" 命令。  
  
3.  使用错误报告设置来指示错误报告中所需的详细信息的范围：  
  
    |Sl. 不能。|命令和参数|输出描述|  
    |-|-|-|  
    |1|报告错误 = "false"|没有关于错误/警告/信息消息的详细信息。|  
    |2|报告错误 = "true"|详细的错误/警告/信息消息。|  
  
    > [!NOTE]  
    > 上面指定的错误报告设置适用于 "生成-评估-报表"、"转换架构"、"迁移数据"、"转换-sql 语句" 命令。  
  
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
  
### <a name="synchronize-target"></a>同步-目标：  
命令**同步-目标**具有 "**报告错误-** 目标" 参数，该参数指定同步操作的错误报告的位置。 然后，按名称**TargetSynchronizationReport &lt; n &gt; 。XML**是在指定的位置创建的，其中** &lt; n &gt; **是在每次执行同一命令时以数字递增的唯一文件号。  
  
**注意：** 如果提供了文件夹路径，则 "报告错误到" 参数将成为命令 "同步目标" 的可选属性。  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="<object-name>"  
  
    on-error="<object-type>"  
  
    report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**对象名称：** 指定被视为同步的对象（它还可以具有单个对象名称或组对象名称）。  
  
**错误：** 指定是否将同步错误指定为警告或错误。 针对出错的可用选项：  
  
-   报表-总警告  
  
-   报告-每个警告  
  
-   fail-脚本  
  
### <a name="refresh-from-database"></a>从数据库刷新：  
**从数据库刷新**的命令具有**报表错误-目标**参数，该参数指定刷新操作的错误报告的位置。 然后，按名称**SourceDBRefreshReport &lt; n &gt; 。XML**是在指定的位置创建的，其中** &lt; n &gt; **是在每次执行同一命令时以数字递增的唯一文件号。  
  
**注意：** 如果提供了文件夹路径，则 "报告错误到" 参数将成为命令 "同步目标" 的可选属性。  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="<object-name>"  
  
    object-type ="<object-type>"  
  
    on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
    report-errors-to="<file-name/folder-name> "  
  
/>  
```  
**对象名称：** 指定要刷新的对象（它还可以具有单个对象名称或组对象名称）。  
  
**错误：** 指定是否将刷新错误指定为警告或错误。 针对出错的可用选项：  
  
-   报表-总警告  
  
-   报告-每个警告  
  
-   fail-脚本  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台（Sybase）](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
