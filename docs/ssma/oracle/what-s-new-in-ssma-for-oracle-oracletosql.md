---
title: 甲骨文（OracleToSQL）SSMA的新增功能 |微软文档
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: jtoland;alexiva
ms.openlocfilehash: 88b87aad931f28637accc95aa4d993037fcf0b0a
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625601"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Oracle SSMA 中的新增功能 （OracleToSQL）

本文列出了每个版本中 Oracle 更改的 SQL 服务器迁移助手 （SSMA）。

## <a name="ssma-v88"></a>SSMA v8.8

Oracle SSMA 的 v8.8 版本包括：

* SQL Server 对象同步稳定性改进
* 评估和转换期间的 GUI 性能改进
* 改进分析`OVER PARTITION`条款的转换
* 分析函数`LEAD`的新转换
* 子查询保理子句的新转换
* Azure `REPLICATE` SQL 数据仓库的新分发选项
* 全新 Oracle 语法解析器，进一步提高转换性能

## <a name="ssma-v87"></a>SSMA v8.7

Oracle 的 SSMA v8.7 版本在图形用户界面中具有轻微的修复和性能改进。

此外，Oracle 的 SSMA 现在允许在"高级对象选择"对话框中根据有效性状态筛选对象。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v86"></a>SSMA v8.6

除了一组旨在提高可用性和性能的有针对性的修补程序外，Oracle 的 V8.6 版本还通过添加允许用户在转换后的代码中省略 SSMA 扩展属性的设置进行了增强。

要利用此设置，在 Oracle 的 SSMA 中，导航到**工具** > **项目设置** > **常规** > **转换**，然后在**Misc**下，将 **"Omit 扩展属性**"设置的值更新为 **"是**"。

![省略扩展属性设置](../oracle/media/ssma-omit-extended-properties.png)

此外，Oracle 的 SSMA 现在提供了对`XMLTABLE`子句的改进解析。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v85"></a>SSMA v8.5

支持 Azure Active Directory 身份验证和对 SQL 服务器中的 JSON 功能的基本支持，以及一组旨在提高可用性和性能的有针对性的修补程序，增强了 Oracle SSMA 的 v8.5 版本。

此外，Oracle 的 SSMA 得到了增强，支持：

* 将用于发现选择的对象数限制为 990（Oracle 子`WHERE .. IN (..)`句限制为 1000 项）。
* 从`RAW`到`UNIQUEIDENTIFIER`的数据迁移。
* 解析`PARALLEL_ENABLE`子句。

最后，Oracle 的 SSMA v8.5 版本现在提供了：

* 改进转换的打包常量的性能。
* .NET 的 Oracle 数据提供程序更新到版本 19.5.0。

> [!IMPORTANT]
> 使用 SSMA v8.5 时，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v84"></a>SSMA v8.4

Oracle 的 SSMA v8.4 版本通过有针对性的修补程序进行增强，这些修补程序旨在解决辅助功能问题并修复 SQL Server 2016 和更高版本的最大索引列（允许 32 而不是 16）相关的 Bug。

此外，此版本的 Oracle SSMA 增加了作为存储`SYS_REFCURSOR`过程`OUT`参数的转换。

> [!IMPORTANT]
> 对于 SSMA 版本 7.4 到 8.4，.NET 4.5.2 是安装的先决条件。

## <a name="ssma-v83"></a>SSMA v8.3

Oracle 的 SSMA v8.3 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。 此外，此版本的 Oracle SSMA 提供了以下修补程序：

* 解决辅助功能问题。
* 添加对`hierarchyid`SQL Server 类型的基本支持。
* 解决通过同义词调用的函数的未知返回类型的问题。
* 将ODP.NET更新为 v19.3。

## <a name="ssma-v82"></a>SSMA v8.2

Oracle 的 SSMA v8.2 版本已增强为：

* 添加 对`DBMS_OUTPUT.ENABLE`/`DISABLE`的支持。
* 删除`CAST AS FLOAT``BINARY_FLOAT`默认`BINARY_DOUBLE`数据迁移查询中的 和 列。
* 如果当前值已更改，修复序列将刷新。
* 如果存在同名列，则修复与误解伪列`ROWNUM`（等） 相关的 Bug。
* 修复发生转换具有不明确未解析`FOR`标识符的循环的崩溃。

