---
title: SSMA for Oracle 中的新增功能（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/06/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 95b2ebd450fe54a2e02e5eed77a5259a8437e7ef
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745486"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle 中的新增功能（OracleToSQL）

本文列出了每个版本中 Oracle 更改的 SQL Server 迁移助手（SSMA）。

## <a name="ssma-v84"></a>SSMA v2。0

SSMA for Oracle 的 v2.0 版本使用旨在解决辅助功能问题的目标修补程序进行了增强，并修复了与最大索引列（为32，而不是16）相关的 bug，以支持 SQL Server 2016 及更高版本。

此外，此版本的 SSMA for Oracle 添加了**SYS_REFCURSOR**的转换作为存储过程输出参数。

> [!IMPORTANT]
> 对于 SSMA 7.4 和更高版本，.Net 4.5.2 是必备组件。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for Oracle 的 v 8.3 版本通过旨在改进质量和转换指标的目标修补程序进行了增强。 此外，此版本的 SSMA for Oracle 还提供了以下修补程序：

* 解决辅助功能问题
* 在 SQL Server 中添加 "hierarchyid" 类型的基本支持
* 解决通过同义词调用的函数的返回类型未知的问题
* 将 ODP.NET 更新为 v 19。3

## <a name="ssma-v82"></a>SSMA v8.2

适用于 Oracle 的 SSMA 的版本8.2 版本增强为：

* 添加对 DBMS_OUTPUT 的支持。启用/禁用。
* 在默认数据迁移查询中删除 BINARY_FLOAT 和 BINARY_DOUBLE 列的 FLOAT 强制转换。
* 如果当前值已更改，则修复序列刷新。
* 如果存在具有相同名称的列，请修复与伪列的误解相关的 bug （ROWNUM 等）。
* 修复了在使用不明确的未解析标识符的情况转换时发生的崩溃。

此外，此版本还包括一组旨在提高质量和转换指标的目标修补程序，以及对的修复：

* 数据迁移后已禁用的非聚集索引的问题。
* 在无提示安装期间检测 .NET Framework。
* 下载新版本时出现间歇性崩溃。

> [!NOTE]
> 自动更新的一个已知问题可能会导致从 SSMA v4.0 到 v4.0 8.2 的更新失败。 如果遇到此错误，请下载并手动安装新版本。

## <a name="ssma-v81"></a>SSMA v8.1

适用于 Oracle 的 SSMA 的7.4 版已通过旨在提高质量和转换指标的目标修补程序进行了增强。

> [!NOTE]
> 自动更新的一个已知问题可能会导致从 SSMA 8.0 到 app-v 8.1 的更新失败。 如果遇到此错误，请下载并手动安装新版本。

## <a name="ssma-v80"></a>SSMA v8.0

SSMA for Oracle 的 v2.0 版本通过旨在改进质量和转换指标的目标修补程序进行了增强。 此版本还提供以下新增功能：

* 支持作为目标**Azure SQL 数据库托管实例**。 你现在可以创建面向 Azure SQL 数据库托管实例的新项目：

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > 还更新了 SSMA for Oracle 扩展包，以允许 Azure SQL 数据库托管实例上的远程安装：
  >
  > ![Oracle 扩展包的 SSMA](../media/ssma-oracle-ext-pack.png)

  面向 Azure SQL 数据库托管实例时，某些功能（包括测试人员和服务器端数据迁移）不受支持。 [在此处](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)阅读详细信息。

* 转换后**修补顾问**。 [在此处](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)了解详细信息。

* 初步的数据库/架构选择。

  连接到源时，用户现在可以选择数据库/感兴趣的架构。 仅选择你计划迁移的架构将在初始连接期间节省时间，并提高总体 SSMA 性能。

  ![SSMA 筛选器对象](../media/ssma-filter-objects.png)

* 能够使用官方的托管网络驱动程序连接到 Oracle。 OCI 驱动程序不再是使用适用于 Oracle 的 SQL Server 迁移助手的先决条件。

* 默认情况下，将 ROWID 和 UROWID 映射到 VARCHAR 的能力。 已从 "uniqueidentifier" 更改为适用于显式 ROWID 列的数据迁移。

