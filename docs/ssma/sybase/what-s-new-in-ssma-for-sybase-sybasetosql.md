---
title: SAP ASE SSMA 的新增功能 （SybaseToSQL） |微软文档
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
ms.author: jtoland;alexiva
ms.openlocfilehash: 7f23c7e1c676b4ade42b43cf963e0fa6956f93c6
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625587"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>SAP ASE SSMA 中的新增功能（SybaseToSQL）

本文列出了每个版本中 SAP ASE（以前 SSMA 表示 Sybase）更改的 SQL 服务器迁移助理 （SSMA）。

## <a name="ssma-v88"></a>SSMA v8.8

面向 SAP ASE 的 SSMA v8.8 版本包括：

* SQL Server 对象同步稳定性改进
* 评估和转换期间的 GUI 性能改进
* 修复了对象 SQL 定义中缺少字符的问题

## <a name="ssma-v87"></a>SSMA v8.7

用于 SAP ASE 的 SSMA v8.7 版本在图形用户界面中具有轻微的修复和性能改进。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v86"></a>SSMA v8.6

除了一组旨在提高可用性和性能的有针对性的修补程序外，SAP ASE 的 SSMA v8.6 版本通过添加允许用户在转换后的代码中省略 SSMA 扩展属性的设置进行了增强。

要利用此设置，在 SAP ASE 的 SSMA 中，导航到**工具** > **项目设置** > **常规** > **转换**，然后在**Misc**下，将 **"省略扩展属性**"设置的值更新为 **"是**"。

