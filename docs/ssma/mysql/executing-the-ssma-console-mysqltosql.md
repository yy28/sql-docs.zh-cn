---
title: 执行 SSMA 控制台 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Script file commands, Database connection commands
- Script file commands, Manageability commands
- Script file commands, Migration commands
- Script file commands, Migration preparation commands
- Script file commands, project commands
- Script file commands, Report commands
- Script file commands, Script generation commands
ms.assetid: e3e9f7e4-0619-4861-a202-3d5d39953b26
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 761cb5368c0b586b63f92952f3938d8708daaf86
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411254"
---
# <a name="executing-the-ssma-console-mysqltosql"></a>执行 SSMA 控制台 (MySQLToSQL)
Microsoft 你提供一组可靠的脚本来执行和控制 SSMA 活动文件命令。  
  
控制台应用程序在本部分中使用作为枚举的某些标准脚本文件命令。  
  
## <a name="project--script-file-commands"></a>项目脚本文件命令  
**Command**  
  
创建新的项目：   
                   创建新的 SSMA 项目。  
  
创建项目、 打开、 保存和退出项目项目命令句柄。  
  
**脚本**  
  
1.  `project-folder` 指示获取创建的项目的文件夹。  
  
2.  `project-name` 指示项目的名称。 {string}  
  
3.  `overwrite-if-exists`可选属性指示是否应覆盖现有项目。 {布尔值}  
  
4.  `project-type:`可选属性。 指示项目类型即"sql server 2005"项目或"sql server 2008"项目或"sql server 2012"或"sql server 2014"项目或"sql azure"项目。 默认值为"sql server 2008"。  
  
**语法示例：**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type=="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"   (optional)  
  
/>  
```  
覆盖如果-共存的属性是**false**默认情况下。  
  
项目类型属性是**sql server 2008**默认情况下。  
  
**Command**  
  
打开项目：   
                  打开现有的项目。  
  
**脚本**  
  
1.  `project-folder` 指示获取创建的项目的文件夹。 如果指定的文件夹不存在，则命令将失败。  {string}  
  
2.  `project-name` 指示项目的名称。 如果指定的项目不存在，则命令将失败。  {string}  
  
**语法示例：**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
> [!IMPORTANT]  
> SSMA MySQL 控制台应用程序的支持向后兼容性。 你将能够打开创建的以前版本的 SSMA 项目。  
  
**Command**  
  
保存项目：保存迁移项目。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<save-project/>  
```  
**Command**  
  
关闭项目  
                  解码的字符：关闭迁移项目。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<save-project/>  
```  
**Command**  
  
关闭项目  
                  解码的字符：关闭迁移项目。  
  
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
  
1.  **浏览**在控制台中不支持 UI 的功能。  
  
2.  **Windows 身份验证**并**端口**连接到 SQL Azure 时，参数不适用。  
  
3.  创建脚本文件的详细信息，请参阅[创建脚本文件&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md)。  
  
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
  
force-load-source/target-database  
  
-   加载源元数据。  
  
-   用于处理脱机迁移项目。  
  
-   如果无法建立与源/目标的连接，会生成错误并停止进一步执行控制台应用程序。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
**语法示例：**  
  
```xml  
<force-load metabase="<source/target>"  
  
      <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
reconnect-source-database  
  
1.  重新连接到源数据库，但不会加载与连接源数据库命令不同的任何元数据。  
  
2.  如果无法建立 （重新） 与源的连接，会生成错误和控制台应用程序停止进一步执行。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
连接目标数据库  
  
1.  连接到目标 SQL Server 或 SQL Azure 数据库并完全加载目标数据库的高级别的元数据，但不是元数据。  
  
2.  如果无法建立到目标连接，会生成错误和控制台应用程序停止进一步执行。  
  
**脚本**  
  
从服务器部分中的服务器连接文件或脚本文件的每个连接而定义的 name 属性检索服务器定义  
  
**语法示例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
1.  重新连接到目标数据库，但不会加载任何元数据，与连接目标数据库命令不同。  
  
2.  如果无法建立 （重新） 连接到目标，生成错误和控制台应用程序停止进一步执行。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>报表脚本文件命令  
报表命令生成各种 SSMA 控制台活动的性能上的报表。  
  
**Command**  
  
generate-assessment-report  
  
