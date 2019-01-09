---
title: 执行 SSMA 控制台 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cbdd0a1394114e3fdef0511c7ed14658f7dd9b0
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52406404"
---
# <a name="executing-the-ssma-console-sybasetosql"></a>执行 SSMA 控制台 (SybaseToSQL)
Microsoft 你提供一组可靠的脚本来执行和控制 SSMA 活动文件命令。 接下来的几节详细介绍相同。  
  
## <a name="script-file-commands"></a>脚本文件命令  
控制台应用程序在本部分中使用作为枚举的某些标准脚本文件命令。  
  
## <a name="project-commands"></a>项目命令  
创建项目、 打开、 保存和退出项目项目命令句柄。  
  
### <a name="create-new-project"></a>创建新的项目  
此命令创建新的 SSMA 项目。  
  
-   `project-folder` 指示获取创建的项目的文件夹。  
  
-   `project-name` 指示项目的名称。 {string}  
  
-   `overwrite-if-exists`可选属性指示是否应覆盖现有项目。 {布尔值}  
  
-   `project-type:`可选属性。 指示项目类型，即"sql server 2005"项目或"sql server 2008"项目或的"sql server 2012"项目或"sql server 2014"项目或的"sql azure"项目。 默认值是"sql server-2008。  
  
**语法示例：**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type="<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>"  
/>  
```  
覆盖如果-共存的属性是**false**默认情况下。  
  
项目类型属性是**sql server 2008**默认情况下。  
  
### <a name="open-project"></a>打开项目  
此命令将打开项目。

-   `project-folder` 指示获取创建的项目的文件夹。 如果指定的文件夹不存在，则命令将失败。  {string}  
  
-   `project-name` 指示项目的名称。 如果指定的项目不存在，则命令将失败。  {string}  
  
**语法示例：**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA for SAP ASE 控制台应用程序支持向后兼容性。 可用于打开创建的以前版本的 SSMA 项目。  
  
### <a name="save-project"></a>保存项目  
此命令将保存迁移项目。  
  
**语法示例：**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>关闭项目  
此命令将关闭迁移项目。  
  
**语法示例：**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
如果修改的属性是可选的**忽略**默认情况下。  
  
## <a name="database-connection-commands"></a>数据库连接命令  
数据库连接命令可帮助连接到数据库。  
  
> [!NOTE]  
> - **浏览**在控制台中不支持 UI 的功能。  
> - 创建脚本文件的详细信息，请参阅[创建脚本文件&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)。  
  
### <a name="connect-source-database"></a>connect-source-database  
此命令执行到源数据库的连接并加载的源数据库，但不是所有元数据的高级元数据。
  
如果无法建立到源的连接，会生成错误和控制台应用程序停止进一步执行。
  
从服务器部分中的服务器连接文件或脚本文件的每个连接而定义的 name 属性中检索服务器定义。  
  
**语法示例：**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>force-load-source/target-database  
此命令加载源元数据，并可用于处理脱机迁移项目。  
  
如果无法建立与源/目标的连接，会生成错误和控制台应用程序停止进一步执行。  
  
此命令需要一个或多个元数据库节点作为命令行参数。  
  
**语法示例：**  
  
```xml  
<force-load metabase="<source/target>" >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>reconnect-source-database  
此命令重新连接到源数据库，但不会加载与连接源数据库命令不同的任何元数据。  
  
如果无法建立 （重新） 与源的连接，会生成错误和控制台应用程序停止进一步执行。  
  
**语法示例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>连接目标数据库  
此命令连接到目标 SQL Server 数据库，并完全加载目标数据库的高级元数据，但不是元数据。  
  
如果无法建立到目标连接，会生成错误和控制台应用程序停止进一步执行。  
  
从服务器部分中的服务器连接文件或脚本文件的每个连接而定义的 name 属性中检索服务器定义。  
  
**语法示例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>reconnect-target-database  
  
此命令重新连接到目标数据库，但不会加载任何元数据，与连接目标数据库命令不同。  
  
如果无法建立 （重新） 连接到目标，生成错误和控制台应用程序停止进一步执行。  
  
**语法示例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>报表命令  
报表命令生成各种 SSMA 控制台活动的性能上的报表。  
  
### <a name="generate-assessment-report"></a>generate-assessment-report  
  
此命令生成评估报告对源数据库。  
  
