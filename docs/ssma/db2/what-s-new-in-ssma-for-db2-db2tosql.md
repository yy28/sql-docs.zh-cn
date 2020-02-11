---
title: SSMA for DB2 中的新增功能（DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/22/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 9b4fc1f9d0ce1128306f27a5f7bf6658377528cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "76516559"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>SSMA for DB2 中的新增功能（DB2ToSQL）

本文列出了每个版本中的 DB2 更改 SQL Server 迁移助手（SSMA）。

## <a name="ssma-v86"></a>SSMA v 8。6

除了旨在提高可用性和性能的目标修补集外，通过添加使用户能够在转换后的代码中省略 SSMA 扩展属性的设置，还增强了 SSMA for DB2 的 v 8.6 版本。

若要利用此设置，请在 SSMA for DB2 中导航到 "**工具** > " "**项目设置** > " "**常规** > **转换**"，然后在 "**杂项**" 下，将 "**省略扩展属性**" 设置的值更新为 **"是"**。

![省略扩展属性设置](../db2/media/ssma-omit-extended-properties.png)

此外，SSMA for DB2 现在提供：

-   用于转换使用默认参数值的函数的修复
-   改进了参数子句中函数的分析。
- 转换 LEAVE 语句的能力。

> [!IMPORTANT]
> 对于 SSMA 的8.5 和更高版本，.Net 4.7.2 是必备组件。 如果需要安装此版本，可以从[此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v85"></a>SSMA 8。5

通过对 SQL server 中的 JSON 功能 Azure Active Directory authentication 和 basic 支持以及旨在提高可用性和性能的目标修补程序集，增强了用于 DB2 的 SSMA 的版本8.5。

此外，SSMA for DB2 已通过以下方式增强：

* 支持添加带 ROW_NUMBER 的 GET 诊断语句的转换。
* 修复了与对象名称开头处空格相关的错误。

> [!IMPORTANT]
> 对于 SSMA 的8.5，.Net 4.7.2 是必备组件。 如果需要安装此版本，可以从[此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v84"></a>SSMA v2。0

SSMA for DB2 的 v2.0 版本使用旨在解决辅助功能问题的目标修补程序进行了增强，并修复了与 SQL Server 2016 及更高版本的最大索引列（32而不是16）相关的 bug。

> [!IMPORTANT]
> 对于 SSMA 版本7.4，8.4，.Net 4.5.2 是必备组件。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for DB2 的 v 8.3 版本通过旨在改进质量和转换指标的目标修补程序进行了增强。 此外，此版本的 SSMA for DB2 还提供了以下修补程序：

* 解决辅助功能问题
* 在 SQL Server 中添加 "hierarchyid" 类型的基本支持
* 在 z/OS 发现查询中使用 RTRIM/LTRIM 替换 TRIM 函数使用情况
* 允许用户在以 "标准模式" （默认为 NULLID）连接时指定包集合
* 添加 CREATE TABLE 的转换为 SELECT
* 改进全局临时表的转换
* 解决对象唯一检查顺序的问题，以便在名称发生冲突的情况下为表设置优先级
* 解决加载 z/OS 日期和时间戳的默认列值的问题
* 支持 Unicode 换行字符（也称为 NEL）
* 解决与缺少返回到子句的游标转换有关的问题
* 添加对标签和 GOTO 的支持

## <a name="ssma-v82"></a>SSMA

的 SSMA for DB2 的7.4 版已通过 SSMA 控制台工具解决了与 Azure SQL 数据库连接有关的问题，并且在转换过程中缺少视图声明中的 COUNT_BIG 列。 此外，此版本还包括一组旨在提高质量和转换指标的目标修补程序，以及对的修复：

* 数据迁移后已禁用的非聚集索引的问题。
* 在无提示安装期间检测 .NET Framework。
* 下载新版本时出现间歇性崩溃。

> [!NOTE]
> 自动更新的一个已知问题可能会导致从 SSMA v4.0 到 v4.0 8.2 的更新失败。 如果遇到此错误，请下载并手动安装新版本。

## <a name="ssma-v81"></a>SSMA 8。1

SSMA for DB2 的 "7.4 版" 版本得到了增强，可提供旨在提高质量和转换指标的目标修补程序。

> [!NOTE]
> 自动更新的一个已知问题可能会导致从 SSMA 8.0 到 app-v 8.1 的更新失败。 如果遇到此错误，请下载并手动安装新版本。

## <a name="ssma-v80"></a>SSMA 8。0

SSMA for DB2 的 v2.0 版本得到了增强，可提供旨在提高质量和转换指标的目标修补程序。 此版本还提供以下新增功能：

* 支持作为目标**Azure SQL 数据库托管实例**。 你现在可以创建面向 Azure SQL 数据库托管实例的新项目：

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

* 转换后**修补顾问**。 [在此处](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)了解详细信息。

* 初步的数据库/架构选择。

  连接到源时，用户现在可以选择数据库/感兴趣的架构。 仅选择你计划迁移的架构将在初始连接期间节省时间，并提高总体 SSMA 性能。

  ![SSMA 筛选器对象](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA

用于 DB2 的 SSMA 的版本7.10 版本包含以下更改：

* 旨在提供附加安全和隐私保护以满足全局要求更改的目标修补程序。
* 用于转换 BEGIN 结束块的修补程序。

## <a name="ssma-v79"></a>SSMA v 7。9

适用于 DB2 的 SSMA 的 v 7.9 版本包含以下更改：

* 改进质量和转换指标的目标修补程序。
* 支持在 SSMA 命令行中更改数据类型映射和项目首选项。
* 支持使用 SQL Server Integration Services （SSIS）迁移数据。 转换架构后，可以使用右键单击上下文菜单选项创建 SSIS 包。
* 还更改了 SSMA 中的 Azure SQL 数据库连接对话框以指定完全限定的服务器名称。 在以前版本的 SSMA 中，必须在项目设置中显式提到 Azure SQL 数据库前缀。

## <a name="ssma-v78"></a>SSMA v 7。8

适用于 DB2 的 SSMA 的版本7.8 版本包含以下更改：

* 更改项目设置中突出显示的类型映射。
* 允许用户禁用遥测数据。

## <a name="ssma-v77"></a>SSMA v4。0

用于 DB2 的 SSMA 的 v4.0 版本包含以下更改：

* 改进质量和转换指标的目标修补程序。
* 基于常用需求，SSMA for DB2 的32位版本已恢复。 与之前的实现（在7.4 之前）相比，有两个安装包，但不能并行安装。 因此，你必须根据你拥有的连接组件选择最适合的版本。 如果可能，始终最好使用64位版本。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for DB2 的版本7.6 版本增强了目标修补程序，可改进质量和转换指标，并支持 SQL Server 2017 （公共预览版）。 对 Windows 和 Linux 上的 SQL Server 2017 的支持是公共预览版，不应用于生产迁移。

## <a name="ssma-v75"></a>SSMA 7。5

SSMA for DB2 的版本7.5 版本增强了几项改进，以确保为残障人士提供更好的辅助功能。

## <a name="ssma-v74"></a>SSMA 7。4

用于 DB2 的 SSMA 的7.4 版本包含以下更改：

* 在源和目标中的架构对象发现期间，现在可以使用 "**查询超时**" 选项。

  ![query timeout 选项](../media/query-timeout_red.png)

* 根据客户的反馈，改进了质量和转换指标。

  > [!IMPORTANT]
  > .Net 4.5.2 是安装 SSMA 7.4 的必备组件。 此外，从7.4 版开始，32位版本的 SSMA 已不再使用。

## <a name="ssma-v73"></a>SSMA 7。3

适用于 DB2 的 SSMA 的7.3 版本包含以下更改：

* 根据客户的反馈，改进了质量和转换指标与目标修复。
* 通过以下各项公开的 SSMA 扩展性框架：
  * 将功能导出到 SQL Server Data Tools （SSDT）项目。
    * 你现在可以将 SSMA 中的架构脚本导出到 SSDT 项目。 您可以使用架构脚本来进行其他架构更改并部署您的数据库。

      ![另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  * 可供 SSMA 使用的库，用于执行自定义转换。
    * 你现在可以构造代码，该代码可以处理 SSMA 之前未处理的自定义语法转换和转换。
      * 此博客文章中提供了有关如何构造自定义转换器的说明，[扩展了 SQL Server 迁移助手的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下载此[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)中用于转换的示例项目。

## <a name="ssma-v72"></a>SSMA 7。2

SSMA for DB2 的 v2.0 版本包含以下更改：

* 根据客户的反馈，改进了质量和转换指标与目标修复。
* 遥测增强功能可提供更好的数据点以解决客户问题并提高 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA 7。1

适用于 DB2 的 SSMA 7.1 版本包含以下更改：

* Windows 和 Linux 上的 SQL Server 2017 现在是支持迁移的目标平台。 此功能在 technical preview 中，允许将架构和数据移动到目标 SQL server。
* 支持自动更新，以下载最新版本的 SSMA （如果可用）。
* SSMA 可安装二进制文件现在通过 Windows Installer 包文件（.msi）传递。

## <a name="may-2016"></a>2016 年 5 月

DB2 的 SSMA 2016 版包含以下更改：  

* 添加了对 SQL Server 2016 的支持。
* 添加了 DB2 内存中和常规表的转换，以便 SQL Server 内存中和 hekaton 的功能。
* 添加了 DB2 访问控制到 SQL Server 策略对象的转换（用于 DB2 的行级别安全性）。
* 添加了 DB2 系统版本控制表到 SQL Server 临时表的转换。
* 改进了 DB2 分析器和解析程序。
* 移除了 .Net 2.0 的安装程序检查。
* 已从 Db2 安装程序中删除不必要的 * .dll。
* 修复了用于 SSMA 控制台的 "保存项目" 和 "打开项目" 命令。
* 修复了 SSMA 控制台的 "securepassword" 命令。
* 修复了初始加载的对象计数。
* 修复了全局设置中的 bug。
  
## <a name="march-2016"></a>2016 年 3 月

SSMA 的2016年3月预览版本增加了对迁移到 SQL Server 2016 的支持。

## <a name="january-2016"></a>2016 年 1 月

SSMA 的2016年1月维护版本包含以下更改：  
  
* 添加了对许多标准函数的支持。  
* 修复了 DB2 分析器错误。  
* 修复了 DB2 v9.x zOS 支持（RFC 5690920）。  
* 修复了转换期间的 DB2 未解决标识符错误。  
* 向 SSMA 添加了 "查看日志" 菜单项（RFC 5706203）。  
* 添加了遥测。
  
## <a name="november-2014"></a>2014 年 11 月

用于 DB2 的 SSMA 11 月2014版是初始版本。