## <a name="ssma-v710"></a>SSMA v7.10

适用于 Oracle 的 SSMA 的版本7.10 版本包含以下更改：

* 旨在提供附加安全和隐私保护以满足全局要求更改的目标修补程序。
* 与分层查询相关的转换改进。

## <a name="ssma-v79"></a>SSMA v7.9

SSMA for Oracle 的 v 7.9 版本包含以下更改：

* 改进质量和转换指标的目标修补程序。
* 支持将 "Continue" 语句从 Oracle 迁移到 SQL Server。
* 支持在 SSMA 命令行中更改数据类型映射和项目首选项。
* 支持使用 SQL Server Integration Services （SSIS）迁移数据。 转换架构后，可以使用右键单击上下文菜单选项创建 SSIS 包。
* 还更改了 SSMA 中的 Azure SQL 数据库连接对话框以指定完全限定的服务器名称。 在以前版本的 SSMA 中，必须在项目设置中显式提到 Azure SQL 数据库前缀。

## <a name="ssma-v78"></a>SSMA v7.8

SSMA for Oracle 的7.4 版版本包含以下更改：

* 支持：
  * IN 子句的行表达式。
  * 隐式类型转换。
  * 适用于 Azure SQL 数据库的 UID 转换。
* 更改项目设置中突出显示的类型映射。
* 允许用户禁用遥测数据。

## <a name="ssma-v77"></a>SSMA v7.7

SSMA for Oracle 的 v4.0 版本包含以下更改：

* SSMA for Oracle 已通过可提高质量和转换指标的目标修补程序进行了增强。
* 基于热门需求，SSMA for Oracle 的32位版本将恢复。 与之前的实现（在7.4 之前）相比，有两个安装包，但不能并行安装。 因此，你必须根据你拥有的连接组件选择最适合的版本。 如果可能，始终最好使用64位版本。
* SQL Server 2017 支持现已正式成为 Linux 上支持的 Oracle 扩展包（新的远程安装选项）。 请注意，在 Linux 上安装时，扩展包功能是有限的，因为不支持测试人员和服务器端数据迁移功能。
* SSMA for Oracle 允许您将具体化视图作为常规表进行迁移（可通过**项目设置** -> **同步** -> **发现具体化视图的支持表**）中的设置进行配置。

## <a name="ssma-v76"></a>SSMA v7.6

适用于 Oracle 的 SSMA 的版本7.6 版本通过改进质量和转换指标的目标修补程序进行了增强，并支持 SQL Server 2017 （公共预览版）。 对 Windows 和 Linux 上的 SQL Server 2017 的支持是公共预览版，不应用于生产迁移。

## <a name="ssma-v75"></a>SSMA v7.5

适用于 Oracle 的 SSMA 的7.5 版本包含以下更改：

* 增强了几项改进功能，确保为残障人士提供更好的辅助功能。
* 经过更新，以通过目标修补程序提高质量和转换指标，例如，在数据迁移过程中改进了日期和 float 数据类型的处理，这是基于客户的反馈。

## <a name="ssma-v74"></a>SSMA v7.4

SSMA for Oracle 的7.4 版包含以下更改：

* SSMA for Oracle 现在支持将 Azure SQL 数据仓库作为迁移的目标平台。

  !["新建项目" 窗口](../media/new-project.png)
  * 支持数据仓库存储选项，如下图所示：

  ![用于数据仓库的存储选项](../media/storage-options_red.png)
  * 支持数据分发选项，如下图所示：

  ![数据仓库的数据分布](../media/data-distribution_red.png)

* 在源和目标中的架构对象发现期间，现在可以使用 "**查询超时**" 选项。

  ![query timeout 选项](../media/query-timeout_red.png)

* 根据客户的反馈，改进了质量和转换指标。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA 7.4 的必备组件。 此外，从7.4 版开始，32位版本的 SSMA 即将停止使用。

## <a name="ssma-v73"></a>SSMA v7.3

SSMA for Oracle 的7.3 版包含以下更改：

