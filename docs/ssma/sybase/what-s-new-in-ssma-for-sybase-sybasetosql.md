---
title: SSMA for SAP ASE 中的新增功能 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: b0284d0a562578e8b27f492e79e9662a240f8ccb
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811437"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>SSMA for SAP ASE 中的新增功能 (SybaseToSQL)
本文列出了每个版本中的 SAP ASE SQL Server 迁移助手 (以前称为 SSMA) 的更改。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for SAP ASE 的 v 8.3 版本已通过旨在提高质量和转换指标的目标修补程序进行了增强。 此外, 此版本的 SSMA for SAP ASE 提供以下修补程序:

* 解决辅助功能问题
* 在 SQL Server 中添加 "hierarchyid" 类型的基本支持

> [!IMPORTANT]
> 对于 SSMA 7.4 和更高版本, .Net 4.5.2 是必备组件。

## <a name="ssma-v82"></a>SSMA v8.2

SSMA for SAP ASE 的7.4 版已通过一组旨在提高质量和转换指标的目标修补程序进行了增强, 并为以下方面提供了修复:

* 数据迁移后已禁用的非聚集索引的问题。
* 在无提示安装期间检测 .NET Framework。
* 下载新版本时出现间歇性崩溃。

> [!NOTE]
> 自动更新的一个已知问题可能会导致从 SSMA v4.0 到 v4.0 8.2 的更新失败。 如果遇到此错误, 请下载并手动安装新版本。

> [!IMPORTANT]
> 对于 SSMA 7.4 和更高版本, .Net 4.5.2 是必备组件。

## <a name="ssma-v81"></a>SSMA v8.1

适用于 SAP ASE 的 SSMA 的7.4 版已通过旨在提高质量和转换指标的目标修补程序进行了增强。

> [!NOTE]
> 自动更新的一个已知问题可能会导致从 SSMA 8.0 到 app-v 8.1 的更新失败。 如果遇到此错误, 请下载并手动安装新版本。

## <a name="ssma-v80"></a>SSMA v8.0

SSMA for SAP ASE 的 v2.0 版本增强了目标修补程序, 旨在提高质量和转换指标。 此外, 此版本还提供以下新增功能:

* 支持作为目标**Azure SQL 数据库托管实例**。 你现在可以创建面向 Azure SQL 数据库托管实例的新项目:

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

* 转换后**修补顾问**。 [在此处](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)了解详细信息。