1.  生成对源数据库的评估报告。  
  
2.  如果执行此命令之前不执行源数据库连接，则会生成错误和控制台应用程序退出。  
  
3.  命令执行期间，连接到源数据库服务器失败也会终止的控制台应用程序。  
  
**脚本**  
  
1.  `assessment-report-folder:` 指定评估报告可以在其中存储的文件夹。（可选属性）  
  
2.  `object-name:` 指定的生成评估报告 （它可以具有单独的对象名称或组对象名称） 时要考虑的对象。  
  
3.  `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
4.  `assessment-report-overwrite:` 指定是否覆盖评估报表文件夹已存在。  
  
    **默认值：** false。 （可选属性）  
  
5.  `write-summary-report-to:` 指定将生成摘要报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**AssessmentReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration--script-file-commands"></a>迁移脚本文件命令  
迁移命令将目标数据库架构转换为源架构和数据迁移到目标服务器。  
  
设置的迁移命令的默认控制台输出是使用不进行详细的错误报告的完整的输出报表：在源对象树的根节点的唯一摘要。  
  
**Command**  
  
convert-schema  
  
1.  执行架构转换从源到目标架构。  
  
2.  如果执行此命令之前不执行源或目标数据库连接或连接到源或目标数据库服务器失败命令执行时，会生成错误和控制台应用程序退出。  
  
**脚本**  
  
1.  `conversion-report-folder:` 指定评估报告可以在其中存储的文件夹。（可选属性）  
  
2.  `object-name:` 指定用于转换 （可能包含单个对象名或组对象名称） 的架构被视为对象。  
  
3.  `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
4.  `conversion-report-overwrite:` 指定是否覆盖评估报表文件夹已存在。  
  
    **默认值：** false。 （可选属性）  
  
5.  `write-summary-report-to:` 指定将生成摘要报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**SchemaConversionReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    摘要报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<convert-schema  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-names>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Command**  
  
迁移数据  
  
1.  将源数据迁移到目标。  
  
**脚本**  
  
1.  `object-name:` 指定被视为用于迁移的源对象 （可能包含单个对象名或组对象名称） 的数据。  
  
2.  `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
3.  `write-summary-report-to:` 指定将生成摘要报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**DataMigrationReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="true" verbose="true">  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <data-migration-connection  
  
         source-use-last-used="true"/source-server="<server-unique-name>"  
  
         target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
或  
  
```xml  
<migrate-data  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="true" verbose="true"/>  
```  
  
## <a name="migration-preparation-script-file-command"></a>迁移准备脚本文件命令  
迁移准备命令开始架构源和目标数据库之间的映射。  
  
**Command**  
  
映射架构  
  
源数据库到目标架构的架构映射。  
  
**脚本**  
  
1.  `source-schema` 指定我们想要迁移的源架构。  
  
2.  `sql-server-schema` 指定我们想要的位置要迁移的目标架构。  
  
**语法示例：**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>可管理性的脚本文件命令  
可管理性命令可帮助将与源数据库同步目标数据库对象。  
  
> [!NOTE]  
> 设置的迁移命令的默认控制台输出是使用不进行详细的错误报告的完整的输出报表：在源对象树的根节点的唯一摘要。  
  
**Command**  
  
同步目标  
  
1.  将目标对象与目标数据库同步。  
  
2.  如果对源数据库执行此命令时，遇到错误。  
  
3.  如果执行此命令之前不执行目标数据库连接或连接到目标数据库服务器失败命令执行时，会生成错误和控制台应用程序退出。  
  
**脚本**  
  
1.  `object-name:` 指定被视为与目标数据库 （可能包含单个对象名或组对象名称） 进行同步的对象。  
  
2.  `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
3.  `on-error:` 指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
    -   作为警告报告总数  
  
    -   报表的每个-作为-警告  
  
    -   脚本失败  
  
4.  `report-errors-to:` 为同步操作 （以属性为可选） 如果仅指定文件夹路径，然后将文件按名称指定的错误报告位置**TargetSynchronizationReport.XML**创建。  
  
**语法示例：**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
/>  
```  
或  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
或  
  
```xml  
<synchronize-target>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
**Command**  
  
从数据库刷新  
  
1.  刷新数据库中的源对象。  
  