此外，此版本还包括一组旨在提高质量和转化指标的有针对性的修补程序，以及用于以下的修补程序：

* 数据迁移后禁用的非群集索引的问题。
* 在静默安装期间检测 .NET 框架。
* 下载新版本时发生的间歇性崩溃。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.1 到 v8.2 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v81"></a>SSMA v8.1

Oracle 的 SSMA v8.1 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.0 到 v8.1 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v80"></a>SSMA v8.0

Oracle SSMA 的 v8.0 版本通过旨在提高质量和转换指标的有针对性的修补程序得到增强。 此版本还提供以下新功能：

* 支持**Azure SQL 数据库托管实例**作为目标。 现在，您可以创建针对 Azure SQL 数据库托管实例的新项目：

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > Oracle 扩展包的 SSMA 也进行了更新，以允许在 Azure SQL 数据库托管实例上进行远程安装：
  >
  > ![用于 Oracle 扩展包的 SSMA](../media/ssma-oracle-ext-pack.png)

  定位 Azure SQL 数据库托管实例时，不支持某些功能，包括测试人员和服务器端数据迁移。 在[此处](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)阅读详细信息。

* 转换后**修复顾问**。 在此处了解有关它的更多[。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步数据库/架构选择。

  连接到源时，用户现在可以选择感兴趣的数据库/架构。 仅选择计划迁移的架构将节省时间连接期间的时间，并提高 SSMA 的整体性能。

  ![SSMA 筛选对象](../media/ssma-filter-objects.png)

* 能够使用官方管理的 .NET 驱动程序连接到 Oracle。 OCI 驱动程序不再是使用 Oracle SQL 服务器迁移助手的先决条件。

* 默认情况下，可以映射`ROWID`和`UROWID`映射到`VARCHAR`。 更改了`uniqueidentifier`，以适应显式`ROWID`列的数据迁移。

## <a name="ssma-v710"></a>SSMA v7.10

Oracle 的 SSMA v7.10 版本包含以下更改：

* 旨在提供额外安全和隐私保护以满足全球需求变化的有针对性的修补程序。
* 与分层查询相关的转换改进。

## <a name="ssma-v79"></a>SSMA v7.9

Oracle 的 SSMA v7.9 版本包含以下更改：

* 提高质量和转化指标的针对性修复。
* 支持将"继续"语句从 Oracle 迁移到 SQL 服务器。
* 支持 SSMA 命令行以更改数据类型映射和项目首选项。
* 支持使用 SQL 服务器集成服务 （SSIS） 迁移数据。 转换架构后，可以使用右键单击上下文菜单选项创建 SSIS 包。
* SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在 SSMA 的早期版本中，必须在项目设置中显式提及 Azure SQL 数据库前缀。

## <a name="ssma-v78"></a>SSMA v7.8

Oracle 的 SSMA v7.8 版本包含以下更改：

* 支持：
  * 子句的`IN`行表达式。
  * 隐式类型强制转换。
  * `UID`Azure SQL 数据库的转换。
* 更改类型映射在**项目设置**中突出显示。
* 用户禁用遥测功能。

## <a name="ssma-v77"></a>SSMA v7.7

Oracle 的 SSMA v7.7 版本包含以下更改：

* Oracle 的 SSMA 已通过提高质量和转化指标的针对性修补程序进行了增强。
* 根据大众需求，甲骨文的32位版SSMA又回来了。 与以前的实现（在 v7.4 之前）相比，有两个安装程序包，但不能并排安装。 因此，您必须根据拥有的连接组件选择最合适的版本。 如果可能，最好使用 64 位版本。
* SQL Server 2017 支持现在正式，在 Linux 上支持 Oracle 扩展包（新的远程安装选项）。 请注意，在 Linux 上安装扩展包功能受到限制，因为不支持测试人员和服务器端数据迁移功能。
* Oracle 的 SSMA 允许您将具体化视图迁移到常规表（可通过**项目设置** -> **同步** -> 中的设置配置**发现具体视图的备份表**）。

## <a name="ssma-v76"></a>SSMA v7.6

Oracle SSMA 的 v7.6 版本通过提高质量和转换指标的针对性修补程序以及支持 SQL Server 2017（公共预览）来增强。 Windows 和 Linux 上对 SQL Server 2017 的支持处于公共预览版，不应用于生产迁移。

## <a name="ssma-v75"></a>SSMA v7.5

Oracle 的 SSMA v7.5 版本包含以下更改：

* 通过多项改进进行改进，确保残疾人获得更多无障碍环境。
* 通过有针对性的修复改进质量和转换指标，例如根据客户反馈改进数据迁移期间的日期和浮动数据类型的处理。

## <a name="ssma-v74"></a>SSMA v7.4

Oracle 的 SSMA v7.4 版本包含以下更改：

* Oracle 的 SSMA 现在支持 Azure SQL 数据仓库作为迁移的目标平台。

  ![“新建项目”窗口](../media/new-project.png)
  * 支持数据仓库存储选项，如下图所示：

  ![数据仓库的存储选项](../media/storage-options_red.png)
  * 支持如下图像所示的数据分发选项：

  ![数据仓库的数据分发](../media/data-distribution_red.png)

* **查询超时**选项现在在源和目标架构对象发现期间可用。

  ![查询超时选项](../media/query-timeout_red.png)

* 质量和转化指标已根据客户反馈通过有针对性的修复得到了改进。

> [!IMPORTANT]
> .NET 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停产。

## <a name="ssma-v73"></a>SSMA v7.3

Oracle 的 SSMA v7.3 版本包含以下更改：

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

Oracle 的 SSMA v7.2 版本包含以下更改：

* 根据客户反馈有针对性地修复，提高质量和转化指标。
* 遥测增强功能，以提供更好的数据点，以解决客户问题并提高 SSMA 的转化率。

## <a name="ssma-v71"></a>SSMA v7.1

Oracle 的 SSMA v7.1 版本包含以下更改：

* Windows 和 Linux CTP1 上的 SQL Server 2017 现在是支持迁移的目标平台。 此功能处于技术预览中，允许架构和数据移动以目标 SQL 服务器为目标。
* SSMA 现在支持自动更新，以便一旦 SSMA 可用，立即下载。
* SSMA 可安装二进制文件现在通过 Windows 安装程序包文件 （.msi） 传递。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 Oracle SSMA 包含以下更改：

* 添加了对 SQL Server 2016 的支持。
* 将 Oracle 闪回存档表转换为 SQL Server 临时表。

  > [!NOTE]
  > SSMA 不会从 Oracle 闪存数据存档表复制历史数据。 因此，必须在迁移过程中手动复制历史记录数据。 此外，虽然 SSMA 不会在 SQL Server 元数据资源管理器中显示历史记录表，因为它被视为系统表，但您可以在 SQL Server 管理工作室中查看历史记录表。
  >
  > SQL Server 2016 不支持多个 Oracle 闪回功能，包括：
  >
  >   * 甲骨文闪回事务查询
  >   * `DBMS_FLASHBACK`包
  >   * 闪回事务
  >   * 闪回数据存档
  >   * 闪回表
  >   * 闪回丢弃
  >   * 闪回数据库

* 将 Oracle VPD 策略转换为 SQL 服务器策略对象（Oracle 的行级安全性）。
* 减少了 Oracle 的初始加载时间。
* 改进的解析器和解析器。
* 已删除的安装程序检查 .NET 2.0。
* 将扩展包依赖项从 .NET 3.5 更新为 .NET 4.0。
* SSMA 控制台的固定`save-project`和`open-project`命令。
* SSMA 控制台的固定`securepassword`命令。
* 修复了初始加载的对象计数。
* 修复了 Oracle 字符数据类型的转换。
* 修复了全局设置中的 Bug。

## <a name="march-2016"></a>2016 年 3 月

2016 年 3 月为 Oracle 发布的 SSMA 预览版增加了对以下支持：

* 迁移到 SQL Server 2016。
* 迁移 Oracle 行级别安全性（具有一些限制）。
* 将内存表中的 Oracle 迁移到 SQL 服务器列存储。

## <a name="january-2016"></a>2016 年 1 月

2014 年 1 月适用于 Oracle 的 SSMA 维护版本包含以下更改：

* 添加了对群集索引的支持。
* 修复了慢速 Oracle 架构查询 （RFC 5076207）。
* 修复了从控制台连接到 Azure 的连接。
* 将视图日志菜单项添加到 SSMA （RFC 5706203）。
* 添加了遥测。

## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版本的 Oracle SSMA 包含以下更改：

* 添加了对 Azure SQL DB 的支持。
* 扩展包功能移动到架构以支持 Azure SQL DB。
* 添加了对 Oracle 具体化视图的支持。
* 添加了对 SQL Server 2014 内存优化表的支持。
* 包括为具有 10k 个以上对象的数据库测试的性能改进。
* 添加了用于处理大量对象的 UI 改进。
* 添加了已知 LOB 架构的突出显示。
* 包括转换速度改进。
* 添加了对在 UI 中显示对象计数的支持。
* 报表大小减少 25% 以上。
* 改进了未解析构造的错误消息。

## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版本的 Oracle SSMA 包含以下更改：

* 添加了对 MS SQL Server 2014 的支持。
* 添加了对 Oracle 12 和查询优化的支持。
* 修复了有关转换为 Azure 的错误。
* 修复了 IE 10 中不可见报表页的 Bug。

## <a name="january-2012"></a>2012 年 1 月

2012 年 1 月版本的 Oracle SSMA 添加了对 默认`RowType`的`NULL`和默认的输入参数的支持和`RecordType`输入参数。

## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版本的 Oracle SSMA 包含以下更改：

* 添加了对将 Oracle 序列转换为[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]序列生成器的支持。
* 改进了数据迁移期间的错误报告。
* 使用保留词改进语句的转换。
* 改进了函数中日期值的隐式转换。

## <a name="april-2011"></a>2011 年 4 月

2011 年 4 月版本的 Oracle SSMA 包含以下更改：

* 整合的"甲骨文 SSMA"产品，支持[!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]和[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]。
* 添加了对连接和迁移到[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]的支持。
* 增强的客户端数据迁移引擎，支持数据的并行迁移。
* 使用`Simple`和`Bulk`记录恢复模型提高了数据迁移性能。
* 添加了对早期版本的 SSMA（v4.0 和 v4.2）创建的项目的向后兼容性的支持。
* 添加了使用旧版本的 SSMA（v4.0 和 v4.2）并排安装 Oracle v5.0 产品 SSMA （SxS） 的能力。
* 添加了对报告用户定义类型（包括子类型、`VARRAY`对象`NESTED TABLE`表和对象视图）及其在 PL/SQL 块中的用法的支持，并带有特殊错误消息。

## <a name="july-2010"></a>2010 年 7 月

2010 年 7 月发布的 Oracle SSMA 新增了：

* 支持迁移到 SQL Server 2008 R2。
* 用于命令行执行的新 SSMA 控制台应用程序。
* 使用服务器端和客户端数据迁移引擎支持数据迁移。
* 在数据迁移中支持"自定义 SELECT"语句。
* 支持从 Oracle 11g R2 迁移。

## <a name="june-2008"></a>2008 年 6 月

2008 年 6 月版本的 Oracle SSMA 包含以下更改：

* 增加了评估报告的改进，包括同义词的其他信息、可解析对象的原始源、面板和 SQL Server 徽标删除以及布局持久性。
* 在对象转换方面增加了改进：
  * 包`DBMS_LOB` `DBMS_SQL` ， 转换添加.
  * 加入已修订的转化。
  * 修改集合和记录转换，现在转换记录，在通过每个字段的单独变量发布的简单情况下。
  * 改进记录和集合实现。
  * 添加了窗口聚合函数。
  * `ROLLUP`/`CUBE`添加了子句。
  * 改进。 `NEXTVAL` / `CURVAL`
  * 添加了子句`SET`、分组集和分组 ID 中的列分组。
  * `MERGE`声明添加。
  * 支持新的日期时间类型，并在添加 CLR 数据类型时转换记录和集合。
* 添加了测试器的新功能。 现在可以使用 Tester 将表作为对象进行测试，可以更改测试用例中多个可测试对象的调用顺序，用户可以使用记录和集合作为参数和返回值来测试过程和函数，并添加了依赖关系分析器以仅检查使用的表。
  
## <a name="august-2007"></a>2007 年 8 月

2007 年 8 月发布的 Oracle SSMA 增加了：

* 新的 Tester 组件允许您创建、管理和运行测试用例，以验证转换后的 SQL 代码。
* 支持转换 Oracle 子类型、集合和本地模块已添加到 SQL 转换器中。
* 新的同步功能允许您将特定对象与 SQL Server 数据库同步。
* 新的转换选项。
  
## <a name="april-2007"></a>2007年4月

2007 年 4 月发布的 Oracle SSMA 是首次发布。
