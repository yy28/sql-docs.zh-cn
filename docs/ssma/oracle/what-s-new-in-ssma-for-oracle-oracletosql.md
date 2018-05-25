---
title: SSMA for Oracle (OracleToSQL) 中的新增 |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 03/01/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d80bf7637c5c17cdade7c47f25265a6d2b6c94c1
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle (OracleToSQL) 的新增功能
本主题列出每个版本中的 Oracle 更改 SSMA。  

## <a name="ssma-v77"></a>SSMA v7.7
适用于 Oracle 的 SSMA v7.7 版本包含以下更改：
- 适用于 Oracle 的 SSMA 已得到增强提高质量和转换的度量值的目标修补程序。
- 32 位版本的适用于 Oracle 的 SSMA 根据普遍需求，已恢复。 与以前的实现 （之前 v7.4) 相比，有两个安装包，但它们不能并行安装。 因此，你必须选择最适合您的版本基于连接组件。 最好始终使用 64 位版本，如有可能。
- SQL Server 2017 支持现已正式使用 Oracle 扩展包以及支持在 Linux 上 （新的远程安装选项）。 请注意，扩展包功能有限时安装在 Linux 上，因为不支持的测试人员和服务器端数据迁移功能 
- 适用于 Oracle 的 SSMA 允许你迁移作为普通表的具体化视图 (可通过在设置配置**项目设置** -> **同步** ->  **发现的具体化视图的后备表**)。

> [!IMPORTANT]
> SSMA v7.4 和更高版本，.Net 4.5.2 是安装先决条件。

## <a name="ssma-v76"></a>SSMA v7.6
适用于 Oracle 的 SSMA v7.6 版本已得到增强，具有提高质量和转换的度量值的目标修补程序和 SQL Server 2017 （公共预览版） 支持。 对于 Windows 和 Linux 上的 SQL Server 2017 支持是在公共预览版中并不用于生产迁移。

> [!IMPORTANT]
> SSMA v7.4 和更高版本，.Net 4.5.2 的目标是安装先决条件，并已停止使用该工具的 32 位版本。

## <a name="ssma-v75"></a>SSMA v7.5 还是
适用于 Oracle 的 SSMA v7.5 还是版本包含以下更改：
- 增强了多项改进，以确保残障人士更大的可访问性。
- 更新以改进的质量和转换指标，目标修补程序，如改进数据在迁移期间，根据客户反馈的日期和 float 数据类型处理。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.5 还是的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。

## <a name="ssma-v74"></a>SSMA v7.4
适用于 Oracle 的 SSMA v7.4 版本包含以下更改：

- 适用于 Oracle 的 SSMA 现在支持 Azure SQL 数据仓库用作迁移的目标平台。

    ![新项目窗口](../media/new-project.png)
  - 支持的数据仓库存储选项，在下图中所示：

    ![数据仓库的存储选项](../media/storage-options_red.png)
  - 支持的数据分布选项，在下图中所示：

    ![数据仓库的数据分布](../media/data-distribution_red.png)

- **查询超时值**选项现已可用在源和目标架构对象发现期间。

    ![query timeout 选项](../media/query-timeout_red.png)

- 通过目标修补程序，根据客户反馈，改进了的质量和转换的度量值。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。

## <a name="ssma-v73"></a>SSMA v7.3
适用于 Oracle 的 SSMA v7.3 版本包含以下更改：
- 改进的质量和转换度量值根据客户反馈的目标修补程序。
- SSMA 扩展性框架公开通过以下各项：
  - 导出到 SQL Server Data Tools (SSDT) 项目的功能。
    -   你现在可以将架构脚本从 SSMA 导出到 SSDT 项目。 可以使用架构脚本进行其他架构更改和部署你的数据库。