如果执行此命令之前不执行源数据库连接，则会生成错误和控制台应用程序退出。  
  
命令执行期间，连接到源数据库服务器失败也会终止的控制台应用程序。  
  
-   `conversion-report-folder:` 指定可以在其中存储评估报表的文件夹。 （可选属性）  
  
-   `object-name:` 指定评估报表生成 （支持单独的对象名称或组对象名称） 时要考虑的对象。  
  
-   `object-type:` 指定的对象 （如果指定了对象类别，则对象类型将为"类别"） 中的对象名称属性标出的类型。  
  
-   `conversion-report-overwrite:` 指定是否覆盖评估报表文件夹已存在。  
  
    **默认值：** false。 （可选属性）  
  
-   `write-summary-report-to:` 指定将在其中生成报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**AssessmentReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>迁移命令  
迁移命令将目标数据库架构转换为源架构和数据迁移到目标服务器。  
  
### <a name="convert-schema"></a>convert-schema  
此命令执行从源到目标架构的架构转换。  
  
如果执行此命令之前不执行源或目标数据库连接或连接到源或目标数据库服务器失败命令执行时，会生成错误和控制台应用程序退出。  
  
-   `conversion-report-folder:` 指定可以在其中存储评估报表的文件夹。 （可选属性）  
  
-   `object-name:` 指定源对象视为用于转换架构 （支持单独的对象名称或组对象名称）。  
  
-   `object-type:` 指定的对象 （如果指定了对象类别，则对象类型将为"类别"） 中的对象名称属性标出的类型。  
  
-   `conversion-report-overwrite:` 指定是否覆盖评估报表文件夹已存在。  
  
    **默认值：** false。 （可选属性）  
  
-   `write-summary-report-to:` 指定将在其中生成摘要报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**SchemaConversionReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
或  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>迁移数据  
此命令将源数据迁移到目标。  
  
-   `object-name:` 指定被视为用于迁移的源对象 （支持单独的对象名称或组对象名称） 的数据。  
  
-   `object-type:` 指定的对象 （如果指定了对象类别，则对象类型将为"类别"） 中的对象名称属性标出的类型。  
  
