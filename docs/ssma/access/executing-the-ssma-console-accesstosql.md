---
title: 执行 SSMA 控制台 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d1dbbb57527fc2d362837e0340f35a241d764b75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473525"
---
# <a name="executing-the-ssma-console-accesstosql"></a>执行 SSMA 控制台 (AccessToSQL)
Microsoft 为您提供了一系列可靠的脚本文件命令和命令行选项来执行和控制 SSMA 活动。 接下来的几节详细介绍相同。  
  
## <a name="project--script-file-commands"></a>项目脚本文件命令  
创建项目、 打开、 保存和退出项目项目命令句柄。  
  
**Command**  
  
创建新的项目：创建新的 SSMA 项目。  
  
**脚本**  
  
-   `project-folder` 指示获取创建的项目的文件夹。  
  
-   `project-name` 指示项目的名称。 {string}  
  
-   `overwrite-if-exists`可选属性指示是否应覆盖现有项目。 {布尔值}  
  
-   `project-type` 为可选属性。  项目类型有以下选项：  
  
    -   sql-server-2005  
  
    -   sql-server-2008  
  
    -   sql-server-2012  
  
    -   sql-server-2014  
  
    -   sql-server-2016  
  
    -   sql-azure  
  
    默认值为"sql server 2008"。  
  
**示例：**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"  
  
/>  
```  
覆盖如果-共存的属性是**false**默认情况下。  
  
项目类型属性是**sql server 2008**默认情况下。  
  
**Command**  
  
打开项目：打开现有的项目。  
  
**脚本**  
  
-   `project-folder` 指示获取创建的项目的文件夹。 如果指定的文件夹不存在，则命令将失败。  {string}  
  
-   `project-name` 指示项目的名称。 如果指定的项目不存在，则命令将失败。  {string}  
  
**语法示例：**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
**注意：** SSMA 为访问控制台应用程序支持向后兼容性。 你将能够打开创建的以前版本的 SSMA 项目。  
  
**Command**  
  
保存项目：保存迁移项目。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<save-project/>  
```  
**Command**  
  
关闭项目：关闭迁移项目。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<close-project  
  
  if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
如果修改的属性是可选的**忽略**默认情况下。  
  
## <a name="database-connection-script-file-commands"></a>数据库连接脚本文件命令  
数据库连接命令可帮助连接到数据库。  
  
**浏览**在控制台中不支持 UI 的功能。  
  
**Windows 身份验证**并**端口**连接到 SQL Azure 时，参数不适用。  
  
