---
title: 什么是 SSMA for Oracle (OracleToSQL) 中的新增功能 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: HJToland3
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bd80395b4df7957f48cc480ba858af387e870b86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66841099"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>什么是 SSMA for Oracle (OracleToSQL) 中的新增功能
本文列出了每个版本中的 Oracle 更改 SQL Server Migration Assistant (SSMA)。

## <a name="ssma-v82"></a>SSMA v8.2

适用于 Oracle 的 SSMA v8.2 发布功能得到增强：

* 添加对 DBMS_OUTPUT 的支持。启用/禁用。
* 删除 CAST AS 浮动 BINARY_FLOAT 和 BINARY_DOUBLE 列在默认数据迁移的查询。
* 如果当前值已更改，请修复序列刷新。
* 修复 bug 相关错误地解释 （ROWNUM 等） 的伪列，如果存在具有相同名称的列。
* 修复崩溃发生转换具有不明确的无法解析标识符的循环。

此外，此版本包含一组目标的设计用于提高质量和转换指标，以及针对修补程序的修补程序：

* 数据迁移后禁用非聚集索引的问题。
* 在无提示安装过程中的.NET Framework 检测。
* 下载新版本时，会发生间歇性崩溃。

> [!NOTE]
> 自动更新的已知的问题可能会导致失败的更新从 SSMA v8.1 v8.2。 如果遇到此错误，请下载最新版本，然后手动安装它。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v81"></a>SSMA v8.1

适用于 Oracle 的 SSMA v8.1 版本增强了能够提高质量和转换的度量值的目标修补。

> [!NOTE]
> 自动更新的已知的问题可能会导致失败的更新从 SSMA v8.0 v8.1。 如果遇到此错误，请下载最新版本，然后手动安装它。

## <a name="ssma-v80"></a>SSMA v8.0

适用于 Oracle 的 SSMA v8.0 版本增强了设计用于提高质量和转换的度量值的目标修补。 此版本还提供了以下新功能：

* 为支持**Azure SQL 数据库托管实例**作为目标。 现在可以创建目标 Azure SQL 数据库托管实例的新项目：

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > SSMA for Oracle 的扩展包，也已更新为允许远程安装在 Azure SQL 数据库托管实例上：
  >
  > ![SSMA for Oracle 扩展包](../media/ssma-oracle-ext-pack.png)

  面向 Azure SQL 数据库托管实例时，不支持某些功能，包括测试人员和服务器端数据迁移。 有关详细信息[此处](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)。

* 转换后**修复顾问**。 了解有关它的详细信息[此处](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)。

* 初步的数据库架构所选内容。

  连接到源时，用户现在可以选择感兴趣的数据库/架构。 选择你打算迁移的架构将保存在初始连接期间的时间并改进整体 SSMA 性能。

  ![SSMA 筛选对象](../media/ssma-filter-objects.png)

* 能够使用官方，管理连接到 Oracle 的.NET 驱动程序。 OCI 驱动程序不再是使用 SQL Server Migration Assistant for Oracle 的先决条件。

* 默认情况下映射到 VARCHAR ROWID 和 UROWID 功能。 从 'uniqueidentifier' 以适应显式 ROWID 列的数据迁移更改。

## <a name="ssma-v710"></a>SSMA v7.10

适用于 Oracle 的 SSMA v7.10 版本包含以下更改：

* 可提供额外的安全和隐私保护功能以满足全局要求中的更改的目标的修补。
* 转换改进，与分层查询相关。

## <a name="ssma-v79"></a>SSMA v7.9

适用于 Oracle 的 SSMA v7.9 版本包含以下更改：

* 提高质量和转换的度量值的目标的修补。
* 用于从 Oracle 到 SQL Server 的迁移"Continue"语句的支持。
* 支持在 SSMA 命令行中更改数据类型映射和项目首选项。
* 有关迁移支持使用 SQL Server Integration Services (SSIS) 数据。 转换后的架构，则可以通过右键单击上下文菜单选项创建的 SSIS 包。
* SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在以前版本的 SSMA，Azure SQL 数据库前缀必须明确指出在项目设置。

