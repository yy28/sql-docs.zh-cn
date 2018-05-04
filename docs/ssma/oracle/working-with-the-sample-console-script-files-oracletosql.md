---
title: 使用示例控制台脚本文件 (OracleToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Sample Console Script Files, ServersConnectionFileSample.xml
- Sample Console Script Files, SqlStatementConversionSample.xml
- Sample Console Script Files,VariableValueFileSample.xml
ms.assetid: c6202dcc-b994-457b-9b2f-0cd89e79792d
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: abc14047184e35909b83e4af2d98fba56fdcbe2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-the-sample-console-script-files-oracletosql"></a>使用示例控制台脚本文件 (OracleToSQL)
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
  
    -   连接到源和目标服务器的详细信息，请参阅[服务器连接文件创建&#40;OracleToSQL&#41; ](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) 。  
  
-   **VariableValueFileSample.xml:** 已用在示例控制台中的所有变量都脚本文件和`ServersConnectionFileSample.xml`整理后要在此文件中。 若要执行用户必须只需将示例变量的示例控制台脚本值与用户定义的并将此文件作为脚本文件以及其他命令行自变量传递。  
  
    变量的值文件的详细信息，请参阅[创建变量的值文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)。  
  
-   **AssessmentReportGenerationSample.xml:** 此示例使用户能够生成可由用户以进行分析之前他开始转换和迁移数据的 xml 评估报表。  
  
    在`generate-assessment-report`命令，用户必须 mandatorily 更改变量值 (请参阅**VariableValueFileSample.xml**) 中`object-name`属性设为数据库名称是在用户使用。 根据指定对象的种类`object-type`值将还必须更改。  
  
    如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`generate-assessment-report`示例控制台脚本文件的命令的示例 4。  
  
    生成报表的详细信息，请参阅[生成报表&#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md)。  
  
    > [!NOTE]  
    > -   确保变量值文件命令行自变量传递到控制台应用程序，并使用指定的用户更新 VariableValueFileSample.xml 值。  
    > -   确保服务器连接文件命令行自变量传递到控制台应用程序和 ServersConnectionFileSample.xml 更新使用正确的服务器的参数值。  
  
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
  
    -   执行架构转换从源到目标架构。  
  
    -   如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`convert-schema`示例控制台脚本文件的命令的示例 4。  
  
    **属性**  
  
    `object-name`： 指定源数据库/对象需要要转换的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
    **命令名称**  
  
    `synchronize-target`  
  
    -   将目标对象与目标数据库同步。  
  
    -   如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`synchronize-target`示例控制台脚本文件的命令的示例 3。  
  
    **属性**  
  
    `object-name:` 指定 sql server 数据库/对象创建所需的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
    **命令名称**  
  
    `migrate-data`  
  
    -   将源数据迁移到目标。  
  
    -   如果用户必须评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`migrate-data`示例控制台脚本文件的命令的示例 2。  
  
    **属性**  
  
    `object-name:` 指定的源数据库/表需要要迁移的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
## <a name="see-also"></a>另请参阅  
[创建变量值文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
[创建服务器连接文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
[生成报表&#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md)  
  