创建脚本文件的详细信息，请参阅[创建脚本文件&#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md)。  
  
**Command**  
  
connect-source-database  
  
-   执行与源数据库的连接并加载的源数据库但不是所有元数据的高级别元数据。  
  
-   如果无法建立到源的连接，会生成错误并停止进一步执行控制台应用程序。  
  
**脚本**  
  
从服务器部分中的服务器连接文件或脚本文件的每个连接而定义的 name 属性中检索服务器定义。  
  
**语法示例：**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
负载 access 数据库：用于加载访问数据库文件  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
或  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
```  
**Command**  
  
force-load-source/target-database  
  
-   加载源元数据。  
  
-   用于处理脱机迁移项目。  
  
-   如果无法建立与源/目标的连接，会生成错误并停止进一步执行控制台应用程序。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
**语法示例：**  
  
```xml  
<force-load  
  
  object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
或  
  
```xml  
<force-load>  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
reconnect-source-database  
  
-   重新连接到源数据库，但不会加载与连接源数据库命令不同的任何元数据。  
  
-   如果无法建立 （重新） 与源的连接，会生成错误和控制台应用程序停止进一步执行。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
connect-target-database  
  
-   连接到目标 SQL Server 或 SQL Azure 数据库并完全加载目标数据库的高级别的元数据，但不是元数据。  
  
-   如果无法建立到目标连接，会生成错误和控制台应用程序停止进一步执行。  
  
**脚本**  
  
从服务器部分中的服务器连接文件或脚本文件的每个连接而定义的 name 属性检索服务器定义  
  
**语法示例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
-   重新连接到目标数据库，但不会加载任何元数据，与连接目标数据库命令不同。  
  
-   如果无法建立 （重新） 连接到目标，生成错误和控制台应用程序停止进一步执行。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>报表脚本文件命令  
报表命令生成各种 SSMA 控制台活动的性能上的报表。  
  
**Command**  
  
generate-assessment-report  
  
-   生成对源数据库的评估报告。  
  
-   如果执行此命令之前不执行源数据库连接，则会生成错误和控制台应用程序退出。  
  
-   命令执行期间，连接到源数据库服务器失败也会终止的控制台应用程序。  
  
**脚本**  
  
-   `assessment-report-folder:` 指定评估报告可以在其中存储的文件夹。（可选属性）  
  
-   `object-name:` 指定的生成评估报告 （可能包含单个对象名或组对象名称） 时要考虑的对象。  
  
-   `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
-   `assessment-report-overwrite:` 指定是否覆盖评估报表文件夹已存在。  
  
    **默认值：** false。 （可选属性）  
  
-   `write-summary-report-to:` 指定将生成报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**AssessmentReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<generate-assessment-report  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  
  write-summary-report-to="<file>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  conversion-report-folder="<folder>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>迁移脚本文件命令  
迁移命令将目标数据库架构转换为源架构和数据迁移到目标服务器。  
  
设置的迁移命令的默认控制台输出是使用不进行详细的错误报告的完整的输出报表：在源对象树的根节点的唯一摘要。  
  
**Command**  
  
convert-schema  
  
-   执行架构转换从源到目标架构。  
  
-   如果执行此命令之前不执行源或目标数据库连接或连接到源或目标数据库服务器失败命令执行时，会生成错误和控制台应用程序退出。  
  
**脚本**  
  
-   `conversion-report-folder:` 指定评估报告存储的文件夹。（可选属性）  
  
-   `object-name:` 指定源对象视为用于转换的架构 （可能包含单个对象名或组对象名称）。  
  
-   `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
-   `conversion-report-overwrite:` 指定是否覆盖评估报表文件夹已存在。  
  
    **默认值：** false。 （可选属性）  
  
-   `write-summary-report-to:` 指定将生成报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**SchemaConversionReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<convert-schema  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  write-summary-report-to="<filepath/folder>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
或  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```  
**Command**  
  
migrate-data  
  
1.  将源数据迁移到目标。  
  
**脚本**  
  
-   `object-name:` 指定被视为用于迁移的源对象 （可能包含单个对象名或组对象名称） 的数据。  
  
-   `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
-   `write-summary-report-to:` 指定将生成报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**DataMigrationReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true">  
  
    <metabase-object object-name="ssma.TT1"/>  
  
    <metabase-object object-name="ssma.TT2"/>  
  
    <metabase-object object-name="ssma.TT3"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
或  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```  
**Command**  
  
链接表：此命令可链接到目标表的源表 （访问）。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```  
或  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```  
**Command**  
  
取消链接的表：此命令将取消链接的目标表中的源表 （访问）。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```  
或  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>迁移准备脚本文件命令  
迁移准备命令开始架构源和目标数据库之间的映射。  
  
**Command**  
  
映射架构：源数据库到目标架构的架构映射。  
  
**脚本**  
  
-   `source-schema` 指定我们想要迁移的源架构。  
  
-   `sql-server-schema` 指定我们想要的位置要迁移的目标架构。  
  
**语法示例：**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>可管理性命令  
可管理性命令可帮助将与源数据库同步目标数据库对象。  
  
设置的迁移命令的默认控制台输出是使用不进行详细的错误报告的完整的输出报表：在源对象树的根节点的唯一摘要。  
  
**Command**  
  
synchronize-target  
  
1.  将目标对象与目标数据库同步。  
  
2.  如果对源数据库执行此命令时，遇到错误。  
  
3.  如果执行此命令之前不执行目标数据库连接或连接到目标数据库服务器失败命令执行时，会生成错误和控制台应用程序退出。  
  
**脚本**  
  
1.  `object-name:` 指定目标对象被视为与目标数据库 （可能包含单个对象名或组对象名称） 进行同步。  
  
2.  `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
3.  `on-error:` 指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
4.  `report-errors-to:` 为同步操作 （以属性为可选） 如果仅指定文件夹路径，然后将文件按名称指定的错误报告位置**TargetSynchronizationReport.XML**创建。  
  
**语法示例：**  
  
```xml  
<synchronize-target  
  
  object-name="ots_triggers.dbo"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
或  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```  
或  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```  
**Command**  
  
refresh-from-database  
  
-   刷新数据库中的源对象。  
  
-   如果对目标数据库执行此命令，则会生成错误。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
1.  `object-name:` 指定用于刷新 （可能包含单个对象名或组对象名称） 的源数据库中被视为源对象。  
  
2.  `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
3.  `on-error:` 指定是否为警告或错误指定刷新错误。 错误上的可用选项包括：  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
4.  `report-errors-to:` 刷新操作 （以属性为可选） 如果仅指定文件夹路径，然后将文件按名称指定的错误报告位置**SourceDBRefreshReport.XML**创建。  
  
**语法示例：**  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.TT1"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
或  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```  
或  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>脚本生成的脚本文件命令  
脚本生成命令可帮助在脚本文件中保存的控制台输出。  
  
**Command**  
  
save-as-script  
  
用于将对象的脚本保存到文件时提到元数据库 = 目标，这是在其中中我们获取脚本并执行相同目标数据库上的同步命令的替代方法。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
-   `object-name:` 指定的脚本将保存的对象。 （它可以具有单独的对象名称或组对象名称）  
  
-   `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
-   `metabase:` 指定是否在源或目标元数据库。  
  
-   `destination:` 指定的路径或其中脚本已保存，如果文件名称中未给然后文件名称格式 （object_name 属性值）.out 的文件夹  
  
-   `overwrite:` 如果为 true 则它将覆盖存在相同的文件名。 它可以具有值 (true/false)。  
  
**语法示例：**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"  
  
  destination="<file/folder>"  
  
  overwrite="<true/false>"             (optional)  
  
/>  
```  
或  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-step"></a>下一步  
有关命令行选项的信息，请参阅[SSMA 控制台中的命令行选项&#40;AccessToSQL&#41; ](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) 。  
  
有关示例控制台脚本文件的信息，请参阅[使用示例控制台脚本文件执行 SSMA 控制台&#40;AccessToSQL&#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
下一步取决于你的项目要求：  
  
-   用于指定密码或导出 / 导入密码，请参阅[管理密码&#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md)。  
  
-   用于生成报告，请参阅[生成报表&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)。  
  
-   有关故障排除控制台中的问题，请参阅[故障排除&#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md)。  
  
