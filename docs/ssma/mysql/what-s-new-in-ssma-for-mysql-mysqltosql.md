---
title: SSMA 中 MySQL （MySQLSql） 的新增功能 |微软文档
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
ms.author: jtoland;alexiva
ms.openlocfilehash: 9d5c33bbb9e09a5a833c928547a5ec659fe43c96
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625551"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL 中的新增功能 (MySQLToSql)

本文列出了每个版本中 MySQL 更改的 SQL 服务器迁移助手 （SSMA）。

## <a name="ssma-v88"></a>SSMA v8.8

适用于 MySQL 的 SSMA 的 v8.8 版本包括：

* SQL Server 对象同步稳定性改进
* 评估和转换期间的 GUI 性能改进

## <a name="ssma-v87"></a>SSMA v8.7

MySQL 的 SSMA v8.7 版本在图形用户界面中具有轻微的修复和性能改进。

此外，MySQL 的 SSMA 现在为`LIMIT`面向 Azure SQL 时提供子句的转换。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v86"></a>SSMA v8.6

除了一组旨在提高可用性和性能的有针对性的修补程序外，MySQL 的 V8.6 版本还通过添加允许用户在转换后的代码中省略 SSMA 扩展属性的设置进行了增强。

要利用此设置，在 MySQL 的 SSMA 中，导航到**工具** > **项目设置** > **常规** > **转换**，然后在**Misc**下，将 **"省略扩展属性**"设置的值更新为 **"是**"。

