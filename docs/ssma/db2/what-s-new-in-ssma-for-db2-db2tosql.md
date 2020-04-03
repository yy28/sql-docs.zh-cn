---
title: DB2 （DB2ToSQL） SSMA 中的新增功能 |微软文档
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: jtoland;alexiva
ms.openlocfilehash: 53a159627750a5ec66b5aa0b3fd6510c647e26a5
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625516"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>DB2 （DB2ToSQL） SSMA 中的新增功能

本文列出了每个版本中 DB2 更改的 SQL 服务器迁移助手 （SSMA）。

## <a name="ssma-v88"></a>SSMA v8.8

DB2 的 SSMA v8.8 版本包括：

* SQL Server 对象同步稳定性改进
* 评估和转换期间的 GUI 性能改进
* 更新映射，`ROWID``varbinary(40)`以方便数据迁移
* 改进语句转换`SELECT ... FROM NEW/OLD TABLE`
* 程序和职能`ALTER`报表的新转换
* 解构分配的新转换

## <a name="ssma-v87"></a>SSMA v8.7

DB2 的 SSMA v8.7 版本包括全新的 DB2 语法解析器，以及图形用户界面中的次要修复和性能改进。

此外，DB2 的 SSMA 现在提供：

* 在 LUW 上从 DB2 迁移时发现外键的修复程序。
* 改进了语句`SELECT ... FOR UPDATE`的转换。
* 改进了`COUNT`MQ 表中函数的转换。
* 语句的`SAVEPOINT`转换。
* 转换以模拟 DB2 对`NULL`子句中`ORDER BY`的值的行为。
* 分析对关联结果设置语句的支持。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v86"></a>SSMA v8.6

除了一组旨在提高可用性和性能的有针对性的修补程序外，DB2 的 V8.6 版本通过添加允许用户在转换后的代码中省略 SSMA 扩展属性的设置进行了增强。

要利用此设置，在 DB2 的 SSMA 中，导航到 **"工具** > **项目设置** > **常规** > **转换**"，然后在**Misc**下，将 **"省略扩展属性**"设置的值更新为 **"是**"。

![省略扩展属性设置](../db2/media/ssma-omit-extended-properties.png)

此外，DB2 的 SSMA 现在提供：

* 用于转换使用默认参数值的函数的修复程序。
* 改进了函数子`PARAMETER`句的解析。
* 转换`LEAVE`语句的能力。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v85"></a>SSMA v8.5

支持 Azure Active Directory 身份验证和对 SQL 服务器中的 JSON 功能的基本支持，以及一组旨在提高可用性和性能的有针对性的修补程序，增强了 DB2 的 SSMA v8.5 版本。

此外，DB2 的 SSMA 还通过：

* 支持将转换添加到`GET DIAGNOSTICS`语句。 `ROW_NUMBER`
* 与对象名称开头未受尊重的空间相关的 Bug 的修复。

> [!IMPORTANT]
> 使用 SSMA v8.5 时，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v84"></a>SSMA v8.4

DB2 的 SSMA v8.4 版本通过有针对性的修补程序进行增强，这些修补程序旨在解决辅助功能问题并修复 SQL Server 2016 和更高版本的最大索引列（允许 32 而不是 16）相关的 Bug。

> [!IMPORTANT]
> 对于 SSMA 版本 7.4 但 8.4，.NET 4.5.2 是安装的先决条件。

## <a name="ssma-v83"></a>SSMA v8.3

DB2 的 SSMA v8.3 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。 此外，此版本的 DB2 的 SSMA 提供了以下修补程序：

* 解决辅助功能问题。
* 添加对`hierarchyid`SQL Server 类型的基本支持。
* 将 z/OS 发现查询中的 TRIM`RTRIM`/`LTRIM`函数用法替换为 。
* 允许用户在"标准模式"连接时指定包集合（默认为`NULLID`）。
* 添加 转换`CREATE TABLE AS SELECT`。
* 改进全局临时表的转换。
* 解决对象唯一性检查顺序的问题，以便在名称冲突时将表优先于约束的优先级。
* 解决为 z/OS 加载`DATE`默认`TIMESTAMP`列值的问题。
* 支持 Unicode 行馈送字符（`NEL`也称为 ）。
* 解决缺少`RETURN TO`子句的游标转换问题。
* 添加对标签和`GOTO`的支持。

## <a name="ssma-v82"></a>SSMA v8.2

DB2 的 SSMA v8.2 版本得到了增强，用于解决从 SSMA 控制台工具连接到 Azure SQL 数据库的问题，并在转换期间在视图声明中缺少COUNT_BIG列。 此外，此版本还包括一组旨在提高质量和转化指标的有针对性的修补程序，以及用于以下的修补程序：

* 数据迁移后禁用的非群集索引的问题。
* 在静默安装期间检测 .NET 框架。
* 下载新版本时发生的间歇性崩溃。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.1 到 v8.2 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v81"></a>SSMA v8.1

DB2 的 SSMA v8.1 版本得到增强，可提供旨在提高质量和转换指标的有针对性的修补程序。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.0 到 v8.1 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v80"></a>SSMA v8.0

DB2 的 SSMA v8.0 版本得到了增强，可提供旨在提高质量和转换指标的有针对性的修补程序。 此版本还提供以下新功能：