## <a name="ssma-v78"></a>SSMA v7.8

适用于 Oracle 的 SSMA 7.8 版版本包含以下更改：

* 支持：
  * IN 子句的行表达式。
  * 隐式类型转换。
  * Azure SQL 数据库的 UID 转换。
* 更改项目设置中突出显示的类型映射。
* 用户若要禁用遥测数据的能力。

## <a name="ssma-v77"></a>SSMA v7.7

适用于 Oracle 的 SSMA v7.7 版本包含以下更改：

* 适用于 Oracle 的 SSMA 已得到增强改进质量和转换的度量值的目标修补。
* 基于普遍的需求，返回是适用于 Oracle 的 SSMA 的 32 位版本。 与以前的实现 （之前 v7.4) 相比，有两个安装程序软件包，但不能并行安装。 因此，必须选择最适合您的版本根据连接组件。 最好始终使用 64 位版本中，在可能的情况。
* SQL Server 2017 支持现已正式与 Oracle 的扩展包，也支持在 Linux 上 （新的远程安装选项）。 请注意，扩展包功能是在 Linux 上，安装时如不支持测试人员和服务器端数据迁移功能。
* 适用于 Oracle 的 SSMA 允许您将迁移作为常规表的具体化视图 (通过在设置可配置**项目设置** -> **同步** ->  **具体化视图发现后备表**)。

## <a name="ssma-v76"></a>SSMA v7.6

适用于 Oracle 的 SSMA v7.6 版本得到了增强，提高质量和转换的度量值的目标修补和支持 SQL Server 2017 （公共预览版）。 支持 Windows 和 Linux 上的 SQL Server 2017 处于公共预览状态，不应该用于生产迁移。

## <a name="ssma-v75"></a>SSMA v7.5

适用于 Oracle 的 SSMA 版本 7.5 版本包含以下更改：

* 增强了多项改进，以确保为残障人士使用的可访问性。
* 更新以改进质量和转换规格，与目标修补，如改进数据在迁移期间，根据客户反馈的日期和 float 数据类型处理。

## <a name="ssma-v74"></a>SSMA v7.4

适用于 Oracle 的 SSMA v7.4 版本包含以下更改：

* 作为迁移的目标平台，适用于 Oracle 的 SSMA 现在支持 Azure SQL 数据仓库。

  ![新项目窗口](../media/new-project.png)
  * 支持的数据仓库存储选项，在下图中所示：

  ![数据仓库的存储选项](../media/storage-options_red.png)
  * 支持的数据分布选项，在下图中所示：

  ![数据仓库的数据分布](../media/data-distribution_red.png)

* **查询超时值**选项现可在源和目标架构对象发现期间访问。

  ![query timeout 选项](../media/query-timeout_red.png)

* 有所改进质量和转换指标，包括目标修补，根据客户反馈。

> [!IMPORTANT]
> .Net 4.5.2 是用于安装 SSMA v7.4 必备组件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停止。

## <a name="ssma-v73"></a>SSMA v7.3

适用于 Oracle 的 SSMA v7.3 版本包含以下更改：

