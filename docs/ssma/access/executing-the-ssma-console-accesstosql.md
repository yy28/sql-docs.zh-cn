---
title: "执行 SSMA 控制台 (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
caps.latest.revision: 25
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 76f31cffc8f947449d6825a6659b1bb22e0c0b1d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="executing-the-ssma-console-accesstosql"></a>执行 SSMA 控制台 (AccessToSQL)
Microsoft 为你提供了一组可靠的脚本文件命令和命令行选项来执行和控制 SSMA 活动。 接下来的部分详细介绍相同。  
  
## <a name="project--script-file-commands"></a>项目脚本文件命令  
创建项目，打开、 保存和退出项目项目命令句柄。  
  
**Command**  
  
创建新的项目： 创建一个新的 SSMA 项目。  
  
**脚本**  
  
-   `project-folder`指示获取创建的项目的文件夹。  
  
-   `project-name`指示项目的名称。 {字符串}  
  
-   `overwrite-if-exists`可选特性指示是否应覆盖现有项目。 {布尔值}  
  
-   `project-type`是一个可选属性。  对于项目类型有以下选项：  
  
    -   sql server 2005  
  
    -   sql server 2008  
  
    -   sql server 2012  
  
    -   sql server 2014  
  
    -   sql server 2016  
  
    -   sql azure  
  
    默认值为"sql server 2008"。  
  
**示例：**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type=”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”  
  
/>  
```  
覆盖-如果-存在的属性是**false**默认情况下。  
  
属性项目类型是**sql server 2008**默认情况下。  
  
**Command**  
  
打开项目： 打开现有项目。  
  
**脚本**  
  
-   `project-folder`指示获取创建的项目的文件夹。 如果指定的文件夹不存在，则该命令将失败。  {字符串}  
  
-   `project-name`指示项目的名称。 如果指定的项目不存在，则该命令将失败。  {字符串}  
  
**语法示例：**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
**注意：** SSMA 为访问控制台应用程序支持向后兼容性。 你将能够打开创建的以前版本的 SSMA 项目。  
  
**Command**  
  
保存项目： 将保存迁移项目。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<save-project/>  
```  
**Command**  
  
关闭项目： 关闭迁移项目。  
  
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
  
**浏览**控制台中不支持的 UI 的功能。  
  
**Windows 身份验证**和**端口**连接到 SQL Azure 时，参数不适用。  
  