![省略扩展属性设置](../sybase/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v85"></a>SSMA v8.5

支持 Azure Active Directory 身份验证和 SQL 服务器中对 JSON 功能的基本支持，以及一组旨在提高可用性和性能的有针对性的修补程序，增强了用于 SAP ASE 的 SSMA 的 v8.5 版本。

此外，SAP ASE 的 SSMA 现在允许您隐藏系统表和视图（将其排除在转换之外）。

> [!IMPORTANT]
> 使用 SSMA v8.5 时，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v84"></a>SSMA v8.4

针对 SAP ASE 的 SSMA v8.4 版本通过有针对性的修补程序进行增强，这些修补程序旨在解决辅助功能问题并修复 SQL Server 2016 和更高版本的最大索引列（允许 32 而不是 16）相关的 Bug。

> [!IMPORTANT]
> 对于 SSMA 版本 7.4 到 8.4，.NET 4.5.2 是安装的先决条件。

## <a name="ssma-v83"></a>SSMA v8.3

面向 SAP ASE 的 SSMA v8.3 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。 此外，此版本的 SAP ASE SSMA 提供了以下修补程序：

* 解决辅助功能问题
* 添加对`hierarchyid`SQL Server 类型的基本支持

## <a name="ssma-v82"></a>SSMA v8.2

用于 SAP ASE 的 SSMA v8.2 版本通过一组旨在提高质量和转换指标的有针对性的修补程序以及用于以下的修补程序进行增强：

* 数据迁移后禁用的非群集索引的问题。
* 在静默安装期间检测 .NET 框架。
* 下载新版本时发生的间歇性崩溃。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.1 到 v8.2 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v81"></a>SSMA v8.1

面向 SAP ASE 的 SSMA v8.1 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.0 到 v8.1 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v80"></a>SSMA v8.0

针对 SAP ASE 的 SSMA v8.0 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。 此外，此版本还提供以下新功能：

* 支持**Azure SQL 数据库托管实例**作为目标。 现在，您可以创建针对 Azure SQL 数据库托管实例的新项目：

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

* 转换后**修复顾问**。 在此处了解有关它的更多[。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步数据库/架构选择。

  连接到源时，用户现在可以选择感兴趣的数据库/架构。 仅选择计划迁移的架构将节省时间连接期间的时间，并提高 SSMA 的整体性能。

  ![SSMA 筛选对象](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

针对 SAP ASE 的 SSMA v7.10 版本通过有针对性的修补程序进行了增强，旨在提供额外的安全和隐私保护，以满足全球需求的变化。

## <a name="ssma-v79"></a>SSMA v7.9

用于 SAP ASE 的 SSMA v7.9 版本包含以下更改：

* 提高质量和转化指标的针对性修复。
* 支持 SSMA 命令行以更改数据类型映射和项目首选项。
* 支持使用 SQL 服务器集成服务 （SSIS） 迁移数据。 转换架构后，可以使用右键单击上下文菜单选项创建 SSIS 包。
* SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在 SSMA 的早期版本中，必须在项目设置中显式提及 Azure SQL 数据库前缀。

## <a name="ssma-v78"></a>SSMA v7.8

用于 SAP ASE 的 SSMA v7.8 版本包含以下更改：

* 更改类型映射在**项目设置**中突出显示。
* 用户禁用遥测功能。

## <a name="ssma-v77"></a>SSMA v7.7

用于 SAP ASE 的 SSMA v7.7 版本包含以下更改：

* SAP ASE 的 SSMA 已通过提高质量和转化指标的有针对性的修补程序进行了增强。
* 根据大众需求，SAP ASE 的 32 位版本的 SSMA 又回来了。 与以前的实现（在 v7.4 之前）相比，有两个安装程序包，但不能并排安装。 因此，您必须根据拥有的连接组件选择最合适的版本。 如果可能，最好使用 64 位版本。

## <a name="ssma-v76"></a>SSMA v7.6

用于 SAP ASE 的 SSMA v7.6 版本包含以下更改：

* 提高质量和转换指标并支持 SQL Server 2017（公共预览）的针对性修补程序。 Windows 和 Linux 上对 SQL Server 2017 的支持处于公共预览版，不应用于生产迁移。
* 支持转换 Sybase 函数。

## <a name="ssma-v75"></a>SSMA v7.5

用于 SAP ASE 的 SSMA v7.5 版本（以前适用于 Sybase 的 SSMA）包含以下更改：

* 若干改进，以确保残疾人更容易获得无障碍环境。
* 支持`CREATE OR REPLACE`语法。

## <a name="ssma-v74"></a>SSMA v7.4

Sybase 的 SSMA v7.4 版本包含以下更改：

* **查询超时**选项现在在源和目标架构对象发现期间可用。

  ![查询超时选项](../media/query-timeout_red.png)
* 质量和转化指标已根据客户反馈通过有针对性的修复得到了改进。

  > [!IMPORTANT]
  > .NET 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停产。

## <a name="ssma-v73"></a>SSMA v7.3

Sybase 的 SSMA v7.3 版本包含以下更改：

* 根据客户反馈有针对性地修复，提高质量和转化指标。
* 通过以下项目公开的 SSMA 可扩展性框架：
  * 将功能导出到 SQL 服务器数据工具 （SSDT） 项目。
    * 现在，您可以将架构脚本从 SSMA 导出到 SSDT 项目。 您可以使用架构脚本进行其他架构更改并部署数据库。

        ![另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  * SSMA 可使用用于执行自定义转换的库。
    * 现在，您可以构造可以处理 SSMA 以前未处理的自定义语法转换和转换的代码。
      * 有关如何构造自定义转换器的说明，可在此博客文章，[扩展 SQL 服务器迁移助手的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 从这个[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)下载一个转换的示例项目。

## <a name="ssma-v72"></a>SSMA v7.2

Sybase 的 SSMA v7.2 版本包含以下更改：

* 根据客户反馈有针对性地修复，提高质量和转化指标。
* 遥测增强功能，以提供更好的数据点，以解决客户问题并提高 SSMA 的转化率。

## <a name="ssma-v71"></a>SSMA v7.1

Sybase 的 SSMA v7.1 版本包含以下更改：

* Windows 和 Linux CTP1 上的 SQL Server 2017 现在是支持迁移的目标平台。 此功能处于技术预览中，支持针对 SQL 服务器的架构和数据移动。
* 支持自动更新，以便一旦 SSMA 可用，立即下载。
* SSMA 可安装二进制文件现在通过 Windows 安装程序包文件 （.msi） 传递。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 SSMA 适用于 Sybase 包含以下更改：

* 添加了对 SQL Server 2016 的支持。
* 已删除的安装程序检查 .NET 2.0。
* 将扩展包依赖项从 .NET 3.5 更新为 .NET 4.0。
* SSMA 控制台的固定`save-project`和`open-project`命令。
* SSMA 控制台的固定`securepassword`命令。
* 修复了初始加载的对象计数。
* 修复了全局设置中的 Bug。

## <a name="march-2016"></a>2016 年 3 月

Sybase 的 SSMA 预览版 2016 年 3 月增加了对迁移到 SQL Server 2016 的支持。

## <a name="january-2016"></a>2016 年 1 月

Sybase 的 SSMA 2016 年 1 月维护版本包含以下更改：

* 将视图日志菜单项添加到 SSMA （RFC 5706203）。
* 添加了遥测。

## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版本的 SSMA 适用于 Sybase 包含以下更改：

* 改进了 Azure SQL DB 代码转换。
* 将扩展包功能移动到架构以支持 Azure SQL DB。
* 为具有 10k 个以上对象的数据库测试的性能改进。
* 添加了用于处理大量对象的 UI 改进。
* 添加了突出显示已知 LOB 架构（以便在转换中忽略它们）的能力。
* 添加了转换速度改进。
* 添加了在 UI 中显示对象计数的能力。
* 报表大小减少 25% 以上。
* 改进了未解析构造的错误消息。

## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版本的 SSMA 适用于 Sybase 包含以下更改：

* 添加了对 MS SQL Server 2014 的支持。
* 修复了有关转换为 Azure 的错误。
* 修复了 IE 10 中不可见报表页的 Bug。

## <a name="january-2012"></a>2012 年 1 月

Sybase 的 SSMA 2012 年 1 月版本包含以下更改：

* 添加了对回滚触发器转换的支持。
* 提供了用于转换`@@ROWCOUNT`和`@@ERROR`在同一`SET`语句中的修复程序。

## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版 SSMA 用于 Sybase 提供了数据迁移期间改进的错误报告。

## <a name="april-2011"></a>2011 年 4 月

2011 年 4 月版本的 SSMA 适用于 Sybase 包含以下更改：

* 整合的"SSMA 用于 Sybase"产品[!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)]，[!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]支持[!INCLUDE [ssSQL11](../../includes/ssSQL11-md.md)]和 Azure SQL。
* 添加了对连接和迁移到[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]的支持。
* 添加了一个新功能，用于将 Sybase 数据库转换为 Azure SQL。
* 增强的客户端数据迁移引擎，支持数据的并行迁移。
* 使用简单和批量记录恢复模型提高了数据迁移性能。
* 添加了将区分大小写 Sybase 数据库正确转换为区分大小写的 SQL Server 的功能。
* 对 Sybase ASE 非 ANSI 联接语句转换为 SQL Server ANSI 联接语句的附加支持已扩展到 DELETE 和更新语句。
* 提供了其他连接选项，用于使用 Sybase ASE ODBC 提供程序和 Sybase ASE ADO.NET提供程序连接到 Sybase ASE 服务器。
* 删除了对称为 的`SysDB`单独数据库的依赖项，该数据库包含 Sybase 仿真函数（作为扩展包的一部分安装）。
* 添加了在群集上安装[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]Sybase 扩展包 SSMA 的能力。
* 添加了早期版本的 SSMA（v4.0 和 v4.2）创建的项目的向后兼容性。
* 添加了使用旧版本的 SSMA（v4.0 和 v4.2）并行安装 Sybase v5.0 产品的 SSMA 功能。

## <a name="july-2010"></a>2010 年 7 月

Sybase 的 SSMA 2010 年 7 月版本新增：

* 支持迁移到 SQL Server 2008 R2。
* 用于命令行执行的新 SSMA 控制台应用程序。
* 使用服务器端和客户端数据迁移引擎支持数据迁移。
* 在数据迁移中支持"自定义 SELECT"语句。
* 支持从 Sybase ASE 15.0.3 和 15.5 迁移。

## <a name="june-2008"></a>2008 年 6 月

Sybase 的 SSMA 2008 年 6 月版本包含以下更改：

* 添加了 SSMA 测试程序，它自动测试数据库对象转换和 SSMA 进行的数据迁移。 完成所有 SSMA 迁移步骤后，使用 SSMA 测试程序验证转换的对象是否以相同的方式工作，以及所有数据是否正确传输。
* 添加了 SQL 前转换。 用户现在可以为要在转换中使用的每个源过程指定临时表（和其他对象）声明。
* 在对象转换方面增加了改进：
  * 加入已修订的转化。
  * 聚合和非聚合，没有/按子句分组。
  * 具有`IDENTITY`语句的`SELECT INTO`函数。
  * 仅数据锁定的群集约束和索引。
  * 由 创建`SELECT INTO`的临时表。
  * 临时表的约束/索引。
  * 支持[!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]新的约会时间类型。
  * Sybase 15.0 连接和数据类型支持。

## <a name="may-2007"></a>2007 年 5 月

2007 年 5 月 SSMA 版本的 Sybase 补充说：

* 保存项目时更快地加载数据库内容的能力。
* 支持 SQL Server 格式化的 SQL 模式下用户输入的注释。
* 对象转换的改进。

## <a name="november-2006"></a>2006年11月

Sybase 的 SSMA 2006 年 11 月版本包含以下更改：

* 添加了新的全局设置：
  * 您可以选择在编辑器窗口中显示行号。
  * 您可以将 SSMA 配置为提示替换重复的对象，或者始终或从不在架构转换期间替换重复的对象。
* 添加了一个新的转换选项，允许您配置 SSMA 处理以下情况的方式：
  * 包含`CAST`二`CONVERT`进制字符串的 或 语句。
  * 检查相等表达式中的空值。
  * 代理表。
  * 用户消息错误编号`RAISERROR`。
  * `UPDATE`包含未解析标识符的语句。
* 添加了一个新的迁移选项，用于指定 SSMA 如何处理超出[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]日期范围的日期。
* 在**SQL**选项卡上添加了格式化的**SQL**设置，该设置为代码设置格式以提高可读性。
* 错误修复，包括：
  * SSMA 现在通过`LOCK TABLE <table> IN { SHARED | EXCLUSIVE } MODE`向表上的后续`TABLOCK``SELECT`查询`TABLOCKX`添加 或提示来转换语句。
  * 现在，当字符表达式中使用二进制类型时，将添加必要的强制转换。
  * 内存和性能改进。

## <a name="july-2006"></a>2006年7月

2006 年 7 月发布的用于 Sybase 的 SSMA 是初次发布。

## <a name="see-also"></a>请参阅

[开始使用 SSMA 进行 Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