* 支持**Azure SQL 数据库托管实例**作为目标。 现在，您可以创建针对 Azure SQL 数据库托管实例的新项目：

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

* 转换后**修复顾问**。 在此处了解有关它的更多[。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步数据库/架构选择。

  连接到源时，用户现在可以选择感兴趣的数据库/架构。 仅选择计划迁移的架构将节省时间连接期间的时间，并提高 SSMA 的整体性能。

  ![SSMA 筛选对象](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

DB2 的 SSMA v7.10 版本包含以下更改：

* 旨在提供额外安全和隐私保护以满足全球需求变化的有针对性的修补程序。
* 用于转换块的`BEGIN-END`修复程序。

## <a name="ssma-v79"></a>SSMA v7.9

DB2 的 SSMA v7.9 版本包含以下更改：

* 提高质量和转化指标的针对性修复。
* 支持 SSMA 命令行以更改数据类型映射和项目首选项。
* 支持使用 SQL 服务器集成服务 （SSIS） 迁移数据。 转换架构后，可以使用右键单击上下文菜单选项创建 SSIS 包。
* SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在 SSMA 的早期版本中，必须在项目设置中显式提及 Azure SQL 数据库前缀。

## <a name="ssma-v78"></a>SSMA v7.8

DB2 的 SSMA v7.8 版本包含以下更改：

* 更改类型映射在*项目设置*中突出显示。
* 用户禁用遥测功能。

## <a name="ssma-v77"></a>SSMA v7.7

DB2 的 SSMA v7.7 版本包含以下更改：

* 提高质量和转化指标的针对性修复。
* 根据大众需求，DB2 的 32 位版本的 SSMA 又回来了。 与以前的实现（在 v7.4 之前）相比，有两个安装程序包，但不能并排安装。 因此，您必须根据拥有的连接组件选择最合适的版本。 如果可能，最好使用 64 位版本。

## <a name="ssma-v76"></a>SSMA v7.6

DB2 的 SSMA v7.6 版本通过提高质量和转换指标的针对性修补程序以及支持 SQL Server 2017（公共预览）来增强。 Windows 和 Linux 上对 SQL Server 2017 的支持处于公共预览版，不应用于生产迁移。

## <a name="ssma-v75"></a>SSMA v7.5

DB2 的 SSMA v7.5 版本通过多项改进进行了增强，以确保残障人士获得更大的可访问性。

## <a name="ssma-v74"></a>SSMA v7.4

DB2 的 SSMA v7.4 版本包含以下更改：

* **查询超时**选项现在在源和目标架构对象发现期间可用。

  ![查询超时选项](../media/query-timeout_red.png)

* 质量和转化指标已根据客户反馈通过有针对性的修复得到了改进。

  > [!IMPORTANT]
  > .NET 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本已停产。

## <a name="ssma-v73"></a>SSMA v7.3

DB2 的 SSMA v7.3 版本包含以下更改：

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

DB2 的 SSMA v7.2 版本包含以下更改：

* 根据客户反馈有针对性地修复，提高质量和转化指标。
* 遥测增强功能，以提供更好的数据点，以解决客户问题并提高 SSMA 的转化率。

## <a name="ssma-v71"></a>SSMA v7.1

DB2 的 SSMA v7.1 版本包含以下更改：

* Windows 和 Linux CTP1 上的 SQL Server 2017 现在是支持迁移的目标平台。 此功能处于技术预览中，允许架构和数据移动以目标 SQL 服务器为目标。
* 支持自动更新，以便一旦 SSMA 可用，立即下载。
* SSMA 可安装二进制文件现在通过 Windows 安装程序包文件 （.msi） 传递。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 DB2 的 SSMA 包含以下更改：

* 添加了对 SQL Server 2016 的支持。
* 将 DB2 内存中表和常规表转换为 SQL Server 内存中和 hekaton 功能。
* 将 DB2 访问控件转换为 SQL Server 策略对象（DB2 的行级安全性）。
* 将 DB2 系统版本化表转换为 SQL Server 临时性表。
* 改进了 DB2 解析器和解析器。
* 已删除的安装程序检查 .NET 2.0。
* 从\*Db2 安装程序中删除了不必要的 .dll。
* SSMA 控制台的固定`save-project`和`open-project`命令。
* SSMA 控制台的固定`securepassword`命令。
* 修复了初始加载的对象计数。
* 修复了全局设置中的 Bug。
  
## <a name="march-2016"></a>2016 年 3 月

DB2 的 SSMA 预览版 2016 年 3 月增加了对迁移到 SQL Server 2016 的支持。

## <a name="january-2016"></a>2016 年 1 月

DB2 的 SSMA 2016 年 1 月维护版本包含以下更改：
  
* 增加了对许多标准功能的支持。
* 修复了 DB2 分析器错误。
* 固定 DB2 v9 zOS 支持 （RFC 5690920）。
* 修复了转换过程中未解决的 DB2 标识符错误。
* 将视图日志菜单项添加到 SSMA （RFC 5706203）。
* 添加了遥测。
  
## <a name="november-2014"></a>2014 年 11 月

2014 年 11 月版本的 DB2 的 SSMA 是初始版本。
