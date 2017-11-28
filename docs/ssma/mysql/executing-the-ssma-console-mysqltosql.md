---
title: "执行 SSMA 控制台 (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Script file commands, Database connection commands
- Script file commands, Manageability commands
- Script file commands, Migration commands
- Script file commands, Migration preparation commands
- Script file commands, project commands
- Script file commands, Report commands
- Script file commands, Script generation commands
ms.assetid: e3e9f7e4-0619-4861-a202-3d5d39953b26
caps.latest.revision: "25"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5536ace7511bbbb778b9ca5c3732ff78c986afd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="executing-the-ssma-console-mysqltosql"></a>执行 SSMA 控制台 (MySQLToSQL)
Microsoft 为你提供一组可靠的脚本来执行和控制 SSMA 活动的文件命令。  
  
控制台应用程序在此部分中使用作为枚举的某些标准脚本文件命令。  
  
## <a name="project--script-file-commands"></a>项目脚本文件命令  
**Command**  
  
创建新的项目：   
                   创建新的 SSMA 项目。  
  
创建项目，打开、 保存和退出项目项目命令句柄。  
  
**脚本**  
  
1.  `project-folder`指示获取创建的项目的文件夹。  
  
2.  `project-name`指示项目的名称。 {字符串}  
  
3.  `overwrite-if-exists`可选特性指示是否应覆盖现有项目。 {布尔值}  
  
4.  `project-type:`可选特性。 指示项目类型即"sql server 2005"项目或"sql server 2008"项目或"sql server 2012"或"sql server 2014"项目或"sql azure"项目。 默认值为"sql server 2008"。  
  
**语法示例：**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type==”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”   (optional)  
  
/>  
```  
覆盖-如果-存在的属性是**false**默认情况下。  
  
属性项目类型是**sql server 2008**默认情况下。  
  
**Command**  
  
打开项目：   
                  打开现有的项目。  
  
**脚本**  
  
1.  `project-folder`指示获取创建的项目的文件夹。 如果指定的文件夹不存在，则该命令将失败。  {字符串}  
  
2.  `project-name`指示项目的名称。 如果指定的项目不存在，则该命令将失败。  {字符串}  
  
**语法示例：**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
> [!IMPORTANT]  
> SSMA 为 MySQL 控制台应用程序支持向后兼容性。 你将能够打开创建的以前版本的 SSMA 项目。  
  
**Command**  
  
保存项目： 将保存迁移项目。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<save-project/>  
```  
**Command**  
  
关闭项目  
                  ： 关闭迁移项目。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<save-project/>  
```  
**Command**  
  
关闭项目  
                  ： 关闭迁移项目。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
如果修改的属性是可选的**忽略**默认情况下。  
  
## <a name="database-connection-script-file-commands"></a>数据库连接脚本文件命令  
数据库连接命令帮助连接到数据库。  
  
1.  **浏览**控制台中不支持的 UI 的功能。  
  
2.  **Windows 身份验证**和**端口**连接到 SQL Azure 时，参数不适用。  
  
3.  创建脚本文件的详细信息，请参阅[创建脚本文件 &#40;MySQLToSQL &#41;](../../ssma/mysql/creating-script-files-mysqltosql.md).  
  
**Command**  
  
连接源数据库  
  
-   执行与源数据库的连接并加载的高级别的元数据的源数据库但不是所有元数据。  
  
-   如果无法建立到源的连接，会生成错误并且控制台应用程序会进一步停止执行  
  
**脚本**  
  
从定义的服务器部分中的每个连接的服务器连接文件或脚本文件的名称特性中检索服务器定义。  
  
**语法示例：**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
强制负载-源/目标的数据库  
  
-   加载源元数据。  
  
-   用于处理脱机迁移项目。  
  
-   如果无法建立到源/目标连接，会生成错误和控制台应用程序将停止进一步执行  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
**语法示例：**  
  
```xml  
<force-load metabase="<source/target>"  
  
      <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
重新连接源数据库  
  
1.  重新连接到源数据库，但不会加载与连接源数据库命令的任何元数据。  
  
2.  如果无法建立 (re) 与源的连接，会生成错误和控制台应用程序将停止进一步执行。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
连接目标数据库  
  
1.  连接到目标 SQL Server 或 SQL Azure 数据库并完全加载的目标数据库的高级别元数据，但不是元数据。  
  
2.  如果无法建立到目标连接，会生成错误和控制台应用程序将停止进一步执行。  
  
**脚本**  
  
从定义的服务器部分中的每个连接的服务器连接文件或脚本文件的名称特性中检索服务器定义  
  
