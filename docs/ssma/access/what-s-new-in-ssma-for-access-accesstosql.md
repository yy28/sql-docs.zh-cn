---
title: SSMA 中用于访问的新增功能 （访问到SQL） |微软文档
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: jtoland;alexiva
ms.openlocfilehash: 2fd3da31e6a635a65f3d2a2f75320dd0586159d9
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625585"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>SSMA 中用于访问的新增功能（访问到SQL）

本文列出了 SQL Server 迁移助手 （SSMA） 用于每个版本中的访问更改。

## <a name="ssma-v88"></a>SSMA v8.8

用于访问的 SSMA 的 v8.8 版本包括：

* SQL Server 对象同步稳定性改进
* 评估和转换期间的 GUI 性能改进
* 全新访问语法解析器，进一步提高转换性能

## <a name="ssma-v87"></a>SSMA v8.7

SSMA 的 v8.7 版本改进了查询中`IIF`功能的转换，以及图形用户界面中的一些小修复和性能改进。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v86"></a>SSMA v8.6

除了一组旨在提高可用性和性能的有针对性的修补程序外，通过添加允许用户在转换后的代码中省略 SSMA 扩展属性的设置，还增强了 SSMA 访问版本的 v8.6 版本。

要利用此设置，在 SSMA 中访问，导航到 **"工具** > **项目设置** > **常规** > **转换**"，然后在**Misc**下，将 **"Omit 扩展属性**"设置的值更新为 **"是**"。