创建脚本文件的详细信息，请参阅[创建脚本文件 &#40;AccessToSQL &#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
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
  
负载 access 数据库： 用于加载 access 数据库文件  
  
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
  
强制负载-源/目标的数据库  
  
-   加载源元数据。  
  
-   用于处理脱机迁移项目。  
  
-   如果无法建立到源/目标连接，会生成错误和控制台应用程序将停止进一步执行  
  
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
  
重新连接源数据库  
  
-   重新连接到源数据库，但不会加载与连接源数据库命令的任何元数据。  
  
-   如果无法建立 (re) 与源的连接，会生成错误和控制台应用程序将停止进一步执行。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
连接目标数据库  
  
-   连接到目标 SQL Server 或 SQL Azure 数据库并完全加载的目标数据库的高级别元数据，但不是元数据。  
  
-   如果无法建立到目标连接，会生成错误和控制台应用程序将停止进一步执行。  
  
**脚本**  
  
从定义的服务器部分中的每个连接的服务器连接文件或脚本文件的名称特性中检索服务器定义  
  
**语法示例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
重新连接目标数据库  
  
-   重新连接到目标数据库，但不会加载任何元数据，与不同的是连接目标数据库命令。  
  
-   如果无法建立 (re) 连接到目标，生成错误和控制台应用程序将停止进一步执行。  
  
**脚本**  
  
**语法示例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>报表脚本文件命令  
报表命令生成有关各种 SSMA 控制台活动的性能报告。  
  
**Command**  
  
生成评估报表  
  
-   生成对源数据库的评估报表。  
  
-   如果执行此命令，将生成错误并控制台应用程序退出，则不会执行源数据库连接。  
  
-   命令在执行期间，连接到源数据库服务器失败也会导致终止控制台应用程序。  
  
**脚本**  
  
-   `assessment-report-folder:`指定评估报表可以存储在其中的文件夹。（可选属性）  
  
-   `object-name:`指定被认为是评估报表生成 （它可以具有 indivdual 对象名称或组对象名称） 的对象。  
  
-   `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
-   `assessment-report-overwrite:`指定是否要覆盖评估报表文件夹，如果它已存在。  
  
    **默认值：** false。 （可选属性）  
  
-   `write-summary-report-to:`指定将生成报表的路径。  
  
    如果只提到的文件夹路径，然后按名称文件**AssessmentReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors`（="true/false"，使用默认为"false"（可选属性））  
  
    -   `verbose`（="true/false"，使用默认为"false"（可选属性））  
  
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
迁移命令将目标数据库架构转换为源架构，并将数据迁移到目标服务器。  
  
迁移命令设置了默认控制台输出，则与不进行详细的错误报告的完整输出报告： 源对象树的根节点处仅摘要。  
  
**Command**  
  
转换架构  
  
-   执行架构转换从源到目标架构。  
  
-   如果源或目标数据库连接不执行在执行此命令之前或在命令执行过程中与源或目标数据库服务器的连接失败，则会生成错误并控制台应用程序退出。  
  
**脚本**  
  
-   `conversion-report-folder:`指定可以在其中存储评估报表文件夹。（可选属性）  
  
-   `object-name:`指定进行转换 （它可以具有 indivdual 对象名称或组对象名称） 的架构被视为源对象。  
  
-   `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
-   `conversion-report-overwrite:`指定是否要覆盖评估报表文件夹，如果它已存在。  
  
    **默认值：** false。 （可选属性）  
  
-   `write-summary-report-to:`指定将生成报表的路径。  
  
    如果只提到的文件夹路径，然后按名称文件**SchemaConversionReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors`（="true/false"，使用默认为"false"（可选属性））  
  
    -   `verbose`（="true/false"，使用默认为"false"（可选属性））  
  
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
  
迁移数据  
  
1.  将源数据迁移到目标。  
  
**脚本**  
  
-   `object-name:`指定被视为用于迁移的源对象数据 （它可以具有 indivdual 对象名称或组对象名称）。  
  
-   `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
-   `write-summary-report-to:`指定将生成报表的路径。  
  
    如果只提到的文件夹路径，然后按名称文件**DataMigrationReport&lt;n&gt;。XML**创建。 （可选属性）  
  
    报表创建具有两个其他子类别：  
  
    -   `report-errors`（="true/false"，使用默认为"false"（可选属性））  
  
    -   `verbose`（="true/false"，使用默认为"false"（可选属性））  
  
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
  
链接表： 此命令链接到的目标表的源表 （访问）。  
  
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
  
取消链接表： 此命令将取消目标表中的源表 （访问） 的链接。  
  
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
迁移准备命令会启动源和目标数据库之间的架构映射。  
  
**Command**  
  
映射架构： 架构映射到目标架构的源数据库。  
  
**脚本**  
  
-   `source-schema`指定我们想要迁移的源架构。  
  
-   `sql-server-schema`指定希望它要迁移的目标架构。  
  
**语法示例：**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>可管理性命令  
可管理性命令帮助将目标数据库对象与源数据库同步。  
  
迁移命令设置了默认控制台输出，则与不进行详细的错误报告的完整输出报告： 源对象树的根节点处仅摘要。  
  
**Command**  
  
同步目标  
  
1.  将目标对象与目标数据库同步。  
  
2.  如果针对源数据库执行此命令，则被遇到错误。  
  
3.  如果在执行此命令之前不执行目标数据库连接或连接到的目标数据库服务器在命令执行期间失败，则生成错误并控制台应用程序退出。  
  
**脚本**  
  
1.  `object-name:`指定与目标数据库 （它可以具有 indivdual 对象名称或组对象名称） 进行同步视为目标对象。  
  
2.  `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
3.  `on-error:`指定是否为警告或错误指定同步错误。 错误上的可用选项包括：  
  
    -   为警告报告总数  
  
    -   报表-每个-作为-警告  
  
    -   失败脚本  
  
4.  `report-errors-to:`为同步操作 （可选） 如果只提供了文件夹路径，然后将文件按名称指定了错误报告位置**TargetSynchronizationReport.XML**创建。  
  
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
  
从数据库中刷新  
  
-   刷新数据库中的源对象。  
  
-   如果针对目标数据库执行此命令，则会生成错误。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
1.  `object-name:`指定视为刷新从 （它可以具有 indivdual 对象名称或组对象名称） 的源数据库的源对象。  
  
2.  `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
3.  `on-error:`指定是否为警告或错误指定刷新错误。 错误上的可用选项包括：  
  
    -   为警告报告总数  
  
    -   报表-每个-作为-警告  
  
    -   失败脚本  
  
4.  `report-errors-to:`刷新操作 （可选） 如果只提供了文件夹路径，然后将文件按名称指定的错误报告的位置**SourceDBRefreshReport.XML**创建。  
  
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
  
## <a name="script-generation-script-file-commands"></a>脚本生成脚本文件命令  
命令帮助脚本生成将控制台输出保存在脚本文件。  
  
**Command**  
  
保存为脚本  
  
用于将对象的脚本保存到文件时提到元数据库 = 目标，这是同步命令，其中在我们获取脚本脚本并在目标数据库上执行相同的替代方法。  
  
**脚本**  
  
作为命令行参数需要一个或多个元数据库节点。  
  
-   `object-name:`指定其脚本将保存的对象。 （可以单独的对象名称或组对象名称）  
  
-   `object-type:`指定的类型 （如果指定对象类别，则对象类型将为"类别"） 中的对象名称属性指定的对象。  
  
-   `metabase:`指定它是否是源或目标元数据库。  
  
-   `destination:`指定的路径或其中脚本已保存，如果文件没有给定的名称然后文件名格式 （object_name 属性值）.out 中的文件夹  
  
-   `overwrite:`如果为 true 然后它将覆盖如果存在相同的文件名。 它可具有的值 (true/false)。  
  
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
有关命令行选项的信息，请参阅[SSMA 控制台 &#40; 中的命令行选项AccessToSQL &#41;](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) .  
  
示例控制台脚本文件的信息，请参阅[SSMA 控制台 &#40; 使用示例控制台脚本文件执行AccessToSQL &#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
下一步取决于您的项目要求：  
  
-   用于指定的密码或导出 / 导入密码，请参阅[管理密码 &#40;AccessToSQL &#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
-   有关生成报表，请参阅[生成报表 &#40;AccessToSQL &#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
-   有关故障排除控制台中的问题，请参阅[故障排除 &#40;AccessToSQL &#41;](../../ssma/access/troubleshooting-accesstosql.md).  
  

