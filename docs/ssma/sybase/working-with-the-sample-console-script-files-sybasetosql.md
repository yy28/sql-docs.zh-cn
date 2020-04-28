---
title: 使用示例控制台脚本文件（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Sample Console Script Files
ms.assetid: ef221118-b442-4ca6-9409-6ee1d9f8d948
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: fe9e05f0078f0d1a9d3ab5ea6e2763ac28207085
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68091793"
---
# <a name="working-with-the-sample-console-script-files-sybasetosql"></a>使用示例控制台脚本文件 (SybaseToSQL)
提供了一些示例文件，其中包含有关用户参考和使用情况的产品。 本部分介绍了如何轻松地自定义这些脚本以满足最终用户需求。  
  
## <a name="sample-console-script-files"></a>示例控制台脚本文件  
以下示例控制台脚本文件涵盖了用于用户引用的不同方案：  
  
-   ServersConnectionFileSample  
  
-   VariableValueFileSample  
  
-   AssessmentReportGenerationSample  
  
-   SqlStatementConversionSample  
  
-   ConversionAndDataMigrationSample  
  
-   **ServersConnectionFileSample：**  
  
    -   此示例为源数据库和目标数据库提供了不同的连接模式，用户可以根据需要选择任何模式。 此示例包含服务器定义。  
  
    -   用户只需将值更改为所需的源和目标服务器定义，就可以连接到所需的数据库。 在本示例中，提供了所有值作为可在**VariableValueFileSample**中使用的变量值。  可以从用户的工作服务器连接文件中删除所有其他连接参数。  
  
    -   有关连接到源服务器和目标服务器的详细信息，请参阅[创建服务器连接文件 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)。  
  
-   **VariableValueFileSample：**  
    已在示例控制台脚本文件中使用的所有变量，并`ServersConnectionFileSample.xml`已在此文件中进行排序。 若要执行示例控制台脚本，用户必须只需将示例变量值替换为用户定义的变量值，并将此文件作为附加命令行参数和脚本文件一起传递。  
  
    有关变量值文件的详细信息，请参阅[创建变量值文件 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)。  
  
-   **AssessmentReportGenerationSample：**  
    此示例使用户能够生成一个 xml 评估报表，用户可以在开始转换和迁移数据之前，使用该报表进行分析。  
  
    在`generate-assessment-report`命令中，用户必须 mandatorily 将`object-name`属性中的变量值（请参阅**VariableValueFileSample**）更改为用户正在使用的数据库名称。 根据指定的对象类型，还必须更改`object-type`值。  
  
    如果用户必须评估多个对象/数据库，他可以指定多`metabase-object`个节点，如示例`generate-assessment-report`控制台脚本文件的命令示例4中所示。  
  
    有关生成报表的详细信息，请参阅[&#40;SybaseToSQL&#41;中生成报表](../../ssma/sybase/generating-reports-sybasetosql.md)。  
  
    > [!NOTE]  
    > -   确保将变量值 file 命令行参数传递到控制台应用程序，并以用户指定的值更新 VariableValueFileSample。  
    > -   确保将服务器连接文件命令行参数传递到控制台应用程序，并用正确的服务器参数值更新 ServersConnectionFileSample。  
  
-   **SqlStatementConversionSample：**  
    此示例允许用户为作为输入提供的`t-sql`源数据库`sql`命令生成相应的脚本。  
  
    在`convert-sql-statement`命令中，用户必须 mandatorily 将`context`属性中的变量值（请参阅**VariableValueFileSample**）更改为用户正在使用的数据库名称。 还需要用户将`sql`属性值更改为其需要转换的源数据库`sql`命令。  
  
    用户还可以提供要转换的 sql 文件。 此`convert-sql-statement`命令在示例控制台脚本文件的示例4中进行了说明。  
  
    > [!NOTE]  
    > 确保将变量值 file 命令行参数传递到控制台应用程序，并以用户指定的值更新 VariableValueFileSample。  
  
-   **ConversionAndDataMigrationSample：**  
     使用此示例，用户可以执行端到端迁移，从转换到数据迁移。 下面列出了需要更改的必需属性值的列表：  
  
    **命令名：**  
  
    `map-schema`  
  
    将源数据库映射到目标架构的架构。  
  
    **特性**  
  
    -   `source-schema:`指定需要转换的源数据库。  
  
    -   `sql-server-schema`：指定要迁移到的目标数据库  
  
    **命令名：**  
  
    `convert-schema`  
  
    -   执行从源到目标架构的架构转换。  
  
    -   如果用户必须评估多个对象/数据库，他可以指定多`metabase-object`个节点，如示例`convert-schema`控制台脚本文件的命令示例4中所示。  
  
    **特性**  
  
    `object-name`：指定需要转换的源数据库/对象名称。 确保根据在中`object-type`指定的对象类型更改相应的`object-name`  
  
    **命令名：**  
  
    `synchronize-target`  
  
    -   将目标对象与目标数据库同步。  
  
    -   如果用户必须评估多个对象/数据库，他可以指定多`metabase-object`个节点，如示例`synchronize-target`控制台脚本文件的命令示例3中所示。  
  
    **特性**  
  
    `object-name:`指定需要创建的 sql server 数据库/对象名称。 确保根据在中`object-type`指定的对象类型更改相应的`object-name`  
  
    **命令名：**  
  
    `migrate-data`  
  
    -   将源数据迁移到目标。  
  
    -   如果用户必须评估多个对象/数据库，他可以指定多`metabase-object`个节点，如示例`migrate-data`控制台脚本文件的命令示例2中所示。  
  
    **特性**  
  
    `object-name:`指定需要迁移的源数据库/表名称。 确保根据在中`object-type`指定的对象类型更改相应的`object-name`  
  
## <a name="see-also"></a>另请参阅  
[创建变量值文件 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
[&#40;SybaseToSQL 创建服务器连接文件&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
[&#40;SybaseToSQL 生成报告&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)  
  
