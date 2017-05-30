---
title: "SQL Server Data Tools (SSDT) 的更改日志 | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8798c5319cdce7b68f71868722aacfbf4cb34d9f
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="changelog-for-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) 的更改日志
此更改日志适用于随 [SQL Server 2016](https://msdn.microsoft.com/library/ms130214.aspx) 一起发布的 [SQL Server Data Tools (SSDT) for Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx)。  
  
有关新增功能和已更改功能的详细文章，请访问 [SSDT 团队博客](https://blogs.msdn.microsoft.com/ssdt/)。  

## <a name="ssdt-165-for-sql-server-2016"></a>SSDT 16.5（适用于 SQL Server 2016）
发布日期：2016 年 10 月 20日

内部版本号：14.0.61021.0

**新增功能**


### <a name="connection-improvements"></a>连接改进

* “浏览”选项卡中的新搜索框可帮助你筛选本地服务器、网络服务器和 Azure SQL 数据库。**** 如果这些列表中显示了大量的服务器或数据库，此功能将十分有用。
* “历史记录”选项卡中包含右键菜单选项用于固定/取消固定收藏项目，并提供一个新选项用于从历史记录中删除连接。****

### <a name="sqlpackage-and-dacfx-api-improvements"></a>SqlPackage 和 DacFx API 改进

现在，使用 SqlPackage.exe 和 DacFx API 可以通过一项操作来生成部署报告和部署脚本，以及发布到数据库。 对于想要保留有关部署期间发布内容的报告的任何人而言，这项改进可以节省时间。 另一项优势是，在 Azure 方案中，将会针对 master 数据库和部署目标数据库创建单独的脚本。 目前只会创建单个脚本，这对于重复部署不会起到作用。

针对 SqlPackage 的发布和脚本操作，已添加两个新参数。

* DeployScriptPath（短名称：dsp）。 这是要将部署脚本写入到的可选路径。 对于 Azure 部署，如果使用 TSQL 命令创建或修改了数据库，则会将主脚本写入相同的路径，但使用“Filename_Master.sql”作为输出文件名。
* DeployReportPath（短名称：drp）。 这是要将部署报告写入到的可选路径。

请注意，对于脚本操作，应使用现有的输出路径参数或者新的脚本/报告特定的参数，但不能同时使用两者。

示例用法：

**发布操作**

```Sqlpackage.exe /a:Publish /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

**脚本操作**

```Sqlpackage.exe /a:Script /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

在 DacFx 中已添加两个新的 API：DacServices.Publish() 和 DacServices.Script()。 这些 API 还支持通过单个操作执行发布 + 脚本 + 报告操作。 示例用法：

```
DacServices service = new DacServices(connectionString);
using(DacPackage package = DacPackage.Load(@"C:\My\db.dacpac")) {
var options = new PublishOptions() {
    GenerateDeploymentScript = true, // Should a deployment script be created?
    GenerateDeploymentReport = true, // Should an xml deploy report be created?
    DatabaseScriptPath = @"C:\My\OutputScript.sql", // optional path to save script to
    MasterDbScriptPath = @"C:\My\OutputScript_Master.sql", // optional path to save master script to
    DeployOptions = new DacDeployOptions()
};

// Call publish and receive deployment script & report in the results
PublishResult result = service.Publish(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);

// Call script and receive deployment script & report in results
result = service.Script(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);
```

**Analysis Services 和 Reporting Services**

在处理较大的 DAX 表达式时，SSAS 表格设计器 DAX 分析器的性能已得到改进。
有关详细信息，请阅读 [Analysis Services 博客文章](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/)。

### <a name="fixed--improved-this-month"></a>本月修复/改进的功能

**Database Tools**

* [连接 bug 3055711](https://connect.microsoft.com/SQLServer/feedback/details/3055711/columns-cannot-be-selected-from-cross-apply-openjson-with-explicit-schema) – 无法从使用显式架构的 CROSS APPLY OPENJSON 中选择列
* 已修复 – 自动生成的历史记录表索引问题：重新部署时 DacFx 会删除索引
* 已修复 – DacFx 批处理分析器无法分析转义的括号“]”字符，导致发布失败的问题
* 已改进 – 现在，SqlPackage 将在帮助输出中包含每个操作的说明
* 已修复 – 编辑“高级”选项以及编辑发布、架构比较和其他文件中保存的连接字符串时，连接对话框中的“记住密码”选项不会保留设置
* 已修复 – 对于“历史记录”选项卡中显示的、IntegratedAuthentication = true 的连接，连接属性中的“身份验证”字段保留空白。 现在会按预期显示“Windows 身份验证”
* 已修复 – 对“工具”->“选项”->“文本编辑器”下的“SQL Server Tools Intellisense”设置所做的更改不会保留
* 已改进 – 连接对话框中“历史记录”选项卡上的“固定”/“取消固定”按钮现在更紧凑，减少了出现滚动条的可能性
* 已修复 – 已修复连接对话框中的多个辅助功能问题。

**Analysis Services 和 Reporting Services**

* 修复了 SSDT AS 表格设计器中的一个问题：在某些情况下，单击数据网格中的滚动条 Thumb 控件会导致崩溃
* 修复了 SSDT AS 表格设计器中未提供以当前用户模拟连接的选项问题
* 修复了 SSDT AS 表格设计器中的一个问题：过度展开公式栏可能导致项目无法重新打开
* 修复了在选择表选项卡后，按键时发生 SSDT AS 表格设计器崩溃的问题
* 修复了 SSDT AS 项目中的一个问题：选择“在 Excel 中分析”不会连接到下层 AS 服务器版本

**集成服务**

* 修复了连接 bug [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks)：移动多个集成服务包任务





## <a name="ssdt-164-for-sql-server-2016"></a>SSDT 16.4（适用于 SQL Server 2016）
发布日期：2016 年 9 月 20日

内部版本号：14.0.60918

**新增功能**

现在，SqlPackage.exe 和数据层应用程序框架 (DacFx) API 支持架构比较。 有关详细信息，请参阅 [Schema Compare in SqlPackage and the Data-Tier Application Framework](https://blogs.msdn.microsoft.com/ssdt/2016/09/20/schema-compare-in-sqlpackage-and-the-data-tier-application-framework-dacfx/)（SqlPackage 和数据层应用程序框架中的架构比较）。

**Analysis Services – 适用于 SSDT Tabular 的集成工作区模式 (SSAS)**

SSDT Tabular 现在包含内部 SSAS 实例，如果启用集成工作区模式，SSDT Tabular 将在后台自动启动该实例，使你能够在模型设计器中添加和查看表、列与数据，而无需提供外部工作区服务器实例。 集成工作区模式不会更改 SSDT 表格与工作区服务器和数据库配合工作的方式。 更改的是 SSDT 表格托管工作区数据库的位置。 若要启用集成工作区模式，请在创建新表格项目时显示的“表格模型设计器”对话框中选择“集成工作区”选项。 对于当前使用显式工作区服务器的现有表格项目，可以通过在“属性”窗口（在解决方案资源管理器中选择 Model.bim 文件时会显示该窗口）中，将“集成工作区模式”参数设置为 True 切换到集成工作区模式。 有关详细信息，请参阅 [Analysis Services 博客文章](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/)。

**更新和修复**
**数据库工具：**

- [连接问题 3087775](https://connect.microsoft.com/SQLServer/feedback/details/3087775)：针对 VS Data Tools 中临时表损坏的 7 月更新 14.0.60629.0：“值不能为 null。 参数名称: reportedElement”
- [连接问题 1026648](https://connect.microsoft.com/SQLServer/feedback/details/1026648)：在 SSDT 比较结果中 IsPersistedNullable 显示为有差异
- [连接问题 2054735](https://connect.microsoft.com/SQLServer/feedback/details/2054735)：导入 BACPAC 时标识重置
- [连接问题 2900167](https://connect.microsoft.com/SQLServer/feedback/details/2900167)：运行 SSDT 单元测试会留下临时文件
- [连接问题 1807712](https://connect.microsoft.com/SQLServer/feedback/details/1807712)：破坏向后兼容性 – AppLocal 和 Nugetization

**Analysis Services 和 Reporting Services**

* 修复了 SSDT 中的一个问题：编辑 DirectQuery 的 DAX 计算列时错误提示弹出窗口会妨碍操作。
* 修复了 SSDT AS 表格网格中的一个问题：当 Windows 缩放系数设置为高 DPI 200% 以上时，KPI 图标不会显示在度量网格中。
* 修复了 SSDT AS 中的一个问题：粘贴大型表数据可能导致表格项目无响应。
* 修复了 SSDT AS 表格模型编辑器中的一个问题。现在，在重命名连接的友好名称时，会将模型标记为需要保存更改。
* 修复了 SSDT AS 表格项目中的一个问题：无法调整管理关系对话框中的列宽。
* 修复了 SSDT AS 表格 1200 级模型中的一个问题：使用“德语”等区域设置时，从 Excel 粘贴数据无法正确将逗号视为小数分隔符。
* 修复了 SSDT AS 项目中的一个问题：某些 KPI 图标集可能会产生错误“无法检索此视觉对象的数据”。
* 修复了 SSDT AS 项目属性对话框中的一个问题。现在，在以高 DPI 缩放比例调整大小时，可以正确定位。
* 修复了 SSDT AS 项目中一个可能会导致升级包含粘贴表的某些模型时出错的问题。
* 修复了 SSDT AS 中的一个问题：从 Excel 粘贴所有工作表行时速度非常缓慢，并且会创建许多不需要的列。
* 修复了 SSDT AS 中的一个问题：大型静态 DataTable 表达式的分析和突出显示速度非常缓慢，似乎已挂起。
* 修复了 SSDT AS 中的一个问题，现在会将度量值和 KPI 值添加到在编辑器中选择的当前透视图。
* 修复了 SSDT 中的一个问题：从 SQL Azure 导入 AS 项目的数据不支持除“dbo”以外的架构类型。



## <a name="ssdt-163-for-sql-server-2016"></a>SSDT 16.3（适用于 SQL Server 2016）
发布日期：2016 年 8 月 15日

内部版本号：14.0.60812.0  

**新增功能**

- **发行版本控制和编号：**现在，发行版按编号顺序而不是按月份标记。 这符合新的 SSMS 策略；当某个月份推出多个版本或修补程序时，这种版本控制方式可以简化我们的工作。 此发行版为 16.3，表示自 RTM 发行版推出之后的第三次更新。 任何修补程序的版本从 16.3.1 开始递增，下一次更新（计划在下个月推出）的版本为 16.4。
- **Analysis Services – 表格模型资源管理器：**使用表格模型资源管理器可以方便地浏览模型中的各种元数据对象，例如数据源、表、度量值和关系。 它是以单独的工具窗口实现的，在 Visual Studio 中打开“视图”菜单，指向“其他窗口”，然后单击“表格模型资源管理器”即可显示。 表格模型资源管理器默认显示在单独选项卡上的“解决方案资源管理器”区域中。 表格模型资源管理器在树结构中组织元数据对象，该结构和 1200 表格模型的架构很相似，并提供其他许多新功能。
- **数据库工具 – Always Encrypted**：此发行版提供新的“Always Encrypted 密钥管理”对话框，方便你在数据库项目中添加列主密钥或列加密密钥，或者在 SQL Server 对象资源管理器中添加实时数据库。[](https://msdn.microsoft.com/library/mt708953.aspx) 此发行版支持 Windows 证书存储中的证书。 以后的发行版将支持 Azure Key Vault 和 CNG 提供程序。
    - 创建列主密钥或列加密密钥时，单击“更新数据库”后，更改可能不会立即显示在 SQL Server 对象资源管理器中。 若要解决此问题，可在 SQL Server 对象资源管理器中刷新数据库节点。
    - 如果尝试加密某个表中包含 SQL Server 对象资源管理器中数据的列，该操作可能会失败。 此功能目前仅在 SSDT 数据库项目和 SSMS 中受支持。 以后的发行版将会实现对 SQL Server 对象资源管理器的支持。


**更新和修复**
* **数据库工具：**
    - **SSDT：**
        - 连接 bug 1898001 [修复了列说明存在的 128 字符限制的问题](https://connect.microsoft.com/SQLServer/feedback/details/1898001/column-description-limited-to-128-characters)。
        - 修复了以下问题：从 VS 发布数据库不会应用发布配置文件 xml 中的 DatabaseServiceObjective 属性。
        - 连接 bug 2900167 [修复了运行单元测试时错误地留下临时文件的问题](http://connect.microsoft.com/SQLServer/feedback/details/2900167/running-ssdt-unit-tests-leaves-temp-files-behind)。
        - 修复了以下问题：“数据库设置”中的“保留期”组合框被截断。
        - 修复了更改密码时，不会验证 SQL CLR 项目属性中的空旧密码的问题。
    - **DACFx：**
        - 修复了以下问题：由于发生 SqlAzureV12 错误，DACFx 兼容级别未更新。
        - 修复了以下问题：从模型比较中错误地排除 IsAutoGeneratedHistoryTable 属性。

- **Analysis Services 和 Reporting Services**
    - **SSDT：**
        - 修复了服务器连接断开时无法保存表格模型的问题。
        - 修复了以下问题：由于 AS 中可能存在无限循环问题，SSDT 无响应。
        - 修复了以下问题：根据 DAX 表达式的提交方式，该表达式会导致不一致的行为。
        - 修复了创建 KPI 时 VS 崩溃的问题。
        - 修复了针对 SQL Server 2008 R2、2012 和 2014 生成无效报告的问题。
        - 修复了以下问题：层次结构顺序导致 .dwpro 项目发生无限循环错误。
        - 修复了一个 RS RDL 问题：降级 RDL 要求完全重新生成，使用户感到迷惑。
        - 修复了一个 KPI 问题：“从客户端工具中隐藏”不起作用。
        

 
  
## <a name="ssdt-july-for-sql-server-2016"></a>SSDT 7 月版（适用于 SQL Server 2016）  
发布日期：2016 年 6 月 30 日  
  
内部版本号：14.0.60629.0  
  
**新增功能**  
* **Always Encrypted 支持：**对于包含 Always Encrypted 列的数据库，此发行版通过我们的核心 API 和命令行工具 (SqlPackage.exe) 添加了对 Always Encrypted 的完全支持。 你可以生成并发布完全支持所有 Always Encrypted 功能的数据库项目。  
* **临时表增强支持：**可以在修改之前取消链接临时表，在完成修改后重新链接临时表，因此简化了体验。 这意味着，在受支持的操作方面，临时表的功能与其他表类型（标准表、内存中表）完全相同。 
* **SqlPackage.exe 和安装更改：**从 SQL Server 引擎中隔离 SSDT 的方式发生更改，SSMS 有了更新。 有关详细信息，请参阅 [Changes to SSDT and SqlPackage.exe installation and updates](https://blogs.msdn.microsoft.com/ssdt/2016/06/30/changes-to-ssdt-and-sqlpackage-exe-installation-and-updates/)（SSDT 和 SqlPackage.exe 安装与更新的更改）。

 

**更新和修复**
* **数据库工具：**
    * 从现在起，SSDT 永远不会在数据库中禁用透明数据加密 (TDE)。 以前，由于项目数据库设置中的默认加密选项已禁用，因此会关闭加密。 使用此修复程序可以启用加密，但发布期间永远不会禁用加密。 
    * 增大了初始连接期间的重试计数和 Azure SQL DB 连接的复原能力。
    * 如果默认文件组不是 PRIMARY，导入/发布到 Azure V12 将会失败。 现在，在发布时将忽略此设置。
    * 修复了以下问题：导出包含带引号标识符对象的数据库时，在某些情况下导出验证可能会失败。
    * 修复了以下问题：创建 Hekaton 表时错误地添加 TEXTIMAGE_ON 选项，这是不允许的。
    * 修复了以下问题：导出大量数据时，导出需要花费很长时间，原因是数据阶段完成后写入 model.xml 文件导致重写 .bacpac 文件的内容。
    * 修复了以下问题：用户未显示在 Azure SQL 数据仓库和 APS 连接的“安全”文件夹中。


 * **Analysis Services 和 Reporting Services：**
    * 修复了 MSOLAP OLEDB 提供程序的一个 SxS 问题：只安装 32 位提供程序，从而影响 64 位 Excel 2016 连接到 SQL Server 2014（在 Office365 中执行 ClickOnce 安装不会出现此问题，只有执行 MSI Excel 安装时才出现）。
    * 修复了相关问题，使以下极端情况变得更可靠：将包含粘贴表的 AS 模型从 1103 升级到 1200 兼容级别时，可能出现错误“关系使用无效的列 ID”。
    * 修复了一个 SxS 问题：卸载 SSDT 2015（装入共享注册表设置）后，同一台计算机上的 SSDT BI 2013 不再能够导入 AS 模型中的数据。
    * 改进了可靠性，解决了当与 AS 引擎的连接断开（例如，SSDT 保持打开一整夜、AS 服务器被回收，或者暂时断开连接的其他情况）时发生的问题/崩溃。 
    * 修复了在多监视器方案中，对话框在非 VS 的屏幕上打开的问题。 
    * 已修复/已启用从 AS 模型粘贴表中的 HTML 表（网格数据）粘贴的支持。 
    * 修复了无法将空白粘贴表升级到 1200（只用作用于度量的容器表）的问题。 
    * 修复了有关以下操作的问题：将包含粘贴表的 AS 表格模型升级到 1200 来解决 CalcTables（用于 1200 中的粘贴表）的 AS 引擎问题，以便在升级后针对新的计算表执行完整过程。 
    * 修复了以下问题：取消创建包含不完整 DAX 表达式的新 AS 1200 模型计算表可能会崩溃。 
    * 修复了当数据库名称与表名称相同时，将 1200 模型从服务器导入 SSDT AS 项目时出现的问题。 
    * 修复了在 1103 表格模型中编辑 KPI 度量值时出现的问题。 
    * 修复了在网格中为 AS 1200 模型粘贴 KPI 度量值时，对象引用未设置异常命中的问题。 
    * 修复了以下问题：无法从 1200 模型的图示视图中删除计算表中的列。 
    * 修复了在代码视图中查看 model.bim 项目文件属性时，对象引用未设置异常命中的问题。 
    * 修复了以下问题：在使用逗号作为小数分隔符的国际区域设置中，将数据粘贴到 AS 模型网格以创建粘贴表时，会生成错误的值。 
    * 修复了在 SSDT 中打开 2008 RS 项目并选择不升级该项目时出现的问题。 
    * 修复了为列类型使用默认格式，以便能够从 UI 更改格式类型时，1200 兼容级别模型计算表中存在的问题。 
    

## <a name="ssdt-june-for-sql-server-2016"></a>SSDT 6 月版（适用于 SQL Server 2016）  
发布日期：2016 年 6 月 1 日  
  
内部版本号：14.0.60525.0 

SSDT 正式版 (GA) 现已发布。 2016 年 6 月 SSDT GA 更新添加了对 SQL Server 2016 RTM 最新更新的支持，并修复了多个 bug。 有关详细信息，请参阅 [SQL Server Data Tools GA update for June 2016](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/)（SQL Server Data Tools GA 2016 年 6 月更新）。

      

## <a name="ssdt-april-for-sql-server-2016-rc3"></a>SSDT 4 月版（适用于 SQL Server 2016 RC3）  
发布日期：2016 年 4 月 15日  
  
内部版本号：14.0.60413.0  
  
**SQL Server 数据库**  
* **Always Encrypted 支持：**对于包含 Always Encrypted 列的数据库，SSDT 和 DacFx 允许查看和编辑这些数据库，以及从数据库项目发布到这些数据库。 请注意，将来的发行版会支持更改已启用列加密的列。  
* **连接对话框和 SQL Server 对象资源管理器：**多项修复和改进。  
    * 列出高级连接属性的“详细信息”页经过全新设计，可在多行框中显示完整的连接字符串，以及改进对 DPI 计算机的支持。  
    * 我们重新引入了包含详细连接错误信息的传统错误对话框。 此对话框提供更明确的错误消息和堆栈跟踪，可帮助诊断登录问题，使 DBA 或 CSS 能够获得所需的信息来诊断问题。  
    * 针对拥有最低权限的用户，我们修复了有关在连接对话框中和 SQL Server 对象资源管理器中列出数据库、查看“安全”文件夹等方面的多个问题。  
    * 展开数据库节点以列出所有数据库时，Azure SQL 数据库的性能得到了改进。  
* **SSDT 安装程序：**  
    * 修复了卸载时下载 .Net 的问题。  
    * 在高 DPI 计算机上，现在会正确设置安装程序大小。  
    * 取消版本检查。存在更新的 SQL Server 版本时，版本检查会阻止安装 SSDT。  
    * 架构比较：修复了以下性能问题：在 Visual Studio 中选中/取消选中多个项需要很长时间。  
    * 支持在 x86 计算机上使用 LocalDB 2014，因为 SQL Server 2016 没有 x86 版本。  
* **生成和部署：**  
    * 修复了临时表不支持计算列的问题。  
    * 部署到 Azure V12 时，将忽略“在单用户模式下执行部署脚本”选项，因为云方案不支持此选项。  
  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc2"></a>SSDT 修补程序（适用于 SQL Server 2016 RC2）  
发布日期：2016 年 4 月 5日  
  
内部版本号：14.0.60329.0  
  
此内部版本包含提供 SQL Server Integration Services 功能的 SSDT 版本的修补程序。 也可以针对 SQL Server 2016 中的 Analysis Services 和 Reporting Services 使用内部版本 14.0.60316.0。   
  
若要获取此修补程序，请使用[此博客文章中的下载链接](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/)。  
  
报告开发人员使用此版 SSDT 生成新报告时，请[阅读已知问题和解决方法](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/)，了解只会在此修补程序中出现的 SSRS 报告中的暂时性问题。  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc0"></a>SSDT 修补程序（适用于 SQL Server 2016 RC0）  
发布日期：2016 年 3 月 18 日  
  
内部版本号：14.0.60316.0  
  
此内部版本包含提供 SQL Server 2016 RC0 功能的 SSDT 版本的修补程序。 目前不提供 RC1 版本的 SSDT。 可以针对 RC0 或 RC1 版本的 SQL Server 2016 使用内部版本 14.0.60316.0。  
      
## <a name="ssdt-february-2016-preview-for-sql-server-2016-rc0"></a>SSDT 2016 年 2 月预览版（适用于 SQL Server 2016 RC0）  
发布日期：2016 年 3 月 7 日  
  
内部版本号：14.0.60305.0  
  
-   **SQL Server 项目模板**  
  
    没有此 SSDT 预览版本的通知。 请参阅[数据库引擎中的新增功能](https://msdn.microsoft.com/library/bb510411.aspx)了解有关此发行版中的其他功能。  
  
-   **SSIS 包项目模板**  
  
    SSIS 设计器为 SQL Server 2016、2014 或 2012 创建和维护包。 重命名为部件的新模板。 SSIS Hadoop 连接器支持 ORC 格式。 请参阅 [Integration Services 中的新增功能](https://msdn.microsoft.com/library/bb522534.aspx)了解详细信息。  
  
-   **SSAS 项目模板（表格模型项目）**  
  
    本月 Analysis Services 的更新提供对表格模型和创建的任何模型的显示文件夹，SSIS 包现在支持新的 SQL Server 2016 兼容级别。 有关详细信息， 请参阅 [Analysis Services 中的新增功能（博客文章](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx)。  
  
-   **SSRS 报告项目模板**  
  
    没有此 SSDT 预览版本的通知。 请参阅 [Reporting Services 中的新增功能](https://msdn.microsoft.com/library/ms170438.aspx)了解有关此发行版中的其他功能。  
  
## <a name="ssdt-january-2016-preview"></a>SSMS 2016 年 1 月预览版  
发布日期：2016 年 2 月 4 日  
  
内部版本号：14.0.60203.0  
  
-   **SQL Server 项目模板**  
  
    没有此 SSDT 预览版本的通知。 请参阅[数据库引擎中的新增功能](https://msdn.microsoft.com/library/bb510411.aspx)了解有关此 CTP 中的其他功能。  
  
-   **SSIS 包项目模板**  
  
    添加了对 ODBC 源和目标组件、CDC 控制任务、  
      CDC 源和拆分器组件、Microsoft Connector for SAP BW 和用于 Azure 的 Integration Services 功能包的支持。 请参阅 [Integration Services 中的新增功能](https://msdn.microsoft.com/library/bb522534.aspx)了解详细信息。  
  
-   **SSAS 项目模板**  
  
    包括改进 1200 兼容性级别的表格模型、DirectQuery 模式下模型的计算列和行级别的安全性、模型元数据的翻译、SSIS Analysis Services 执行 DDL 任务中的 TMSL 脚本执行并修复了多处 Bug。  
    请参阅 [Analysis Services 中的新增功能 (msdn)](https://msdn.microsoft.com/library/bb522628.aspx) 或 [Analysis Services 中的新增功能（博客文章）](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx)了解详细信息。  
  
-   **SSRS 报告项目模板**  
  
    没有此 SSDT 预览版本的通知。 请参阅 [Reporting Services 中的新增功能](https://msdn.microsoft.com/library/ms170438.aspx)了解有关此 CTP 中的其他功能。  
  
## <a name="ssdt-december-2015-preview"></a>SSDT 2015 年 12 月预览版  
  
-   **SQL Server 项目模板**包括针对“连接”对话框、最近的历史列表，以及在加载数据库列表时正确使用连接属性中设置的身份验证上下文的 Bug 修补程序。  
  
    -   将测试连接超时值更改为 15 秒。  
  
    -   如果在加载数据库列表时未注册客户端 IP，则创建 Azure SQL 数据库服务器防火墙规则。  
  
    -   SQL Server 2016 CTP3.2 功能可编程性支持。  
  
-   **SSAS 项目模板**添加了对基于 DAX 表达式和模型中已定义的其他对象创建计算表的支持。  
  
-   **SSIS 包项目模板**附加件包括 Avro 文件格式和 Kerberos 身份验证的 SSIS Hadoop 连接器支持。   
    请注意，此更新中尚未包含 SSIS 设计器对 SSIS 2012 和 2014 的支持。  
  
## <a name="ssdt-november-2015-preview"></a>SSDT 2015 年 11 月预览版  
  
-   **SQL Server 项目模板**。 SQL Server 和 Azure SQL 数据库改进的连接体验预览。  
  
-   **SSIS 包项目模板**。 SSIS 目录性能改进：针对非 SSIS 管理员用户的大多数 SSIS 目录视图的性能都得到了改进。  
  
-   **SSAS 项目模板**包括对 Analysis Services 中表格模型项目的增强功能。 可以使用“查看代码”命令查看 JSON 中的模型定义。**** 如果你现在使用的不是完整功能版的 Visual Studio 2015，那么你将需要这个版本来获得 JSON 编辑器。 可以免费下载 [Visual Studio Community Edition](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)。  
  
## <a name="ssdt-october-2015-preview"></a>SSDT 2015 年 10 月预览版  
  
-   用于 BI 的新项目模板（Analysis Services 模型、Reporting Services 报表和 Integration Services 包）。 所有 SQL Server 项目模板现在都位于一个 SSDT 中。  
  
-   新的 SSIS 功能，包括 Hadoop 连接器、控制流模板，以及放宽的数据流任务最大缓冲区大小。  
  
-   对关系数据库项目的 SQL Server 2016 CTP 3.0 功能支持。  
  
-   SSIS 中的各种 Bug 修补程序以及对 Windows 7 OS 的支持。  
  
## <a name="ssdt-september-2015-preview"></a>SSDT 2015 年 9 月预览版  
  
-   此预览版中新增了多语言支持。  
  
## <a name="ssdt-august-2015-preview"></a>SSDT 2015 年 8 月预览版  
  
-   用于安装 SSDT 的新的独立 Setup.exe 程序。  你不再需要使用 SQL Server 安装程序的修改版本。 此 SSDT 版本包括用于生成部署到 SQL Server 或 Azure SQL 数据库的关系数据库的项目模板。  
  
## <a name="see-also"></a>另请参阅  
[下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  
[以前版本的 SQL Server Data Tools（SSDT 和 SSDT-BI）](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)  
[数据库引擎中的新增功能](https://msdn.microsoft.com/library/bb510411.aspx)  
[Analysis Services 中的新增功能](https://msdn.microsoft.com/library/bb522628.aspx)  
[Integration Services 中的新增功能](https://msdn.microsoft.com/library/bb522534.aspx)  
  