* 根据客户的反馈，改进了质量和转换指标与目标修复。
* 通过以下各项公开的 SSMA 扩展性框架：
  * 将功能导出到 SQL Server Data Tools （SSDT）项目。
    * 你现在可以将 SSMA 中的架构脚本导出到 SSDT 项目。 您可以使用架构脚本来进行其他架构更改并部署您的数据库。

      ![另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  * 可供 SSMA 使用的库，用于执行自定义转换。
    * 你现在可以构造代码，该代码可以处理 SSMA 之前未处理的自定义语法转换和转换。
      * 此博客文章中提供了有关如何构造自定义转换器的说明，[扩展了 SQL Server 迁移助手的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下载此[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)中用于转换的示例项目。

## <a name="ssma-v72"></a>SSMA v7.2

SSMA for Oracle 的 v2.0 版本包含以下更改：

* 根据客户的反馈，改进了质量和转换指标与目标修复。
* 遥测增强功能可提供更好的数据点以解决客户问题并提高 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1

SSMA for Oracle 的 v2.0 版本包含以下更改：

* Windows 和 Linux 上的 SQL Server 2017 现在是支持迁移的目标平台。 此功能在 technical preview 中，允许将架构和数据移动到目标 SQL server。
* SSMA 现在支持自动更新，以下载最新版本的 SSMA。
* SSMA 可安装二进制文件现在通过 Windows installer 包文件（.msi）传递。

## <a name="may-2016"></a>可能为2016

SSMA for Oracle 的5月2016版包含以下更改：  

* 添加了对 SQL Server 2016 的支持。
* 添加了 Oracle 闪回存档表到 SQL Server 临时表的转换。

  > [!NOTE]
  > SSMA 不复制 Oracle 闪回数据存档表中的历史记录数据。 因此，在迁移过程中必须手动复制历史记录数据。 此外，SSMA 不会在 SQL Server 元数据资源管理器中显示历史记录表，因为它被视为系统表，你可以在 SQL Server Management Studio 中查看历史记录表。
  >
  > SQL Server 2016 不支持多个 Oracle 闪回功能，其中包括：
  >
  > * Oracle 闪回事务查询
  > * DBMS_FLASHBACK 包
  > * 闪回事务
  > * 闪回数据存档
  > * 闪回表
  > * 闪回
  > * 闪回数据库
* 添加了 Oracle VPD 策略到 SQL Server 策略对象（Oracle 行级别安全性）的转换。
* 缩短了 Oracle 初始加载的时间。
* 改进的分析器和解析程序。
* 移除了 .Net 2.0 的安装程序检查。
* 更新了从 .Net 3.5 到 .Net 4.0 的扩展包。
* 修复了用于 SSMA 控制台的 "保存项目" 和 "打开项目" 命令。
* 修复了 SSMA 控制台的 "securepassword" 命令。
* 修复了初始加载的对象计数。
* 修复了 Oracle 的字符数据类型的转换。
* 修复了全局设置中的 bug。
  
## <a name="march-2016"></a>2016 年 3 月

SSMA for Oracle 2016 年3月预览版本添加了对的支持：  
  
* 迁移到 SQL Server 2016。  
* 迁移 Oracle 行级别安全性（有一些限制）。  
* 将 Oracle in memory 表迁移到 SQL Server 列存储。  
  
## <a name="january-2016"></a>2016年1月

SSMA for Oracle 的2014年1月维护版本包含以下更改：  
  
* 添加了对聚集索引的支持。  
* 固定速度缓慢的 Oracle 架构查询（RFC 5076207）。  
* 修复了从控制台连接到 Azure。  
* 向 SSMA 添加了 "查看日志" 菜单项（RFC 5706203）。 
* 添加了遥测。
  
## <a name="july-2014"></a>2014 年 7 月

SSMA for Oracle 的2014年7月发行版本包含以下更改：  
  
* 添加了对 Azure SQL 数据库的支持。
* 扩展包功能已移动到架构以支持 Azure SQL DB。
* 添加了对 Oracle 具体化视图的支持。  
* 添加了对 SQL Server 2014 内存优化表的支持。  
* 为具有超过10k 对象的数据库测试了性能改进。  
* 添加了用于处理大量对象的 UI 改进。  
* 添加了 "知名" LOB 架构的突出显示。  
* 包含转换速度改进。  
* 添加了对在 UI 中显示对象计数的支持。  
* 将报表大小减少 25% 以上。
* 改进了未分析构造的错误消息。  
  
## <a name="april-2014"></a>2014年4月

SSMA for Oracle 的2014年4月版包含以下更改：  
  
* 添加了对 MS SQL Server 2014 的支持。  
* 添加了对 Oracle 12 和查询优化的支持。  
* 修复了有关转换到 Azure 的 bug。  
* 修复了 IE 10 中不可见报表页的相关 bug。  
  
## <a name="january-2012"></a>2012年1月

SSMA for Oracle 的2012年1月版增加了对 RowType 和 RecordType 输入参数的支持，默认为 NULL。  
  
## <a name="july-2011"></a>2011年7月

SSMA for Oracle 的2011年7月发行版本包含以下更改：  
  
* 添加了对将 Oracle 序列转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 序列生成器的支持。
* 在数据迁移过程中改进了错误报告。  
* 使用保留字改进了语句的转换。  
* 改进了函数中 date 值的隐式转换。  
  
## <a name="april-2011"></a>2011年4月

SSMA for Oracle 的2011年4月版包含以下更改：  
  
* 合并的 "SSMA for Oracle" 产品，它[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 "Denali"。
* 添加了对连接和迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 的支持。  
* 增强了客户端数据迁移引擎，支持并行数据迁移。  
* 通过简单和大容量日志恢复模式改进了数据迁移性能。  
* 添加了对 SSMA 早期版本创建的项目的后向兼容性支持（4.0 和4.2）。  
* 添加了一种功能，该功能能够安装 SSMA for Oracle 5.0 5.0 产品（早期版本的 SSMA，4.0 和4.2）。
* 添加了对报表用户定义类型（包括子类型、VARRAY、嵌套表、对象表和对象视图）的支持以及它们在 PL/SQL 块中的用法以及特殊错误消息。  

## <a name="july-2010"></a>2010年7月

添加的 SSMA for Oracle 2010 年7月发行版：

* 支持迁移到 SQL Server 2008 R2。  
* 用于执行命令行的新 SSMA 控制台应用程序。  
* 支持使用服务器端和客户端数据迁移引擎进行数据迁移。  
* 支持数据迁移中的 "自定义" SELECT 语句。  
* 支持从 Oracle 11g R2 迁移。  
  
## <a name="june-2008"></a>2008年6月

SSMA for Oracle 的2008年6月发行版包含以下更改：  
  
* 增加了对评估报表的改进，包括同义词的其他信息、可分析对象的原始源、面板和 SQL Server 徽标删除以及布局持久性。  
* 增加了对象转换的改进：  
  * 添加了包 DBMS_LOB，DBMS_SQL 转换。  
  * 联接转换已修订。  
  * 修改集合和记录转换后，就是通过每个字段的单独变量释放的简单事例中的记录转换。  
  * 改进了记录和集合实现。  
  * 添加了窗口化聚合函数。  
  * 已添加汇总/多维数据集子句。  
  * 改进 NEXTVAL/CURVAL。  
  * 添加了 SET 子句、分组集和分组 ID 中的列分组。  
  * 已添加 MERGE 语句。  
  * 添加了新的日期时间类型以及将记录和集合转换为添加的 CLR 数据类型。  
* 添加了测试人员的新功能。 现在可以使用测试人员将表测试为对象，可以更改测试用例中多个可测试对象的调用顺序，用户可以使用记录和集合测试过程和函数作为参数和返回值，并添加了依赖项分析器来检查仅使用的表。  
  
## <a name="august-2007"></a>2007年8月

添加的 SSMA for Oracle 2007 年8月版已添加：

* 新的测试人员组件允许您创建、管理和运行测试用例，以验证转换后的 SQL 代码。  
* 已将 Oracle 子类型、集合和本地模块的转换支持添加到 SQL 转换器。  
* 利用新的同步功能，您可以将特定对象与 SQL Server 数据库同步。  
* 新的转换选项。  
  
## <a name="april-2007"></a>2007年4月

SSMA for Oracle 的2007年4月版是初始版本。