**语法示例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
重新连接目标数据库  
  
1.  重新连接到目标数据库，但不会加载任何元数据，与不同的是连接目标数据库命令。  
  
2.  如果无法建立 (re) 连接到目标，生成错误和控制台应用程序将停止进一步执行。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>报表脚本文件命令  
报表命令生成有关各种 SSMA 控制台活动的性能报告。  
  
**Command**  
  
生成评估报表  
  
1.  生成对源数据库的评估报表。  
  
2.  如果执行此命令，将生成错误并控制台应用程序退出，则不会执行源数据库连接。  
  
3.  命令在执行期间，连接到源数据库服务器失败也会导致终止控制台应用程序。  
  
**脚本**  
  
1.  `assessment-report-folder:`指定评估报表可以存储在其中的文件夹。（可选属性）  
  
2.  `object-name:`指定被认为是评估报表生成 （它可以具有单独的对象名称或组对象名称） 的对象。  
  
3.  `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
4.  `assessment-report-overwrite:`指定是否要覆盖评估报表文件夹，如果它已存在。  
  
    **默认值：** false。 （可选属性）  
  
5.  `write-summary-report-to:`指定将生成摘要报表的路径。  
  
    如果只提到的文件夹路径，然后按名称文件**AssessmentReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors`（="true/false"，使用默认为"false"（可选属性））  
  
    -   `verbose`（="true/false"，使用默认为"false"（可选属性））  
  
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
迁移命令将目标数据库架构转换为源架构，并将数据迁移到目标服务器。  
  
迁移命令设置了默认控制台输出，则与不进行详细的错误报告的完整输出报告： 源对象树的根节点处仅摘要。  
  
**Command**  
  
转换架构  
  
1.  执行架构转换从源到目标架构。  
  
2.  如果源或目标数据库连接不执行在执行此命令之前或在命令执行过程中与源或目标数据库服务器的连接失败，则会生成错误并控制台应用程序退出。  
  
**脚本**  
  
1.  `conversion-report-folder:`指定评估报表可以存储在其中的文件夹。（可选属性）  
  
2.  `object-name:`指定进行转换 （它可以具有 indivdual 对象名称或组对象名称） 的架构被视为对象。  
  
3.  `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
4.  `conversion-report-overwrite:`指定是否要覆盖评估报表文件夹，如果它已存在。  
  
    **默认值：** false。 （可选属性）  
  
5.  `write-summary-report-to:`指定将生成摘要报表的路径。  
  
    如果只提到的文件夹路径，然后按名称文件**SchemaConversionReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    摘要报表创建具有两个其他子类别：  
  
    -   `report-errors`（="true/false"，使用默认为"false"（可选属性））  
  
    -   `verbose`（="true/false"，使用默认为"false"（可选属性））  
  
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
  
1.  `object-name:`指定被视为用于迁移的源对象数据 （它可以具有 indivdual 对象名称或组对象名称）。  
  
2.  `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
3.  `write-summary-report-to:`指定将生成摘要报表的路径。  
  
    如果只提到的文件夹路径，然后按名称文件**DataMigrationReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors`（="true/false"，使用默认为"false"（可选属性））  
  
    -   `verbose`（="true/false"，使用默认为"false"（可选属性））  
  
**语法示例：**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>”  
  
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
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true"/>  
```  
  
## <a name="migration-preparation-script-file-command"></a>迁移准备脚本文件命令  
迁移准备命令会启动源和目标数据库之间的架构映射。  
  
**Command**  
  
映射架构  
  
架构映射到目标架构的源数据库。  
  
**脚本**  
  
1.  `source-schema`指定我们想要迁移的源架构。  
  
2.  `sql-server-schema`指定希望它要迁移的目标架构。  
  
**语法示例：**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>可管理性脚本文件命令  
可管理性命令帮助将目标数据库对象与源数据库同步。  
  
> [!NOTE]  
> 迁移命令设置了默认控制台输出，则与不进行详细的错误报告的完整输出报告： 源对象树的根节点处仅摘要。  
  
**Command**  
  
同步目标  
  
1.  将目标对象与目标数据库同步。  
  
2.  如果针对源数据库执行此命令，则被遇到错误。  
  
3.  如果在执行此命令之前不执行目标数据库连接或连接到的目标数据库服务器在命令执行期间失败，则生成错误并控制台应用程序退出。  
  
**脚本**  
  
1.  `object-name:`指定被视为与目标数据库 （它可以具有 indivdual 对象名称或组对象名称） 进行同步的对象。  
  
