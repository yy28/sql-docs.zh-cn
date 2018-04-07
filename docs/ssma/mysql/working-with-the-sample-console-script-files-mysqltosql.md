---
title: 使用示例控制台脚本文件 (MySQLToSQL) |Microsoft 文档
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
- Sample console script files
ms.assetid: 7e6aaa8a-5f5c-414d-9fb8-21e56b9ffaef
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 667cd2b758e5b7f249379b00266db3fc41c1d398
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="working-with-the-sample-console-script-files-mysqltosql"></a>使用示例控制台脚本文件 (MySQLToSQL)
几个示例文件已与产品一起提供的用户参考和使用情况。 本部分介绍的方法轻松地自定义这些脚本以满足的最终用户需求。  
  
## <a name="sample-console-script-files"></a>示例控制台脚本文件  
为用户参考提供了涵盖不同的方案的以下示例控制台脚本文件：  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   此示例让源和目标数据库不同的可连接模式，并且用户可以选择根据每个需求的任何模式。 此示例包含的服务器定义。  
  
    -   只需将值更改为所需的源和目标服务器定义的情况下，用户可以连接到所需的数据库。 提供的示例中的所有值都提供了为变量的值中提供的**VariableValueFileSample.xml**。  所有其他连接参数可以删除从用户的工作服务器连接文件。  
  
    -   连接到源和目标服务器的详细信息，请参阅[服务器连接文件创建&#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md) 。  
  
-   **VariableValueFileSample.xml:**已用在示例控制台中的所有变量都脚本文件和`ServersConnectionFileSample.xml`整理后要在此文件中。 若要执行用户必须只需将示例变量的示例控制台脚本值与用户定义的并将此文件作为脚本文件以及其他命令行自变量传递。  
  
    变量的值文件的详细信息，请参阅[创建变量的值文件&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)。  
  
-   **AssessmentReportGenerationSample.xml:**此示例使用户能够生成可由用户以进行分析之前他开始转换和迁移数据的 xml 评估报表。  
  
    在`generate-assessment-report`命令，用户必须 mandatorily 更改变量值 (请参阅**VariableValueFileSample.xml**) 中`object-name`属性设为数据库名称是在用户使用。 根据指定对象的种类`object-type`值将还必须更改。  
  
    如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`generate-assessment-report`示例控制台脚本文件的命令的示例 4。  
  
    生成报表的详细信息，请参阅[生成报表&#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md)。  
  
    **说明：**  
  
    -   确保变量值文件命令行自变量传递到控制台应用程序，并使用指定的用户更新 VariableValueFileSample.xml 值。  
  
    -   确保服务器连接文件命令行自变量传递到控制台应用程序和 ServersConnectionFileSample.xml 更新使用正确的服务器的参数值。  
  
-   **SqlStatementConversionSample.xml:**  
    此示例使用户能够生成对应`t-sql`源数据库的脚本`sql`作为输入提供的命令。  
  
    在`convert-sql-statement`命令，用户必须 mandatorily 更改变量值 (请参阅**VariableValueFileSample.xml**) 中`context`属性设为正在使用用户的数据库名称。 用户还将需要更改`sql`属性值设为源数据库`sql`他/她需要要转换的命令。  
  
    用户还可以提供要转换的 sql 文件。 具有已中阐释了这`convert-sql-statement`示例控制台脚本文件的命令的示例 4。  
  
    > [!NOTE]  
    > 确保变量值文件命令行自变量传递到控制台应用程序，并使用指定的用户更新 VariableValueFileSample.xml 值。  
  
-   **ConversionAndDataMigrationSample.xml:**  
     此示例使用户能够从转换为数据迁移执行端到端迁移。 下面列出的他们将需要更改的必需的属性值列表：  
  
    **命令名称**  
  
    `map-schema`  
  
    架构映射到目标架构的源数据库。  
  
    **属性**  
  
    -   `source-schema:` 指定需要要转换的源数据库。  
  
    -   `sql-server-schema`： 指定是要迁移到目标数据库  
  
    **命令名称**  
  
    `convert-schema`  
  
    1.  执行架构转换从源到目标架构。  
  
    2.  如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`convert-schema`示例控制台脚本文件的命令的示例 4。  
  
    **属性**  
  
    `object-name`： 指定源数据库/对象需要要转换的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
    **命令名称**  
  
    `synchronize-target`  
  
    1.  将目标对象与目标数据库同步。  
  
    2.  如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`synchronize-target`示例控制台脚本文件的命令的示例 3。  
  
    **属性**  
  
    `object-name:` 指定 sql server 数据库/对象创建所需的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
    **命令名称**  
  
    `migrate-data`  
  
    1.  将源数据迁移到目标。  
  
    2.  如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`migrate-data`示例控制台脚本文件的命令的示例 2。  
  
    **属性**  
  
    `object-name:` 指定的源数据库/表需要要迁移的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
## <a name="see-also"></a>另请参阅  
[创建变量值文件&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
[创建服务器连接文件&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
[生成报表&#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md)  
  