![将另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  - 可用于执行自定义转换供 SSMA 的库。
    - 你现在可以构造自定义的语法转换和先前未由 SSMA 处理的转换可以处理的代码。
      - 在此博客文章中，提供了有关如何构造的自定义转换器说明[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 下载此转换的示例项目[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。


## <a name="ssma-v72"></a>SSMA 7.2 版
适用于 Oracle 的 SSMA 7.2 版版本包含以下更改：
- 改进的质量和转换度量值根据客户反馈的目标修补程序。
- 遥测功能增强以提供更好的数据点，以解决客户问题和改进 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1
适用于 Oracle 的 SSMA v7.1 版本包含以下更改：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 现在是一个用于迁移的支持的目标平台。 此功能是 technical preview 中，并且允许架构和数据移动到目标 SQL 服务器。
- SSMA 现在支持自动更新，以下载最新版本的 SSMA，只要可用。
- SSMA 可安装二进制文件现在被通过 Windows installer 包文件 (.msi)。

**资源**

[将 SQL Server Migration Assistant 的转换功能扩展](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[评估并将数据从非 Microsoft 数据平台迁移到 SQL Server *（与 Oracle 示例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年 5 月  
适用于 Oracle 的 SSMA 的 2016 年 5 月版本包含以下更改：  

- 添加了对 SQL Server 2016 的支持。
- 向 SQL Server 临时表的 Oracle 闪回存档表添加的转换。

    **请注意**-SSMA 不会复制从 Oracle 闪回数据存档表的历史记录数据。 因此，必须在迁移过程中手动复制历史记录数据。 此外，虽然 SSMA 不在 SQL Server 元数据资源管理器中显示历史记录表，因为它将被视为系统表，你可以在 SQL Server Management Studio 中查看历史记录表。
    SQL Server 2016 中不支持多个 Oracle 闪回功能，包括：
    - Oracle 闪回事务查询
    - DBMS_FLASHBACK 包
    - 闪回事务
    - 闪回数据存档
    - 闪回表
    - 闪回拖放
    - 闪回数据库
- 添加的转换 Oracle VPD 策略为 SQL Server 策略对象 （适用于 Oracle 的行级别安全性）。
- 适用于 Oracle 的初始加载降低的时间。
- 改进的分析器和冲突解决程序。
- 删除安装程序检查 for.Net 2.0。
- 更新到.Net 4.0 通过.Net 3.5 的扩展包依赖性。
- "保存项目"固定和 SSMA 控制台的"打开项目"命令。
- SSMA 控制台的固定"securepassword"命令。
- 固定的初始加载的对象计数。
- 修复对于 Oracle 的字符数据类型转换。
- 全局设置中的已修复的 bug。
  
## <a name="march-2016"></a>2016 年 3 月  
适用于 Oracle 的 SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
-   添加了对迁移到 SQL Server 2016 的支持。  
-   添加了对迁移 Oracle 行级别安全性 （有一些限制） 的支持。  
-   添加了支持迁移到 SQL Server 列存储在内存中的 Oracle 表。  
  
## <a name="january-2016"></a>2016 年 1 月  
2014 年 1 月的适用于 Oracle 的 SSMA 维护版本包含以下更改：  
  
-   添加了对聚集索引的支持。  
-   修复速度慢的 Oracle 架构查询 (RFC 5076207)。  
-   固定从控制台连接到 Azure。  
-   添加的视图日志菜单项的 SSMA (文档 RFC 5706203)。 
-   添加的遥测。  
  
## <a name="july-2014"></a>2014 年 7 月  
适用于 Oracle 的 SSMA 的 2014 年 7 月版本包含以下更改：  
  
-   添加了对 Azure SQL DB 的支持。  
-   扩展包功能移到架构以支持 Azure SQL DB。  
-   添加了对 Oracle 具体化视图的支持。  
-   添加的支持 SQL Server 2014 内存优化表。  
-   包含的性能改进测试具有超过 10 k 的数据库对象。  
-   添加了对具有大量对象的处理 UI 改进。  
-   添加突出显示的"已知"LOB 架构。  
-   包括转换速度方面的改进。  
-   添加了对显示对象支持对用户界面中进行计数。  
-   降低的报表大小超过 25%。
-   未分析构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
适用于 Oracle 的 SSMA 的 2014 年 4 月版本包含以下更改：  
  
-   添加了 MS SQL Server 2014 的支持。  
-   添加了支持的 Oracle 12 和查询优化。  
-   有关转换到 Azure 的已修复的 bug。  
-   有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
适用于 Oracle 的 SSMA 的 2012 年 1 月版本包含以下更改：  
  
-   添加了对 RowType 和 RecordType 输入参数支持默认为 NULL。  
  
## <a name="july-2011"></a>2011 年 7 月  
适用于 Oracle 的 SSMA 的 2011 年 7 月版本包含以下更改：  
  
-   增加了对转换到的 Oracle 序列支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"序列生成器。  
-   改进了的错误报告数据迁移过程。  
-   使用保留的字的语句的改进的转换。  
-   改进的函数中的日期值的隐式转换。  
  
## <a name="april-2011"></a>2011 年 4 月  
适用于 Oracle 的 SSMA 的 2011 年 4 月版本包含以下更改：  
  
-   合并"SSMA 为 Oracle"产品，它支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   增加了对连接并将迁移到支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   增强的客户端数据迁移引擎，支持的数据的并行迁移。  
-   提高的数据迁移性能与简单和大容量日志恢复模式。  
-   添加了对早期版本的 SSMA （v4.0 和 v4.2） 创建的项目的向后兼容性的支持。  
-   添加要为 Oracle 5.0 版产品并行 (SxS) 与旧版本的 SSMA （v4.0 和 v4.2） 安装 SSMA 的能力。  
-   添加了对用户定义类型 （包括子类型、 VARRAY、 嵌套表、 对象表和对象视图） 和它们的用法 PL/SQL 块使用特殊的错误消息中报告的支持。  

## <a name="july-2010"></a>2010 年 7 月  
适用于 Oracle 的 SSMA 2010 年 7 月版本包含以下更改：  
  
-   添加了对将迁移到 SQL Server 2008 R2 的支持。  
-   添加的新的 SSMA 控制台应用程序命令行执行。  
-   添加了对使用服务器端和客户端数据迁移引擎的数据迁移的支持。  
-   添加了对"自定义选择"语句中数据迁移的支持。  
-   添加了对从 Oracle 11g R2 进行迁移的支持。  
  
## <a name="june-2008"></a>2008 年 6 月  
适用于 Oracle 的 SSMA 2008 年 6 月版本包含以下更改：  
  
-   添加到评估报表中，包括有关同义词的其他信息、 分析对象、 面板和 SQL Server 徽标删除操作，和布局持久性的原始源了改进。  
-   添加了对象转换中的改进：  
    -   包 DBMS_LOB、 DBMS_SQL 转换添加。  
    -   联接修订的转换。  
    -   修改集合和记录转换，现在简单的情况下释放通过为每个字段的单独变量中的记录的转换。  
    -   记录和集合实现的改进。  
    -   添加的开窗聚合函数。  
    -   汇总/多维数据集添加子句。  
    -   NEXTVAL/CURVAL 的改善。  
    -   在 SET 子句中分组的列，对集进行分组和分组 ID 已添加。  
    -   MERGE 语句添加。  
    -   新的日期时间类型和记录和集合转换为添加的 CLR 数据类型的支持。  
-   增加的测试人员的新功能。 现在可以使用测试人员对象作为测试表，可以更改测试用例中的几个可测试对象的调用顺序，用户可以测试过程和函数与记录和集合作为参数和返回值，并添加了分析器来检查依赖关系仅使用表。  
  
## <a name="august-2007"></a>2007 年 8 月  
适用于 Oracle 的 SSMA 的 2007 年 8 月版本包含以下更改：  
  
-   添加新的测试人员组件可让您创建、 管理和运行测试用例来验证转换后的 SQL 代码。  
-   添加了对 Oracle 子类型、 集合和本地模块的转换支持已添加到 SQL 转换器。  
-   添加新的同步功能，可以将特定对象与 SQL Server 数据库同步。  
-   添加了新转换选项。  
  
## <a name="april-2007"></a>2007 年 4 月  
2007 年 4 月版本的适用于 Oracle 的 SSMA 是初次发布。
