---
title: 使用示例控制台脚本文件执行 SSMA 控制台 |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ad75b648-d119-4119-98f0-d18f058be68d
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 738577f16beeaf7545b55f894f04649279dc3122
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-the-sample-console-script-filesexecuting-the-ssma-console-accesstosql"></a>使用示例控制台脚本文件执行 SSMA 控制台 (AccessToSQL)
几个示例文件已与产品一起提供的用户参考和使用情况。 本部分介绍的方法轻松地自定义这些脚本以满足的最终用户需求。  
  
## <a name="sample-console-script-files"></a>示例控制台脚本文件  
为用户参考提供了涵盖不同的方案的以下示例控制台脚本文件：  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   此示例让源和目标数据库不同的可连接模式，并且用户可以选择根据每个需求的任何模式。 此示例包含的服务器定义。  
  
    -   只需将值更改为所需的源和目标服务器定义的情况下，用户可以连接到所需的数据库。 提供的示例中的所有值都提供了为变量的值中提供的**VariableValueFileSample.xml**。 所有其他连接参数可以删除从用户的工作服务器连接文件。  
  
    -   连接到源和目标服务器的详细信息，请参阅[服务器连接文件创建&#40;AccessToSQL&#41; ](../../ssma/access/creating-the-server-connection-files-accesstosql.md) 。  
  
-   **VariableValueFileSample.xml:** 已用在示例控制台中的所有变量都脚本文件和`ServersConnectionFileSample.xml`整理后要在此文件中。 若要执行用户必须只需将示例变量的示例控制台脚本值与用户定义的并将此文件作为脚本文件以及其他命令行自变量传递。  
  
    变量的值文件的详细信息，请参阅[创建变量的值文件&#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)。  
  
-   **AssessmentReportGenerationSample.xml:** 此示例使用户能够生成可由用户以进行分析之前他开始转换和迁移数据的 xml 评估报表。  
  
    在`generate-assessment-report`命令，用户必须 mandatorily 更改变量值 (请参阅**VariableValueFileSample.xml**) 中`object-name`属性设为数据库名称是在用户使用。 根据指定对象的种类`object-type`值将还必须更改。  
  
    如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`generate-assessment-report`示例控制台脚本文件的命令的示例 4。  
  
    生成报表的详细信息，请参阅[生成报表&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)。  
  
    > [!NOTE]  
    > -   确保变量值文件命令行自变量传递到控制台应用程序，并使用指定的用户更新 VariableValueFileSample.xml 值。  
    > -   确保服务器连接文件命令行自变量传递到控制台应用程序和 ServersConnectionFileSample.xml 更新使用正确的服务器的参数值。  
  
-   **ConversionAndDataMigrationSample.xml:** 此示例使用户能够从转换为数据迁移执行端到端迁移。 下面列出的他们将需要更改的必需的属性值列表：  
  
    |命令名称|Description|Attribute|  
    |----------------|---------------|-------------|  
    |`map-schema`|架构映射到目标架构的源数据库。|`source-schema:` 指定需要要转换的源数据库。<br /><br />`sql-server-schema`： 指定是要迁移到目标数据库|  
    |`convert-schema`|执行架构转换从源到目标架构。<br /><br />如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`convert-schema`示例控制台脚本文件的命令的示例 4。|`object-name`： 指定源数据库/对象需要要转换的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`|  
    |`synchronize-target`|将目标对象与目标数据库同步。<br /><br />如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`synchronize-target`示例控制台脚本文件的命令的示例 3。|`object-name:` 指定 sql server 数据库/对象创建所需的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`|  
    |`migrate-data`|将源数据迁移到目标。<br /><br />如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`migrate-data`示例控制台脚本文件的命令的示例 2。|`object-name:` 指定的源数据库/表需要要迁移的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`|  
  
## <a name="see-also"></a>另请参阅  
[创建变量值文件&#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
[创建服务器连接文件&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
[生成报表&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)  
  