-   `write-summary-report-to:` 指定将在其中生成报表的路径。  
  
    如果只提到的文件夹路径，然后将文件按名称**DataMigrationReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors` （="true/false"，默认值为"false"（可选属性））  
  
    -   `verbose` （="true/false"，默认值为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
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
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>迁移准备命令  
迁移准备命令开始架构源和目标数据库之间的映射。  
  
> [!NOTE]  
> 设置的迁移命令的默认控制台输出是使用不进行详细的错误报告的完整的输出报表：在源对象树的根节点的唯一摘要。  
  
### <a name="map-schema"></a>映射架构  
此命令提供的架构映射的源数据库到目标架构。  
  
-   `source-schema` 指定要迁移的源架构。  
  
-   `sql-server-schema` 指定源架构将迁移到目标架构。  
  
**语法示例：**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>可管理性命令  
可管理性命令可帮助将与源数据库同步目标数据库对象。  
  
> [!NOTE]  
> 设置的迁移命令的默认控制台输出是使用不进行详细的错误报告的完整的输出报表：在源对象树的根节点的唯一摘要。  
  
### <a name="synchronize-target"></a>同步目标  
此命令将目标对象与目标数据库同步。  
 
如果对源数据库执行此命令时，遇到错误。  
  
如果执行此命令之前不执行目标数据库连接或连接到目标数据库服务器失败命令执行时，会生成错误和控制台应用程序退出。  
  
-   `object-name:` 指定目标对象被视为与目标数据库 （支持单独的对象名称或组对象名称） 进行同步。  
  
-   `object-type:` 指定的对象 （如果指定了对象类别，则对象类型将为"类别"） 中的对象名称属性标出的类型。  
  
-   `on-error:` 指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
    -   作为警告报告总数  
  
    -   报表的每个-作为-警告  
  
    -   脚本失败  
  
-   `report-errors-to:` 指定为同步操作 （可选属性） 的错误报告的位置。 如果仅指定文件夹路径，然后将文件按名称**TargetSynchronizationReport.XML**创建。  
  
**语法示例：**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
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
  
### <a name="refresh-from-database"></a>从数据库刷新  
此命令刷新数据库中的源对象。  
  
如果对目标数据库执行此命令，则会生成错误。  
  
此命令需要一个或多个元数据库节点作为命令行参数。  
  
-   `object-name:` 指定被视为用于刷新源数据库 （支持单独的对象名称或组对象名称） 中的源对象。  
  
-   `object-type:` 指定的类型 （如果指定了对象类别，则对象类型将为"类别"） 的对象名称属性中指定的对象。  
  
-   `on-error:` 指定是否为警告或错误调用刷新错误。 错误上的可用选项包括：  
  
    -   作为警告报告总数  
  
    -   报表的每个-作为-警告  
  
    -   脚本失败  
  
-   `report-errors-to:` 指定刷新操作 （可选属性） 的错误报告的位置。 如果仅指定文件夹路径，然后将文件按名称**SourceDBRefreshReport.XML**创建。  
  
**语法示例：**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
或  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
或  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>生成的脚本命令  
生成脚本命令执行双重任务： 它们帮助节省控制台输出中的脚本文件，并将它们记录 T-SQL 输出到控制台或根据你指定的参数文件。  
  
### <a name="save-as-script"></a>save-as-script  
此命令用于将保存到文件的对象的脚本时提到的元数据库 = 目标。 这是同步命令的替代方法，我们获取脚本并在目标数据库上执行相同。  
  
此命令需要一个或多个元数据库节点作为命令行参数。  
  
-   `object-name:` 指定的脚本将保存 （支持单独的对象名称或组对象名称） 的对象。  
  
-   `object-type:` 指定的对象 （如果指定了对象类别，则对象类型将为"类别"） 中的对象名称属性标出的类型。  
  
-   `metabase:` 指定是否在源或目标元数据库。  
  
-   `destination:` 指定的路径或必须在其中保存该脚本的文件夹。 如果未指定的文件的名称，然后将提供格式 （object_name 属性值）.out 中的文件名。
  
-   `overwrite:` 如果为 true，则它将覆盖同一文件名如果它存在。 它可以具有值 (true/false)。  
  
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
  
### <a name="convert-sql-statement"></a>convert-sql-statement
此命令将为 SQL 语句。  
  
-   `context` 指定架构名称。  
  
-   `destination` 指定是否应将输出存储在文件中。  
  
    如果未指定此属性，则会在控制台上显示转换后的 T-SQL 语句。 （可选属性）  
  
-   `conversion-report-folder` 指定可以在其中存储评估报表的文件夹。 （可选属性）  
  
-   `conversion-report-overwrite` 指定是否覆盖评估报表文件夹已存在。  
  
    **默认值：** false。 （可选属性）  
  
-   `write-converted-sql-to` 指定要存储已转换的 T-SQL 文件 （或） 的文件夹路径。 与指定的文件夹路径时`sql-files`属性，每个源文件都有一个相应的目标指定文件夹下创建的 T-SQL 的文件。 与指定的文件夹路径时`sql`属性，已转换的 T-SQL 写入指定文件夹下名为 Result.out 的文件。  
  
-   `sql` 指定要转换的 Sybase sql 语句可以使用分隔一个或多个语句";"  
  
-   `sql-files` 指定包含要转换为 T-SQL 代码的 sql 文件的路径。  
  
-   `write-summary-report-to` 指定将生成摘要报表的路径。 如果只提到的文件夹路径，然后将文件按名称**ConvertSQLReport.XML**创建。 （可选属性）  
  
    摘要报表创建具有两个其他子类别，即：  
  
    -   报告错误 （="true/false"，为"false"（可选属性） 的默认值）。  
  
    -   详细 （="true/false"，默认值为"false"（可选属性））。  
  
此命令需要一个或多个元数据库节点作为命令行参数。  
  
**语法示例：**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
或  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
或  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>后续步骤  
有关命令行选项的信息，请参阅[SSMA 控制台 (AccessToSQL) 中的命令行选项](../access/command-line-options-in-ssma-console-accesstosql.md)。  
  
有关示例控制台脚本文件的信息，请参阅[使用示例控制台脚本文件&#40;SybaseToSQL&#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
下一步取决于你的项目要求：  
  
-   用于指定密码或导出 / 导入密码，请参阅[管理密码&#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md)。  
  
-   用于生成报告，请参阅[生成报表&#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)。  
  
-   有关故障排除控制台中的问题，请参阅[故障排除&#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md)。  
  