2.  `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
3.  `on-error:`指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
    -   为警告报告总数  
  
    -   报表-每个-作为-警告  
  
    -   失败脚本  
  
4.  `report-errors-to:`为同步操作 （可选） 如果只提供了文件夹路径，然后将文件按名称指定了错误报告位置**TargetSynchronizationReport.XML**创建。  
  
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
  
从数据库中刷新  
  
1.  刷新数据库中的源对象。  
  
2.  如果针对目标数据库执行此命令，则会生成错误。  
  
**脚本**  
  
1.  `object-name:`指定视为刷新从 （它可以具有 indivdual 对象名称或组对象名称） 的源数据库的源对象。  
  
2.  `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
3.  `on-error:`指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
    -   为警告报告总数  
  
    -   报表-每个-作为-警告  
  
    -   失败脚本  
  
4.  `report-errors-to:`为同步操作 （可选） 如果只提供了文件夹路径，然后将文件按名称指定了错误报告位置**SourceDBRefreshReport.XML**创建。  
  
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
  
## <a name="script-generation-script-file-commands"></a>脚本生成脚本文件命令  
脚本生成命令执行双重任务： 它们帮助节省控制台输出在脚本文件;并记录到控制台或基于你指定的参数文件的 T-SQL 的输出。  
  
**Command**  
  
保存为脚本  
  
用于将对象的脚本保存到文件时提到元数据库 = 目标，这是同步命令，其中在我们获取脚本脚本并在目标数据库上执行相同的替代方法。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
1.  `object-name:`指定其脚本将保存的对象。 （它可以具有 indivdual 对象名称或组对象名称）  
  
2.  `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
3.  `metabase:`指定它是否是源或目标元数据库。  
  
4.  `destination:`指定的路径或其中脚本已保存，如果文件没有给定的名称然后文件名格式 （object_name 属性值）.out 中的文件夹  
  
5.  `overwrite:`如果为 true 然后它将覆盖如果存在相同的文件名。 它可具有的值 (true/false)。  
  
**语法示例：**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file-name/folder-name>”  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file-name/folder-name>”  
  
      <metabase-object object-name="<object-name>"  
  
            object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Command**  
  
转换 sql 语句  
  
1.  `context`指定的架构名称。  
  
2.  `destination`指定是否应将输出存储在文件中。  
  
    如果未指定此属性，则在控制台上显示转换后的 T-SQL 的语句。 （可选属性）  
  
3.  `conversion-report-folder`指定评估报表可以存储在其中的文件夹。（可选属性）  
  
4.  `conversion-report-overwrite`指定是否要覆盖评估报表文件夹，如果它已存在。  
  
    **默认值：** false。 （可选属性）  
  
5.  `write-converted-sql-to`指定的文件 （或） 存储转换后的 T-SQL 所在的文件夹路径。 当与指定的文件夹路径`sql-files`属性，每个源文件将具有相应的目标的指定文件夹下创建的 T-SQL 文件。 当与指定的文件夹路径`sql`属性，转换后的 T-SQL 的写入到指定的文件夹下名为 Result.out 的文件。  
  
6.  `sql`指定要转换一个或多个语句的 MySQL sql 语句可以使用分隔";"  
  
7.  `sql-files`指定的路径的 sql 文件具有要转换为 T-SQL 代码。  
  
8.  `write-summary-report-to`指定将生成摘要报表的路径。 如果只提到的文件夹路径，然后按名称文件**ConvertSQLReport.XML**创建。 （可选属性）  
  
    创建具有 viz 进一步子类别的 2 的报表。。，：  
  
    -   报告错误 （="true/false"，使用默认为"false"（可选属性））。  
  
    -   详细 （="true/false"，使用默认为"false"（可选属性））。  
  
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
有关命令行选项的信息，请参阅[SSMA 控制台 &#40; 中的命令行选项MySQLToSQL &#41;](../../ssma/mysql/command-line-options-in-ssma-console-mysqltosql.md) .  
  
示例控制台脚本文件的详细信息，请参阅[使用控制台中的示例脚本文件 &#40;MySQLToSQL &#41;](../../ssma/mysql/working-with-the-sample-console-script-files-mysqltosql.md)  
  
下一步取决于您的项目要求：  
  
1.  用于指定的密码或导出 / 导入密码，请参阅[管理密码 &#40;MySQLToSQL &#41;](../../ssma/mysql/managing-passwords-mysqltosql.md).  
  
2.  有关生成报表，请参阅[生成报表 &#40;MySQLToSQL &#41;](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
3.  有关故障排除控制台中的问题，请参阅[故障排除 &#40;MySQLToSQL &#41;](../../ssma/mysql/troubleshooting-mysqltosql.md).  
  
