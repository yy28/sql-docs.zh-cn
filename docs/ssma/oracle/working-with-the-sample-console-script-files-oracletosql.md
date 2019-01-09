---
title: 使用示例控制台脚本文件 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sample Console Script Files, ServersConnectionFileSample.xml
- Sample Console Script Files, SqlStatementConversionSample.xml
- Sample Console Script Files,VariableValueFileSample.xml
ms.assetid: c6202dcc-b994-457b-9b2f-0cd89e79792d
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 152d8ba2964c8485a1f158b71717067fdea948a2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52406014"
---
# <a name="working-with-the-sample-console-script-files-oracletosql"></a>使用示例控制台脚本文件 (OracleToSQL)
几个示例文件与产品一起提供的用户参考和使用情况。 本部分介绍的方法轻松地自定义这些脚本以满足最终用户需求。  
  
## <a name="sample-console-script-files"></a>示例控制台脚本文件  
为用户参考提供了涵盖不同的方案的以下示例控制台脚本文件：  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   此示例对源和目标数据库都提供了不同的可用连接模式，用户可以选择根据要求任何模式。 此示例包含的服务器定义。  
  
    -   只需将值更改为所需的源和目标服务器定义的情况下，用户可以连接到所需的数据库。 在提供的示例中的所有值都提供了为变量值中可用**VariableValueFileSample.xml**。  可以从用户的工作服务器连接文件中删除所有其他连接参数。  
  
    -   连接到源和目标服务器的详细信息，请参阅[创建服务器连接文件&#40;OracleToSQL&#41; ](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) 。  
  
-   **VariableValueFileSample.xml:** 所有变量已使用在示例控制台都脚本文件和`ServersConnectionFileSample.xml`整理后要在此文件中。 若要执行用户必须只需替换为示例变量的示例控制台脚本值与用户定义的并将此文件作为脚本文件以及其他命令行参数传递。  
  
    变量值文件的详细信息，请参阅[创建的变量值文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)。  
  
-   **AssessmentReportGenerationSample.xml:** 此示例使用户能够生成一个 xml 评估报告，可由用户进行分析之前他开始转换并迁移数据。  
  
    在`generate-assessment-report`命令，用户必须 mandatorily 更改变量值 (请参阅**VariableValueFileSample.xml**) 中`object-name`属性数据库名称不由用户使用。 根据指定，对象的种类`object-type`值也需要进行更改。  
  
    如果用户具有以评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`generate-assessment-report`命令的示例 4 的示例控制台脚本文件。  
  
    生成报告的详细信息，请参阅[生成报表&#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md)。  
  
    > [!NOTE]  
    > -   确保变量值文件命令行参数传递到控制台应用程序，并使用指定的用户更新 VariableValueFileSample.xml 值。  
    > -   请确保服务器连接文件的命令行参数传递到控制台应用程序和 ServersConnectionFileSample.xml 更新使用正确的服务器的参数值。  
  
-   **SqlStatementConversionSample.xml:**  
    此示例使用户能够生成相应`t-sql`的源数据库脚本`sql`作为输入提供的命令。  
  
    在`convert-sql-statement`命令，用户必须 mandatorily 更改变量值 (请参阅**VariableValueFileSample.xml**) 中`context`正在由用户使用的数据库名称的属性。 用户还将需要更改`sql`属性值与源数据库`sql`他/她需要要转换的命令。  
  
    用户还可以提供要转换的 sql 文件。 具有已说明了这`convert-sql-statement`命令的示例 4 的示例控制台脚本文件。  
  
    > [!NOTE]  
    > 确保变量值文件命令行参数传递到控制台应用程序，并使用指定的用户更新 VariableValueFileSample.xml 值。  
  
-   **ConversionAndDataMigrationSample.xml:**  
     此示例使用户能够从转换到数据迁移执行端到端迁移。 下面列出了必需的属性值，它们将需要更改的列表：  
  
    **命令名**  
  
    `map-schema`  
  
    源数据库到目标架构的架构映射。  
  
    **Attribute**  
  
    -   `source-schema:` 指定转换所需的源数据库。  
  
    -   `sql-server-schema`设置用户帐户 ：指定是要迁移到目标数据库  
  
    **命令名**  
  
    `convert-schema`  
  
    -   执行架构转换从源到目标架构。  
  
    -   如果用户具有以评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`convert-schema`命令的示例 4 的示例控制台脚本文件。  
  
    **Attribute**  
  
    `object-name`设置用户帐户 ：指定源数据库/对象要求要转换的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
    **命令名**  
  
    `synchronize-target`  
  
    -   将目标对象与目标数据库同步。  
  
    -   如果用户具有以评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`synchronize-target`示例控制台脚本文件的命令的示例 3。  
  
    **Attribute**  
  
    `object-name:` 指定 sql server 数据库/对象创建所需的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
    **命令名**  
  
    `migrate-data`  
  
    -   将源数据迁移到目标。  
  
    -   如果用户具有以评估多个对象 / 数据库他可以指定多个`metabase-object`节点中所示`migrate-data`命令的示例 2 的示例控制台脚本文件。  
  
    **Attribute**  
  
    `object-name:` 指定源数据库/表迁移所需的名称。 确保相应`object-type`根据中指定的对象的类型进行更改 `object-name`  
  
## <a name="see-also"></a>请参阅  
[创建变量值文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
[创建服务器连接文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
[生成报告&#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md)  
  