* 初步的数据库/架构选择。

  连接到源时, 用户现在可以选择数据库/感兴趣的架构。 仅选择你计划迁移的架构将在初始连接期间节省时间, 并提高总体 SSMA 性能。

  ![SSMA 筛选器对象](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

SSMA for SAP ASE 的 v2.0 版本增强了目标修补程序, 旨在提供额外的安全性和隐私保护以满足全局要求的变化。

## <a name="ssma-v79"></a>SSMA v7.9

SSMA for SAP ASE 的 v 7.9 版本包含以下更改:

* 改进质量和转换指标的目标修补程序。
* 支持在 SSMA 命令行中更改数据类型映射和项目首选项。
* 支持使用 SQL Server Integration Services (SSIS) 迁移数据。 转换架构后, 可以使用右键单击上下文菜单选项创建 SSIS 包。
* 还更改了 SSMA 中的 Azure SQL 数据库连接对话框以指定完全限定的服务器名称。 在以前版本的 SSMA 中, 必须在项目设置中显式提到 Azure SQL 数据库前缀。

## <a name="ssma-v78"></a>SSMA v7.8

SSMA for SAP ASE 的7.4 版版本包含以下更改:

* 更改项目设置中突出显示的类型映射。
* 允许用户禁用遥测数据。

## <a name="ssma-v77"></a>SSMA v7.7

SSMA for SAP ASE 的 v4.0 版本包含以下更改:

* SAP ASE 的 SSMA 已通过改进质量和转换指标的目标修补程序进行了增强。
* 基于常用需求, SSMA for SAP ASE 的32位版本已恢复。 与上一实现相比 (到7.4 之前), 有两个安装包, 但不能并行安装。 因此, 你必须根据你拥有的连接组件选择最适合的版本。 如果可能, 始终最好使用64位版本。

## <a name="ssma-v76"></a>SSMA v7.6

SSMA for SAP ASE 的版本7.6 版本包含以下更改:

* 目标修补程序, 可提高质量和转换指标, 并支持 SQL Server 2017 (公共预览版)。 对 Windows 和 Linux 上的 SQL Server 2017 的支持是公共预览版, 不应用于生产迁移。
* 支持 Sybase 函数的转换。

## <a name="ssma-v75"></a>SSMA v7.5

适用于 SAP ASE 的 SSMA (以前的 SSMA) 的7.5 版本包含以下更改:

* 确保为残障人士提供更好的辅助功能的多项改进。
* 支持 CREATE 或 REPLACE 语法。

## <a name="ssma-v74"></a>SSMA v7.4

用于 Sybase 的 SSMA 的7.4 版本包含以下更改:

* 在源和目标中的架构对象发现期间, 现在可以使用 "**查询超时**" 选项。

  ![query timeout 选项](../media/query-timeout_red.png)
* 根据客户的反馈, 改进了质量和转换指标。

  > [!IMPORTANT]
  > .Net 4.5.2 是安装 SSMA 7.4 的必备组件。 此外, 从7.4 版开始, 32 位版本的 SSMA 即将停止使用。  

## <a name="ssma-v73"></a>SSMA v7.3

用于 Sybase 的 SSMA 的7.3 版本包含以下更改:

* 根据客户的反馈, 改进了质量和转换指标与目标修复。
* 通过以下各项公开的 SSMA 扩展性框架:
  * 将功能导出到 SQL Server Data Tools (SSDT) 项目。
    * 你现在可以将 SSMA 中的架构脚本导出到 SSDT 项目。 您可以使用架构脚本来进行其他架构更改并部署您的数据库。

        ![另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  * 可供 SSMA 使用的库, 用于执行自定义转换。
    * 你现在可以构造代码, 该代码可以处理 SSMA 之前未处理的自定义语法转换和转换。
      * 此博客文章中提供了有关如何构造自定义转换器的说明,[扩展了 SQL Server 迁移助手的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下载此[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)中用于转换的示例项目。

## <a name="ssma-v72"></a>SSMA v7.2

用于 Sybase 的 SSMA 的7.2 版本包含以下更改:

* 根据客户的反馈, 改进了质量和转换指标与目标修复。
* 遥测增强功能可提供更好的数据点以解决客户问题并提高 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1

用于 Sybase 的 SSMA 的7.1 版本包含以下更改:

* Windows 和 Linux 上的 SQL Server 2017 现在是支持迁移的目标平台。 此功能在 technical preview 中, 支持将架构和数据移动到目标 SQL server。
* 支持自动更新, 以下载最新版本的 SSMA (如果可用)。
* SSMA 可安装二进制文件现在通过 Windows installer 包文件 (.msi) 传递。

## <a name="may-2016"></a>可能为2016

Sybase 的 SSMA 2016 版包含以下更改:  

* 添加了对 SQL Server 2016 的支持。
* 移除了 .Net 2.0 的安装程序检查。
* 更新了从 .Net 3.5 到 .Net 4.0 的扩展包。
* 修复了用于 SSMA 控制台的 "保存项目" 和 "打开项目" 命令。
* 修复了 SSMA 控制台的 "securepassword" 命令。
* 修复了初始加载的对象计数。
* 修复了全局设置中的 bug。

## <a name="march-2016"></a>2016 年 3 月

用于 Sybase 的 SSMA 的2016年3月预览版本增加了对迁移到 SQL Server 2016 的支持。  
  
## <a name="january-2016"></a>2016年1月

用于 Sybase 的 SSMA 的2016年1月维护版本包含以下更改:  
  
* 向 SSMA 添加了 "查看日志" 菜单项 (RFC 5706203)。  
* 添加了遥测。

## <a name="july-2014"></a>2014 年 7 月

SSMA 的2014年7月发行版本包含以下更改:  
  
* 改进了 Azure SQL DB 代码转换。  
* 已将扩展包功能移到架构以支持 Azure SQL DB。  
* 增加了针对具有超过10k 对象的数据库测试的性能改进。  
* 添加了用于处理大量对象的 UI 改进。  
* 添加了突出显示 "众所周知的" LOB 架构的功能 (因此可以在转换时忽略它们)。  
* 增加了转换速度改进。  
* 添加了在 UI 中显示对象计数的功能。
* 将报表大小减少 25% 以上。  
* 改进了未分析构造的错误消息。  
  
## <a name="april-2014"></a>2014年4月

用于 Sybase 的 SSMA 的2014年4月版本包含以下更改:  
  
* 添加了对 MS SQL Server 2014 的支持。  
* 修复了有关转换到 Azure 的 bug。  
* 修复了 IE 10 中不可见报表页的相关 bug。  
  
## <a name="january-2012"></a>2012年1月

用于 Sybase 的 SSMA 的2012年1月版包含以下更改:  
  
* 添加了对回滚触发器转换的支持。
* 为转换提供修复 @@ROWCOUNT 和 @@ERROR 在同一组语句。  
  
## <a name="july-2011"></a>2011年7月

SSMA 2011 年7月发行版本在数据迁移过程中提供了改进的错误报告功能。  
  
## <a name="april-2011"></a>2011年4月

用于 Sybase 的 SSMA 的2011年4月版本包含以下更改:  
  
* 合并的 "SSMA for Sybase" 产品, 支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 和 Azure SQL。  
* 添加了对连接和迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 的支持。  
* 添加了一项新功能, 可将 Sybase 数据库转换和迁移到 Azure SQL。  
* 增强了客户端数据迁移引擎, 支持并行数据迁移。  
* 通过简单和大容量日志恢复模式改进了数据迁移性能。
* 添加了正确地将区分大小写的 Sybase 数据库转换和迁移到区分大小写的 SQL Server 的功能。  
* 添加了对将 Sybase ASE 非 ANSI 联接 SQL Server 语句转换为 DELETE 和 UPDATE 语句的支持。  
* 提供了使用 Sybase ASE ODBC 提供程序和 Sybase ASE ADO.Net 提供程序连接到 Sybase ASE 服务器的其他连接选项。
* 删除了一个名为**SysDB**的独立数据库的依赖项, 该数据库包含 Sybase 模拟函数 (作为扩展包的一部分安装)。
* 添加了在群集上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装适用于 Sybase 扩展包的 SSMA 的功能。
* 添加了 SSMA 早期版本创建的项目的向后兼容性 (4.0 和 4.2)。  
* 添加了一项功能, 该功能能够安装 SSMA for Sybase v1.0 product (SxS) 与较旧版本的 SSMA (v4.0 和 4.2)。  
  
## <a name="july-2010"></a>2010年7月

添加了 Sybase 的 SSMA 2010 年7月发行版:

* 支持迁移到 SQL Server 2008 R2。  
* 用于执行命令行的新 SSMA 控制台应用程序。  
* 支持使用服务器端和客户端数据迁移引擎进行数据迁移。  
* 支持数据迁移中的 "自定义" SELECT 语句。  
* 支持从 Sybase ASE 15.0.3 和15.5 进行迁移。  
  
## <a name="june-2008"></a>2008年6月

SSMA 的2008年6月发行版包含以下更改:  
  
* 添加了 SSMA 测试器, 该测试器自动测试数据库对象转换和 SSMA 进行的数据迁移。 完成所有 SSMA 迁移步骤后, 使用 SSMA 测试人员验证转换后的对象是否以相同方式工作, 并确保所有数据都已正确传输。
* 添加了预 SQL 转换。 用户现在可以为要在转换中使用的每个源过程指定临时表 (及其他对象) 声明。
* 增加了对象转换的改进:  
  * 联接转换已修订。  
  * 聚合和非聚合, 无需按子句分组。  
  * 带有 SELECT INTO 语句的 IDENTITY 函数。  
  * 仅限数据锁定的群集约束和索引。  
  * 通过 SELECT INTO 创建的临时表。  
  * 临时表的约束/索引。  
  * 支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]新的 2008 datetime 类型。  
  * Sybase 15.0 连接和数据类型支持。  
  
## <a name="may-2007"></a>可能为2007

添加了 Sybase 的 SSMA 2007 版:  
  
* 保存项目时能够更快地加载数据库内容。  
* 在 SQL Server 格式的 SQL 模式下支持用户输入的注释。  
* 对象转换的改进。  

## <a name="november-2006"></a>2006年11月

用于 Sybase 的 SSMA 11 月2006版包含以下更改:  
  
* 添加了新的全局设置:  
  * 您可以选择在编辑器窗口中显示行号。  
  * 您可以将 SSMA 配置为提示替换重复的对象, 或者在架构转换期间始终或从不替换重复的对象。  
* 添加了新的转换选项, 使你可以配置 SSMA 处理以下情况的方式:  
  * 包含二进制字符串的强制转换或转换语句。  
  * 检查相等表达式中是否存在 null 值。  
  * 代理表。  
  * RAISERROR 的用户消息错误号。  
  * 包含未解析的标识符的 UPDATE 语句。  
* 添加了新的迁移选项, 使你可以指定 SSMA 应如何处理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期范围以外的日期。  
* 在 " **SQL** " 选项卡上添加了**格式化的 SQL**设置, 该设置将代码的格式设置为增强可读性。  
* Bug 修复, 其中包括:
  * SSMA 现在转换 {SHARED |EXCLUSIVE} MODE 语句, 方法是将 TABLOCK 或 TABLOCKX 提示添加到表的后续 SELECT 查询中。  
  * 在字符表达式中使用二进制类型时, 现在会添加必要的强制转换。  
  * 内存和性能的改进。  
  
## <a name="july-2006"></a>2006年7月

2006 年 7 月发布的用于 Sybase 的 SSMA 是初次发布。  
  
## <a name="see-also"></a>请参阅

[入门用于 Sybase &#40;SYBASETOSQL 的 SSMA&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