2.  如果对目标数据库执行此命令，则会生成错误。  
  
**脚本**  
  
1.  `object-name:` 指定用于刷新 （可能包含单个对象名或组对象名称） 的源数据库中被视为源对象。  
  
2.  `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
3.  `on-error:` 指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
    -   作为警告报告总数  
  
    -   报表的每个-作为-警告  
  
    -   脚本失败  
  
4.  `report-errors-to:` 为同步操作 （以属性为可选） 如果仅指定文件夹路径，然后将文件按名称指定的错误报告位置**SourceDBRefreshReport.XML**创建。  
  
作为命令行参数需要一个或多个元数据库节点。  
  
**语法示例：**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
/>  
```  
或  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
或  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>脚本生成的脚本文件命令  
生成脚本命令执行双重任务：它们帮助节省控制台输出中的脚本文件;并记录到控制台或根据你指定的参数文件的 T-SQL 的输出。  
  
**Command**  
  
save-as-script  
  
用于将对象的脚本保存到文件时提到元数据库 = 目标，这是在其中中我们获取脚本并执行相同目标数据库上的同步命令的替代方法。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
1.  `object-name:` 指定的脚本将保存的对象。 （可能包含单个对象名或组对象名称）  
  
2.  `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
3.  `metabase:` 指定是否在源或目标元数据库。  
  
4.  `destination:` 指定的路径或其中脚本已保存，如果文件名称中未给然后文件名称格式 （object_name 属性值）.out 的文件夹  
  
5.  `overwrite:` 如果为 true 则它将覆盖存在相同的文件名。 它可以具有值 (true/false)。  
  
**语法示例：**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file-name/folder-name>"  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file-name/folder-name>"  
  
      <metabase-object object-name="<object-name>"  
  
            object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Command**  
  
convert-sql-statement  
  
1.  `context` 指定架构名称。  
  
2.  `destination` 指定是否应将输出存储在文件中。  
  
    如果未指定此属性，则会在控制台上显示转换后的 T-SQL 语句。 （可选属性）  
  
3.  `conversion-report-folder` 指定评估报告可以在其中存储的文件夹。（可选属性）  
  
4.  `conversion-report-overwrite` 指定是否覆盖评估报表文件夹已存在。  
  
    **默认值：** false。 （可选属性）  
  
5.  `write-converted-sql-to` 指定的文件 （或） 存储已转换的 T-SQL 所在的文件夹路径。 与指定的文件夹路径时`sql-files`属性，每个源文件将有相应的目标指定的文件夹下创建的 T-SQL 的文件。 与指定的文件夹路径时`sql`属性，已转换的 T-SQL 写入指定文件夹下名为 Result.out 的文件。  
  
6.  `sql` 指定要进行转换，一个或多个语句的 MySQL sql 语句可以使用分隔";"  
  
7.  `sql-files` 指定的路径的 sql 文件具有要转换为 T-SQL 代码。  
  
8.  `write-summary-report-to` 指定将生成摘要报表的路径。 如果只提到的文件夹路径，然后将文件按名称**ConvertSQLReport.XML**创建。 （可选属性）  
  
    创建具有 viz 进一步子类别的 2 的报表..,:  
  
    -   报告错误 （="true/false"，为"false"（可选属性） 的默认值）。  
  
    -   详细 （="true/false"，默认值为"false"（可选属性））。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
**语法示例：**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="stdout/file"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
      <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
或  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
或  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>下一步  
有关命令行选项的信息，请参阅[SSMA 控制台中的命令行选项&#40;MySQLToSQL&#41; ](../../ssma/mysql/command-line-options-in-ssma-console-mysqltosql.md) 。  
  
示例控制台脚本文件的详细信息，请参阅[使用示例控制台脚本文件&#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-the-sample-console-script-files-mysqltosql.md)  
  
下一步取决于你的项目要求：  
  
1.  用于指定密码或导出 / 导入密码，请参阅[管理密码&#40;MySQLToSQL&#41;](../../ssma/mysql/managing-passwords-mysqltosql.md)。  
  
2.  用于生成报告，请参阅[生成报表&#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md)。  
  
3.  有关故障排除控制台中的问题，请参阅[故障排除&#40;MySQLToSQL&#41;](../../ssma/mysql/troubleshooting-mysqltosql.md)。  
  
