---
title: 生成报告 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: abb4264a-622e-4215-af5b-14e309b8a399
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b5138dea4cfea23d77dae5d4bc766b4c2738f4e7
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659059"
---
# <a name="generating-reports-accesstosql"></a>生成报告 (AccessToSQL)
在对象树中级别的 SSMA 控制台中生成使用命令来执行某些活动的报告。  
  
使用以下过程生成的报告：  
  
1.  指定**摘要-报表-向其写入**参数。 相关的报表，存储作为文件的名称 （如果指定） 或指定的文件夹中。 文件名称是系统预定义的下, 表中所述**&lt;n&gt;** 是唯一的文件数，以每次执行同一命令数字递增。  
  
    报表 vis 即命令是：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**Command**|**报表标题**|  
    |1|generate-assessment-report|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|迁移数据|DataMigrationReport&lt;n&gt;。XML|  
    |4|同步目标|TargetSynchronizationReport&lt;n&gt;.XML|  
    |5|从数据库刷新|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > 输出报告是不同的评估报告。 前者是对执行命令时的性能报表，后者是以编程方式使用的 XML 报表。  
  
    （从 Sl 输出报表命令选项。 否。 2-4 以上)，请参阅[执行 SSMA 控制台&#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md)部分。  
  
2.  表示范围中使用的报表的详细级别设置的输出报表所需的详细信息：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**命令和参数**|**输出说明**|  
    |1|verbose=”false”|生成活动的汇总的报告。|  
    |2|verbose=”true”|生成的每个活动的摘要和详细状态报告。|  
  
    > [!NOTE]  
    > 上面指定的报表详细级别设置是适用于生成评估报告、 convert 架构、 迁移数据命令。  
  
3.  指示使用错误报告设置的错误报告中所需的详细信息的程度：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**命令和参数**|**输出说明**|  
    |1|report-errors=”false”|没有错误的详细信息 / 警告 / 信息消息。|  
    |2|report-errors=”true”|详细的错误 / 警告 / 信息消息。|  
  
    > [!NOTE]  
    > 上面指定的错误报告设置是适用于生成评估报告、 convert 架构、 迁移数据命令。  
  
**示例：**  
  
```xml  
<generate-assessment-report  
  
    object-name="testschema"  
  
    object-type="Schemas"  
  
    verbose="yes"  
  
    report-erors="yes"  
  
    write-summary-report-to="$AssessmentFolder$\Report1.xml"  
  
    assessment-report-folder="$AssessmentFolder$\assesment_report"  
  
    assessment-report-overwrite="true"  
  
/>  
```  
  
### <a name="synchronize-target"></a>同步目标：  
该命令**同步目标**已**报表-到错误**参数，它指定为同步操作的错误报告的位置。 然后，按名称的文件**TargetSynchronizationReport&lt;n&gt;。XML**创建在指定的位置，其中**&lt;n&gt;** 是唯一的文件数，以每次执行同一命令数字递增。  
  
**注意：** 如果给定的文件夹路径，则报表-错误-到参数将成为命令同步的目标的一个可选属性。  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="$TargetDB$.dbo"  
  
    on-error="fail-script"  
  
    report-errors-to="$SynchronizationReports$"  
  
/>  
```  
**对象名称：** 指定考虑进行同步 （如果还没有单个对象名或组对象名称） 的对象。  
  
**-error:** 指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
-   作为警告报告总数  
  
-   报表的每个-作为-警告  
  
-   脚本失败  
  
### <a name="refresh-from-database"></a>刷新从数据库：  
该命令**从数据库刷新**已**报表-到错误**参数，它指定刷新操作的错误报告的位置。 然后，按名称的文件**SourceDBRefreshReport&lt;n&gt;。XML**创建在指定的位置，其中**&lt;n&gt;** 是唯一的文件数，以每次执行同一命令数字递增。  
  
**注意：** 如果给定的文件夹路径，则报表-错误-到参数将成为命令同步的目标的一个可选属性。  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="$SourceDatabaseStandard$"  
  
    object-type ="Databases"  
  
    on-error="fail-script"  
  
    report-errors-to="$RefreshDBFolder$\RefreshReport.xml"  
  
/>  
```  
**对象名称：** 指定用于刷新 （它还可以包含单个对象名或组对象名称） 被视为对象。  
  
**-error:** 指定是否为警告或错误指定刷新错误。 错误上的可用选项包括：  
  
-   作为警告报告总数  
  
-   报表的每个-作为-警告  
  
-   脚本失败  
  
## <a name="see-also"></a>请参阅  
[执行 SSMA 控制台 （访问）](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