![省略扩展属性设置](../mysql/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v85"></a>SSMA v8.5

支持 Azure Active Directory 身份验证和对 SQL 服务器中的 JSON 功能的基本支持，以及一组旨在提高可用性和性能的有针对性的修补程序，增强了 MySQL 的 SSMA v8.5 版本。

> [!IMPORTANT]
> 使用 SSMA v8.5 时，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v84"></a>SSMA v8.4

MySQL 的 SSMA v8.4 版本通过有针对性的修补程序进行增强，这些修补程序旨在解决辅助功能问题并修复 SQL Server 2016 和更高版本的最大索引列（允许 32 而不是 16）相关的 Bug。

> [!IMPORTANT]
> 对于 SSMA 版本 7.4 但 8.4，.NET 4.5.2 是安装的先决条件。

## <a name="ssma-v83"></a>SSMA v8.3

MySQL 的 SSMA v8.3 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。 此外，此版本的 MySQL 的 SSMA 提供了以下修补程序：

* 解决辅助功能问题。
* 添加对`hierarchyid`SQL Server 类型的基本支持。

## <a name="ssma-v82"></a>SSMA v8.2

MySQL 的 SSMA v8.2 版本通过一组旨在提高质量和转换指标的有针对性的修补程序以及用于以下的修补程序进行增强：

* 数据迁移后禁用的非群集索引的问题。
* 在静默安装期间检测 .NET 框架。
* 下载新版本时发生的间歇性崩溃。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.1 到 v8.2 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v81"></a>SSMA v8.1

MySQL 的 SSMA v8.1 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.0 到 v8.1 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v80"></a>SSMA v8.0

MySQL 的 SSMA v8.0 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。 此版本还提供以下新功能：

* 支持**Azure SQL 数据库托管实例**作为目标。 现在，您可以创建针对 Azure SQL 数据库托管实例的新项目：

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

* 转换后**修复顾问**。 在此处了解有关它的更多[。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步数据库/架构选择。

  连接到源时，用户现在可以选择感兴趣的数据库/架构。 仅选择计划迁移的架构将节省时间连接期间的时间，并提高 SSMA 的整体性能。

  ![SSMA 筛选对象](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

MySQL 的 SSMA v7.10 版本包含以下更改：

* 旨在提供额外安全和隐私保护以满足全球需求变化的有针对性的修补程序。
* 函数名称和参数列表之间空间转换的修复程序。

## <a name="ssma-v79"></a>SSMA v7.9

MySQL 的 SSMA v7.9 版本包含以下更改：

* 提高质量和转化指标的针对性修复。
* 部分支持将空间数据类型从 MySQL 迁移到 Azure SQL 数据库。
* 支持 SSMA 命令行以更改数据类型映射和项目首选项。
* 支持使用 SQL 服务器集成服务 （SSIS） 迁移数据。 转换架构后，可以使用右键单击上下文菜单选项创建 SSIS 包。
* SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在 SSMA 的早期版本中，必须在项目设置中显式提及 Azure SQL 数据库前缀。

## <a name="ssma-v78"></a>SSMA v7.8

MySQL 的 SSMA v7.8 版本包含以下更改：

* 更改类型映射在项目设置中突出显示。
* 用户禁用遥测功能。

## <a name="ssma-v77"></a>SSMA v7.7

MySQL 的 SSMA v7.7 版本包含以下更改：

* MySQL 的 SSMA 已通过提高质量和转换指标的针对性修补程序进行了增强。
* 根据大众需求，MySQL 的 32 位版本的 SSMA 又回来了。 与以前的实现（在 v7.4 之前）相比，有两个安装程序包，但不能并排安装。 因此，您必须根据拥有的连接组件选择最合适的版本。 如果可能，最好使用 64 位版本。
* MySQL 的 SSMA 现在具有 ODBC 连接字符串连接模式，允许您使用与 MySQL 兼容的任何第三方 ODBC 驱动程序。

## <a name="ssma-v76"></a>SSMA v7.6

MySQL 的 SSMA v7.6 版本已通过提高质量和转换指标的针对性修补程序以及支持 SQL Server 2017（公共预览）进行了增强。 Windows 和 Linux 上对 SQL Server 2017 的支持处于公共预览版，不应用于生产迁移。

## <a name="ssma-v75"></a>SSMA v7.5

MySQL SSMA 的 v7.5 版本经过多次改进得到了增强，以确保残障人士获得更大的可访问性。

## <a name="ssma-v74"></a>SSMA v7.4

MySQL 的 SSMA v7.4 版本包含以下更改：

* **查询超时**选项现在在源和目标架构对象发现期间可用。

    ![查询超时选项](../media/query-timeout_red.png)
* 质量和转化指标已根据客户反馈通过有针对性的修复得到了改进。

> [!IMPORTANT]
> .NET 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停产。

## <a name="ssma-v73"></a>SSMA v7.3

MySQL 的 SSMA v7.3 版本包含以下更改：

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

MySQL 的 SSMA v7.2 版本包含以下更改：

* 根据客户反馈有针对性地修复，提高质量和转化指标。
* 遥测增强功能，以提供更好的数据点，以解决客户问题并提高 SSMA 的转化率。

## <a name="ssma-v71"></a>SSMA v7.1

MySQL 的 SSMA v7.1 版本包含以下更改：

* Windows 和 Linux CTP1 上的 SQL Server 2017 现在是支持迁移的目标平台。 此功能处于技术预览中，允许架构和数据移动以目标 SQL 服务器为目标。
* SSMA 现在支持自动更新，以便一旦 SSMA 可用，立即下载。
* SSMA 可安装二进制文件现在通过 Windows 安装程序包文件 （.msi） 传递。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 MySQL 的 SSMA 包含以下更改：

* 添加了对 SQL Server 2016 的支持。
* 改进的解析器和解析器。
* 已删除的安装程序检查 .NET 2.0。
* 将扩展包依赖项从 .NET 3.5 更新为 .NET 4.0。
* 修复了 MySql 的默认 BigInt 类型映射。
* SSMA 控制台的固定`save-project`和`open-project`命令。
* SSMA 控制台的固定`securepassword`命令。
* 修复了初始加载的对象计数。
* 修复了 MsSql 对象加载。
* 修复了全局设置中的 Bug。

## <a name="march-2016"></a>2016 年 3 月

MySQL 的 SSMA 预览版 2016 年 3 月增加了对迁移到 SQL Server 2016 的支持。
  
## <a name="january-2016"></a>2016 年 1 月

MySQL 的 SSMA 2016 年 1 月维护版本包含以下更改：

* 将视图日志菜单项添加到 SSMA （RFC 5706203）。
* 添加了遥测。
  
## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版本的 MySQL 的 SSMA 包含以下更改：
  
* 改进了 Azure SQL DB 代码转换。
* 扩展包功能移动到架构以支持 Azure SQL DB。
* 对具有 10k 个以上对象的数据库测试了性能改进。
* 用于处理大量对象的 UI 改进。
* 突出显示众所周知的 LOB 架构（以便在转换中忽略它们）。
* 转换速度改进。
* 在 UI 中显示对象计数。
* 报表大小缩减超过 25%。
* 改进了未解析构造的错误消息。
  
## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版本的 MySQL 的 SSMA 包含以下更改：
  
* 添加了对 SQL Server 2014 的支持。
* 修复了有关转换为 Azure 的错误。
* 修复了 IE 10 中不可见报表页的 Bug。
  
## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版本的 MySQL 的 SSMA 包含以下更改：
  
* 支持转换为`LIMIT`[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]`OFFSET`。
* 改进了数据迁移期间的错误报告。
  
## <a name="april-2011"></a>2011 年 4 月

2011 年 4 月版本的 MySQL 的 SSMA 包含以下更改：
  
* 支持 的"SSMA 表示 MySQL"的单一[!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)]可[!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]安装[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]，支持 和 Azure SQL。
* 连接[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]的能力。
* 增强的客户端数据迁移引擎，支持数据的并行迁移。
* 使用简单和批量记录恢复模型提高了数据迁移性能。
* 适用于 MySQL 控制台版本的 SSMA 支持向后兼容性。 您可以打开早期版本创建的项目 SSMA v5.0。
* MySQL v5.0 产品的 SSMA 可以与旧版本的 SSMA 产品并排安装 （SxS）。
  
## <a name="july-2010"></a>2010 年 7 月

2010 年 7 月版本的 MySQL 的 SSMA 包含以下功能：
  
**1. 用户界面的改进：**

* MySQL 数据库对象的"SQL 模式"选项卡
* MySQL 数据库对象的"设置"选项卡
* MySQL 表的"数据"选项卡
* 在转换和迁移页中更新的项目设置
* 表级别的"数据迁移设置"
  
**2. 连接到 MySQL 和 SQL 服务器的改进：**
  
* MySQL 中的 SSL 连接
* SQL 服务器中的加密连接
  
**3. MySQL 元库资源管理器的改进：**
  
* 加载所有 MySQL 数据库对象及其各自的选项卡。
  
**4. 对象转换的改进：**
  
* MySQL 元基对象的转换 - 过程、函数、视图、触发器和语句。
* 对表中空间数据类型的支持有限。
* 将 MySQL 函数转换为 SQL 服务器存储过程的选项
* 在对象转换期间应用 SQL 模式和字符集映射的选项
  
**5. 数据迁移的改进：**  
  
* 使用服务器端和客户端数据迁移引擎支持数据迁移
* 支持空间数据迁移
* 用于表数据迁移的自定义 SQL
  
**6. MySQL 控制台的 SSMA：**  
  
* 支持适用于 MySQL 的 SSMA 的控制台功能  
* 支持脚本级接口  
  
## <a name="january-2010"></a>2010年1月

2010 年 1 月版本的 MySQL SSMA 是初始版本。 它包含以下功能：
  
* 添加了对本地 SQL 服务器和 Azure SQL 迁移的支持。  
  
* **功能快照：** MySQL 表/索引/约束的架构和数据迁移。
