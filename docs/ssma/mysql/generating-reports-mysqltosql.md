---
title: 生成报表 (MySQLToSQL) |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Generating reports
ms.assetid: 1c0202e8-546d-4cb3-a37f-1d2e35d53839
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: baf2bf9e68f60bd4c9f2afc7033430e19ef96a3e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="generating-reports-mysqltosql"></a>生成报表 (MySQLToSQL)
使用命令执行特定活动的报告中在对象树级别的 SSMA 控制台中生成。  
  
使用以下过程以生成报告：  
  
1.  指定**摘要-报表-向其写入**参数。 相关的报表，存储作为文件名称 （如果指定） 或指定的文件夹中。 文件名称是系统预定义的位置下, 表中所述 **&lt; n &gt;** 是唯一的文件数以每次执行同一命令与数字递增。  
  
    报表 vis à vis 命令是：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**Command**|**报表标题**|  
    |@shouldalert|生成评估报表|AssessmentReport&lt;n&gt;。XML|  
    |2|转换架构|SchemaConversionReport&lt;n&gt;。XML|  
    |3|迁移数据|DataMigrationReport&lt;n&gt;。XML|  
    |4|转换 sql 语句|ConvertSQLReport&lt;n&gt;。XML|  
    |5|同步目标|TargetSynchronizationReport&lt;n&gt;。XML|  
    |6|从数据库中刷新|SourceDBRefreshReport&lt;n&gt;。XML|  
  
    > [!IMPORTANT]  
    > 输出报告是不同的评估报表。 前者是对执行命令时的性能报表，后者是以编程方式使用的 XML 报表。  
  
    （从 Sl 输出报告命令选项。 否。 上面的 2-4)，请参阅[执行 SSMA 控制台 &#40;MySQLToSQL &#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)部分。  
  
2.  指示输出报告使用报告详细级别设置所需的详细信息的范围：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**命令和参数**|**输出说明**|  
    |@shouldalert|详细 ="false"|生成的活动汇总的报告。|  
    |2|详细 ="true"|生成每个活动的摘要和详细状态报表。|  
  
    > [!NOTE]  
    > 上面指定的报表详细级别设置是适用于生成评估报表、 转换架构、 迁移数据、 转换 sql 语句命令。  
  
3.  指示要使用的错误报告设置的错误报告中的详细信息的范围：  
  
    ||||  
    |-|-|-|  
    |**Sl。不。**|**命令和参数**|**输出说明**|  
    |@shouldalert|报告错误 ="false"|没有错误的详细信息 / 警告 / 信息消息。|  
    |2|报告错误 ="true"|详细的错误 / 警告 / 信息消息。|  
  
    > [!NOTE]  
    > 上面指定的错误报告设置是适用于生成评估报表、 转换架构、 迁移数据、 转换 sql 语句命令。  
  
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
该命令**同步目标**具有**报表-到错误**参数，指定该同步操作的错误报告的位置。 然后，名称的文件**TargetSynchronizationReport&lt;n&gt;。XML**创建在指定的位置，其中 **&lt; n &gt;** 是唯一的文件数以每次执行同一命令与数字递增。  
  
**注意：**如果给定的文件夹路径，则报表-错误-到参数成为可选命令 ' 同步-target' 属性。  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**对象名称：**指定为同步 （它还可以具有 indivdual 对象名称或组对象名称） 被视为对象。  
  
**-错误：**指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
-   为警告报告总数  
  
-   报表-每个-作为-警告  
  
-   失败脚本  
  
### <a name="refresh-from-database"></a>刷新从数据库：  
该命令**从数据库中刷新**具有**报表-到错误**参数，指定刷新操作的错误报告的位置。 然后，名称的文件**SourceDBRefreshReport&lt;n&gt;。XML**创建在指定的位置，其中 **&lt; n &gt;** 是唯一的文件数以每次执行同一命令与数字递增。  
  
**注意：**如果给定的文件夹路径，则报表-错误-到参数成为可选命令 ' 同步-target' 属性。  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**对象名称：**指定刷新 （它还可以具有 indivdual 对象名称或组对象名称） 被视为对象。  
  
**-错误：**指定是否为警告或错误指定刷新错误。 错误上的可用选项包括：  
  
-   为警告报告总数  
  
-   报表-每个-作为-警告  
  
-   失败脚本  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台 (MySQL)](http://msdn.microsoft.com/en-us/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