![省略扩展属性设置](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v85"></a>SSMA v8.5

通过支持 Azure Active Directory 身份验证和 SQL 服务器中对 JSON 功能的基本支持，以及旨在提高可用性和性能的一组有针对性的修补程序，SSMA 的 v8.5 版本得到了增强。

此外，SSMA 访问现在支持转换多个标准函数 （`ISNULL`等）。 `IIF`

> [!IMPORTANT]
> 使用 SSMA v8.5 时，.NET 4.7.2 是安装的先决条件。 如果需要安装此版本，可以[在此处](https://dotnet.microsoft.com/download/dotnet-framework/net472)下载运行时文件。

## <a name="ssma-v84"></a>SSMA v8.4

SSMA 的 v8.4 版本通过有针对性的修补程序进行增强，这些修补程序旨在解决辅助功能问题并修复 SQL Server 2016 和更高版本的最大索引列（允许 32 而不是 16）相关的 Bug。

> [!IMPORTANT]
> 对于 SSMA 版本 7.4 但 8.4，.NET 4.5.2 是安装的先决条件。

## <a name="ssma-v83"></a>SSMA v8.3

SSMA 的 v8.3 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。 此外，此版本的 SSMA 用于访问提供了以下修补程序：

* 解决辅助功能问题。
* 添加对`hierarchyid`SQL Server 类型的基本支持。

## <a name="ssma-v82"></a>SSMA v8.2

SSMA 的 v8.2 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.1 到 v8.2 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v81"></a>SSMA v8.1

SSMA 的 v8.1 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。

> [!NOTE]
> 自动更新的已知问题可能会导致从 SSMA v8.0 到 v8.1 的更新失败。 如果您遇到此错误，请下载新版本并手动安装。

## <a name="ssma-v80"></a>SSMA v8.0

SSMA 面向访问的 v8.0 版本通过旨在提高质量和转换指标的有针对性的修补程序进行增强。 此版本还提供以下新功能：

* 支持**Azure SQL 数据库托管实例**作为目标。 现在，您可以创建针对 Azure SQL 数据库托管实例的新项目：

  ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

* 转换后**修复顾问**。 在此处了解有关它的更多[。](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733)

* 初步数据库/架构选择。

    连接到源时，用户现在可以选择感兴趣的数据库/架构。 仅选择计划迁移的架构将节省时间连接期间的时间，并提高 SSMA 的整体性能。

   ![SSMA 筛选对象](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

SSMA 的 v7.10 版本通过有针对性的修补程序进行了增强，旨在提供额外的安全和隐私保护，以满足全球需求的变化。

## <a name="ssma-v79"></a>SSMA v7.9

SSMA 的 v7.9 版本包含以下更改：

* 提高质量和转化指标的针对性修复。
* 支持 SSMA 命令行以更改数据类型映射和项目首选项。
* SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在 SSMA 的早期版本中，必须在项目设置中显式提及 Azure SQL 数据库前缀。

## <a name="ssma-v78"></a>SSMA v7.8

SSMA 的 v7.8 版本包含以下更改：

* 更改类型映射在项目设置中突出显示。
* 用户禁用遥测功能。

## <a name="ssma-v77"></a>SSMA v7.7

SSMA 的 v7.7 版本包含以下更改：

* 提高质量和转化指标的针对性修复。
* 根据大众需求，32 位版本的 SSMA 表示访问。 与以前的实现（在 v7.4 之前）相比，有两个安装程序包，但不能并排安装。 因此，您必须根据拥有的连接组件选择最合适的版本。 如果可能，最好使用 64 位版本。

## <a name="ssma-v76"></a>SSMA v7.6

SSMA 的 v7.6 版本通过提高质量和转换指标的针对性修补程序以及支持 SQL Server 2017（公共预览）来增强。 Windows 和 Linux 上对 SQL Server 2017 的支持处于公共预览版，不应用于生产迁移。

## <a name="ssma-v75"></a>SSMA v7.5

通过多项改进，增强了 SSMA 的 v7.5 版本，以确保残疾人获得更大的可访问性。

## <a name="ssma-v74"></a>SSMA v7.4

SSMA 的 v7.4 版本包含以下更改：

* **查询超时**选项现在在源和目标架构对象发现期间可用。

  ![查询超时选项](../media/query-timeout_red.png)

* 质量和转化指标已根据客户反馈通过有针对性的修复得到了改进。

  > [!IMPORTANT]
  > .NET 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本已停产。

## <a name="ssma-v73"></a>SSMA v7.3

SSMA 的 v7.3 版本包含以下更改：

* 根据客户反馈有针对性地修复，提高质量和转化指标。
* 通过以下项目公开的 SSMA 可扩展性框架：
  * 将功能导出到 SQL 服务器数据工具 （SSDT） 项目。
    * 现在，您可以将架构脚本从 SSMA 导出到 SSDT 项目。 您可以使用架构脚本进行其他架构更改并部署数据库。

        ![另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  * SSMA 可使用用于执行自定义转换的库。
    * 现在，您可以构造可以处理 SSMA 以前未处理的自定义语法转换和转换的代码。
      * 有关如何构造自定义转换器的说明以及用于转换的示例项目，可在博客文章["扩展 SQL Server 迁移助手的转换功能](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181)"中提供。

## <a name="ssma-v72"></a>SSMA v7.2

SSMA 的 v7.2 版本包含以下更改：

* 根据客户反馈有针对性地修复，提高质量和转化指标。
* 遥测增强功能，以提供更好的数据点，以解决客户问题并提高 SSMA 的转化率。

## <a name="ssma-v71"></a>SSMA v7.1

SSMA 的 v7.1 版本包含以下更改：

* Windows 和 Linux CTP1 上的 SQL Server 2017 现在是支持迁移的目标平台。 此功能处于技术预览中，支持针对 SQL 服务器的架构和数据移动。
* SSMA 现在支持自动更新，以便一旦 SSMA 可用，立即下载。
* SSMA 可安装二进制文件现在通过 Windows 安装程序包文件 （.msi） 传递。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 SSMA 访问包含以下更改：

* 添加了对 SQL Server 2016 的官方支持。
* 已删除的安装程序检查 .NET 2.0。
* SSMA 控制台的固定`save-project`和`open-project`命令。
* SSMA 控制台的固定`securepassword`命令。
* 修复了初始加载的对象计数。
* 修复了用于访问 UI 选项卡的表数据加载。
* 修复了全局设置中的 Bug。

## <a name="march-2016"></a>2016 年 3 月

2016 年 3 月用于访问的 SSMA 预览版增加了对迁移到 SQL Server 2016 的支持。

## <a name="january-2016"></a>2016 年 1 月

SSMA 的 2016 年 1 月维护版本包含以下更改：

* 修复了 GUID 字段默认值（RFC 3894811）的无效函数。
* 修复了将记录导入到 SQL 数据库 （Azure） （RFC 4919573） 上的挂起。
* 将视图日志菜单项添加到 SSMA （RFC 5706203）。
* 添加了遥测。

## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版本的 SSMA 访问包含以下更改：

* 改进了 Azure SQL DB 代码转换。
* 将扩展包功能移动到架构以支持 Azure SQL DB。
* 测试了具有 10k 个对象数据库的性能改进。
* 添加了用于处理大量对象的 UI 改进。
* 添加了对突出显示"众所周知"LOB 架构的支持（以便在转换中可以忽略它们）。
* 添加了转换速度改进。
* 添加了对在 UI 中显示对象计数的支持。
* 报表大小减少 25% 以上。
* 改进了未解析构造的错误消息。

## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版本的 SSMA 访问包含以下更改：

* 添加了对 MS SQL Server 2014 的支持。
* 修复了与转换为 Azure 相关的 Bug。
* 修复了 IE 10 中与不可见报表页相关的 Bug。

## <a name="january-2012"></a>2012 年 1 月

2012 年 1 月版本的 SSMA 用于访问包含以下更改：

* 提供了在迁移后不保留 MS Access 链接表的用户名和密码的选项。
* 为循环引用设置为"无操作"设置级联操作。
* 提供的正确消息，指示循环引用的级联操作已设置为"无操作"。

## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版本的 SSMA 用于访问增加了数据迁移期间改进的错误报告。

## <a name="april-2011"></a>2011 年 4 月

2011 年 4 月版本的 SSMA 用于访问包含以下更改：

* 添加了"SSMA 用于访问"的单一可安装，该安装[!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)]支持[!INCLUDE [ssSQL10](../../includes/sssql10-md.md)][!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]和 。
* 添加了连接到[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]的功能。
* 添加了用于访问控制台版本的 SSMA，支持向后兼容性。 您可以打开早期版本创建的项目 SSMA v5.0。
* 添加了使用旧版本的 SSMA 产品并排安装 SSMA v5.0 产品 （SxS） 的能力。

## <a name="july-2010"></a>2010 年 7 月

2010 年 7 月版本的 SSMA 表示访问包含以下更改：

* 添加了对迁移到 SQL Server 2008 R2 和 Azure SQL 的支持。
* 向 SQL 服务器和 Azure SQL 添加了安全连接。
* 添加了对 Access 2010 数据库的支持。
* 添加了用于命令行执行的新 SSMA 控制台应用程序。
* 添加了对 SQL Server`DateTime2`数据类型的支持。

## <a name="june-2008"></a>2008 年 6 月

2008 年 6 月版本的 SSMA 访问增加了对 Access 2007 数据库的支持。

## <a name="may-2007"></a>2007 年 5 月

2007 年 5 月版本的 SSMA 用于访问包含以下更改：

* 添加了对使用工作组策略的 Access 数据库的支持。
* 提供了从 SQL Server 元数据资源管理器中删除转换对象的功能。
* 在 SQL Server 格式化的 SQL 模式下添加了对用户输入的注释的支持。
* 添加了对象转换的改进。

## <a name="november-2006"></a>2006年11月

2006 年 11 月版本的 SSMA 用于访问包含以下更改：

* 添加了新的数据库迁移向导，用于指导您完成单个数据库从 Access 迁移到[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]的迁移过程。
* 添加了新的"转换、加载"和"迁移"命令，该命令将 Access 数据库转换[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]、将转换的对象加载到[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]中，并在一个步骤中将数据迁移到所有。
* 改进了查询迁移。 查询迁移现在将更多 SELECT 查询转换为视图。 有关详细信息，请参阅[转换访问数据库对象](converting-access-database-objects-accesstosql.md)。
* 添加了在[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]**"表"** 选项卡上编辑表和索引属性的能力。
* 添加了新的全局设置：
  * 您可以选择在编辑器窗口中显示行号。
  * 您可以将 SSMA 配置为提示替换重复的对象，或者始终或从不在架构转换期间替换重复的对象。
* 添加了一个新的转换选项，用于指定当复杂查询包含通配符时 SSMA 是否显示警告。

## <a name="july-2006"></a>2006年7月

2006 年 7 月版本的 SSMA 用于访问是初始版本。