* 改进的质量和转换度量值与目标修补，根据客户反馈。
* 通过以下各项公开的 SSMA 可扩展性框架：
  * 导出到 SQL Server Data Tools (SSDT) 项目的功能。
    * 现在，您可以到 SSDT 项目从 SSMA 导出架构脚本。 架构脚本可用于进行附加的架构更改和部署你的数据库。

      ![将另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  * 可供执行的自定义转换 SSMA 的库。
    * 现在可以构造自定义语法转换和转换之前未处理的 SSMA 能处理的代码。
      * 在此博客文章提供了有关如何构造自定义转换器说明[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下载此转换的示例项目[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA v7.2

适用于 Oracle 的 SSMA 7.2 版版本包含以下更改：

* 改进的质量和转换度量值与目标修补，根据客户反馈。
* 遥测数据增强功能提供更好的数据点来解决客户问题并提高 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1

适用于 Oracle 的 SSMA v7.1 版本包含以下更改：

* SQL Server 2017 的 Windows 和 Linux CTP1 现在是用于迁移的支持的目标平台。 此功能是 technical preview 中，使架构和数据移动到目标 SQL 服务器。
* SSMA 现在支持自动更新，以下载最新版本的 SSMA 立即可用。
* SSMA 可安装二进制文件现在被通过 Windows installer 包文件 (.msi)。

## <a name="may-2016"></a>2016 年 5 月

适用于 Oracle 的 SSMA 的 2016 年 5 月版本包含以下更改：  

* 添加了对 SQL Server 2016 的支持。
* 添加的转换 Oracle 闪回存档表为 SQL Server 的临时表。

  > [!NOTE]
  > SSMA 不会将历史记录数据复制从 Oracle 闪回数据存档表。 因此，必须在迁移过程中手动复制历史记录数据。 此外，虽然 SSMA 不会在 SQL Server 元数据资源管理器中显示历史记录表，因为它被视为系统表，您可以在 SQL Server Management Studio 中查看历史记录表。
  >
  > SQL Server 2016 不支持多个 Oracle 闪回功能，包括：
  >
  > * Oracle 闪回事务查询
  > * DBMS_FLASHBACK 包
  > * 闪回事务
  > * 闪回数据存档
  > * 闪回表
  > * 闪回下拉
  > * 闪回数据库
* 到 SQL Server 策略对象 （适用于 Oracle 的行级别安全性） 的 Oracle VPD 策略添加了的转换。
* 适用于 Oracle 的初始加载时间减少。
* 改进了的分析器和冲突解决程序。
* 删除.Net 2.0 的安装程序检查。
* 已更新的扩展包依赖项从.Net 3.5 到.Net 4.0。
* 修复了"保存项目"和 SSMA 控制台的"打开项目"命令。
* SSMA 控制台中的固定"securepassword"命令。
* 修复了初始加载的对象的计数。
* 修复了用于 Oracle 的字符数据类型转换。
* 全局设置中修复了 bug。
  
## <a name="march-2016"></a>2016 年 3 月

适用于 Oracle 的 SSMA 的 2016 年 3 月预览版本添加了对支持：  
  
* 迁移到 SQL Server 2016。  
* 迁移 Oracle 行级别安全性 （有一些限制）。  
* 迁移到 SQL Server 列存储内存表中的 Oracle。  
  
## <a name="january-2016"></a>2016 年 1 月

2014 年 1 月维护版本的适用于 Oracle 的 SSMA 还包含以下更改：  
  
* 添加了的对聚集索引。  
* 修复了速度慢的 Oracle 架构查询 (RFC 5076207)。  
* 固定从控制台连接到 Azure。  
* SSMA (RFC 5706203) 添加了的视图日志菜单项。 
* 添加了遥测数据。
  
## <a name="july-2014"></a>2014 年 7 月

适用于 Oracle 的 SSMA 的 2014 年 7 月版本包含以下更改：  
  
* 添加了的对 Azure SQL DB。
* 扩展包功能移到架构以支持 Azure SQL DB。
* 添加了的对 Oracle 具体化视图。  
* 添加了的对 SQL Server 2014 内存优化表。  
* 包含的性能改进测试具有超过 10 k 的数据库对象。  
* 添加了的大量对象处理的 UI 改进。  
* 添加突出显示的"已知"LOB 架构。  
* 包括转换速度方面的改进。  
* 添加了对显示对象支持对用户界面中进行计数。  
* 降低的报表大小的 25%以上。
* 未分析的构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月

适用于 Oracle 的 SSMA 的 2014 年 4 月版本包含以下更改：  
  
* MS SQL Server 2014 添加了的支持。  
* 添加了的支持的 Oracle 12 和查询优化。  
* 有关转换到 Azure 的已修复的 bug。  
* 有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月

适用于 Oracle 的 SSMA 的 2012 年 1 月版本添加了对行类型支持，RecordType 输入的参数的默认设置为 NULL。  
  
## <a name="july-2011"></a>2011 年 7 月

适用于 Oracle 的 SSMA 的 2011 年 7 月版本包含以下更改：  
  
* 添加支持转换到的 Oracle 序列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"序列生成器。
* 改进了的错误报告数据迁移过程。  
* 使用保留的字的声明，改进了的转换。  
* 改进了在函数中的日期值的隐式转换。  
  
## <a name="april-2011"></a>2011 年 4 月

适用于 Oracle 的 SSMA 的 2011 年 4 月版本包含以下更改：  
  
* 合并"用于 Oracle 的 SSMA"产品，它支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。
* 添加了对连接和迁移到支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。  
* 增强的客户端的数据迁移引擎，支持并行迁移的数据。  
* 改进的数据迁移性能与简单和大容量日志恢复模式。  
* 为了向后兼容早期版本的 SSMA （版本 4.0 和 4.2 版） 创建的项目添加了的支持。  
* 添加了安装 SSMA for Oracle 5.0 版产品并排 (SxS) 与较旧版本的 SSMA （版本 4.0 和 4.2 版）。
* 用于报告用户定义类型 （包括子类型、 VARRAY、 嵌套表、 对象表和对象视图） 和它们的用法 PL/SQL 块使用特殊的错误消息中添加了的支持。  

## <a name="july-2010"></a>2010 年 7 月

SSMA for Oracle 添加 2010 年 7 月版本：

* 迁移到 SQL Server 2008 R2 的支持。  
* 命令行执行的新 SSMA 控制台应用程序。  
* 使用服务器端和客户端的数据迁移引擎数据迁移的支持。  
* 对"自定义选择"语句中的数据迁移的支持。  
* 从 Oracle 11g R2 迁移的支持。  
  
## <a name="june-2008"></a>2008 年 6 月

适用于 Oracle 的 SSMA 2008 年 6 月版本包含以下更改：  
  
* 评估报告，其中包括同义词的其他信息、 分析对象、 面板和 SQL Server 徽标删除和布局持久性的原始源添加了的改进。  
* 添加了对象转换中的改进：  
  * 包 DBMS_LOB、 添加 DBMS_SQL 转换。  
  * 联接修订的转换。  
  * 修改集合和记录转换，现在发布通过为每个字段的不同变量的简单用例中的记录的转换。  
  * 记录和集合实现的改进。  
  * 添加窗口化聚合函数。  
  * 汇总/多维数据集添加子句。  
  * NEXTVAL/CURVAL 的改进。  
  * 已将列在 SET 子句中分组，分组集，并对 ID 进行分组添加。  
  * MERGE 语句添加。  
  * 新日期时间类型和为添加的 CLR 数据类型的记录和集合的转换的支持。  
* 添加了新功能的测试人员。 现在可以使用测试人员对象测试表、 可以更改测试用例中的多个可测试对象的调用顺序，用户可以测试过程和函数与记录和集合作为参数和返回值和添加了一种依赖关系分析程序来检查仅已用表。  
  
## <a name="august-2007"></a>2007 年 8 月

SSMA for Oracle 添加 2007 年 8 月版本：

* 新的测试人员组件，可以创建、 管理和运行测试用例，若要验证转换后的 SQL 代码。  
* 支持转换 Oracle 子类型、 集合和本地模块已添加到 SQL 转换器。  
* 新的同步功能允许您将特定对象与 SQL Server 数据库同步。  
* 新转换选项。  
  
## <a name="april-2007"></a>2007 年 4 月

2007 年 4 月发布的适用于 Oracle 的 SSMA 是初次发布。
