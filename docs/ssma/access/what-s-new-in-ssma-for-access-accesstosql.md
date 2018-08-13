---
title: 什么是适用于 Access(AccessToSQL) SSMA 中的新增功能 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/05/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
caps.latest.revision: 37
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: eabb6b1364b36a84da8acd4f70fe82f962b31081
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556587"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>什么是 SSMA for Access (AccessToSQL) 中的新增功能
本主题列出了每个版本中的访问权限更改 SSMA。  

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for Access v7.7 版本包含以下更改：
- 适用于 Access 的 SSMA 已得到增强改进质量和转换的度量值的目标修补。
- SSMA for Access 的 32 位版本是返回基于普遍的需求。 与以前的实现 （之前 v7.4) 相比，有两个安装程序软件包，但不能并行安装。 因此，必须选择最适合您的版本根据连接组件。 最好始终使用 64 位版本中，在可能的情况。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for Access v7.6 版本已得到增强，提高质量和转换的度量值的目标修补和支持 SQL Server 2017 （公共预览版）。 对 Windows 和 Linux 上的 SQL Server 2017 的支持处于公共预览状态，并不用于生产的迁移。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 的安装先决条件，并已停止使用该工具的 32 位版本。

## <a name="ssma-v75"></a>SSMA 版本 7.5
SSMA for Access 的版本 7.5 版本已得到增强了一些改进，以确保为残障人士使用的可访问性。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA 版本 7.5 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Access v7.4 版本包含以下更改：
- **查询超时值**选项现可在源和目标架构对象发现期间访问。
![query timeout 选项](../media/query-timeout_red.png)

- 有所改进质量和转换指标，包括目标修补，根据客户反馈。

> [!IMPORTANT]
> .Net 4.5.2 是用于安装 SSMA v7.4 必备组件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停止。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Access v7.3 版本包含以下更改：
- 改进的质量和转换度量值与目标修补，根据客户反馈。
- 通过以下各项公开的 SSMA 可扩展性框架：
  - 导出到 SQL Server Data Tools (SSDT) 项目的功能。
    -   现在，您可以到 SSDT 项目从 SSMA 导出架构脚本。 架构脚本可用于进行附加的架构更改和部署你的数据库。
![将另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)

  - 可供执行的自定义转换 SSMA 的库。
    - 现在可以构造自定义语法转换和转换之前未处理的 SSMA 能处理的代码。
      - 在此博客文章提供了有关如何构造自定义转换器说明[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 用于转换的示例项目可以下载这[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA 7.2 版
SSMA for Access 7.2 版版本包含以下更改：
- 改进的质量和转换度量值与目标修补，根据客户反馈。
- 遥测数据增强功能提供更好的数据点来解决客户问题并提高 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access v7.1 版本包含以下更改：
- SQL Server 2017 的 Windows 和 Linux CTP1 现在是用于迁移的支持的目标平台。 此功能在 technical preview 中，支持架构和数据移动到目标 SQL 服务器。
- SSMA 现在支持自动更新，以下载最新版本的 SSMA 立即可用。
- SSMA 可安装二进制文件现在被通过 Windows installer 包文件 (.msi)。

**资源**

[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>2016 年 5 月  
SSMA for Access 的 2016 年 5 月版本包含以下更改：  
  
-  添加了对 SQL Server 2016 的官方支持
-  删除.Net 2.0 的安装程序检查。
-  修复了"保存项目"和 SSMA 控制台的"打开项目"命令。
-  SSMA 控制台中的固定"securepassword"命令。
-  修复了初始加载的对象的计数。
-  固定表的数据加载 UI 选项卡进行访问。
-  全局设置中修复了 bug。 
   
## <a name="march-2016"></a>2016 年 3 月  
SSMA for Access 的 2016 年 3 月预览版本包含以下更改：  
  
-  添加了对迁移到 SQL Server 2016 的支持。  
   
## <a name="january-2016"></a>2016 年 1 月  
SSMA for Access 的 2016 年 1 月维护版本包含以下更改：  
  
-  默认值为 GUID 字段 (RFC 3894811) 的修复无效函数。  
-  导入到 SQL 数据库 (Azure) (RFC 4919573) 记录的固定的挂起。  
-  SSMA (RFC 5706203) 添加了的视图日志菜单项。  
-  添加了遥测数据。  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for Access 的 2014 年 7 月版本包含以下更改：  
  
-   改进了的 Azure SQL DB 代码转换。  
-   移动到架构以支持 Azure SQL DB 扩展包功能。  
-   对于超过 10 万个对象的数据库的已测试的性能改进。  
-   添加了的大量对象处理的 UI 改进。  
-   添加了的对突出显示的"已知"LOB 架构 （因此也可以在转换过程中忽略）。  
-   添加转换速度改进。
-   添加了对显示对象支持对用户界面中进行计数。
-   降低的报表大小的 25%以上。
-   未分析的构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for Access 的 2014 年 4 月版本包含以下更改：  
  
-   MS SQL Server 2014 添加了的支持。  
-   有关转换到 Azure 的已修复的 bug。  
-   有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
SSMA for Access 的 2012 年 1 月版本包含以下更改：  
  
-   提供的选项以在迁移之后，MS Access 链接表不保留用户名和密码。  
-   设置为 No Action 的循环引用级联操作。  
-   提供正确的消息级联操作的循环引用，该值指示已设置为 No Action。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for Access 的 2011 年 7 月版本包含以下更改：  
  
-   改进了的错误报告数据迁移过程。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for Access 的 2011 年 4 月版本包含以下更改：  
  
-   添加可安装的"SSMA 为访问"，它支持的单个[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"和 Azure SQL。  
-   添加连接的能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   用于访问控制台版本添加了的 SSMA 支持向后兼容性。 您可以打开到 SSMA 5.0 版之前的版本所创建的项目。
-   添加了使用较旧版本的 SSMA 产品安装 SSMA 5.0 版产品并排 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for Access 2010 年 7 月版本包含以下更改：  
  
-   添加了对迁移到 SQL Server 2008 R2 和 Azure SQL 的支持。
-   添加安全连接到 SQL Server 和 Azure SQL。  
-   添加了的对 Access 2010 数据库。
-   添加新命令行执行的 SSMA 控制台应用程序。
-   添加了的对 SQL Server DateTime2 数据类型。
  
## <a name="june-2008"></a>2008 年 6 月  
SSMA for Access 的 2008 年 6 月版本包含以下更改：  
  
-   添加了的对 Access 2007 数据库。  
  
## <a name="may-2007"></a>2007 年 5 月  
SSMA for Access 2007 年 5 月版本包含以下更改：  
  
-   添加了的对使用工作组策略的 Access 数据库。  
-   提供的功能从 SQL Server 元数据资源管理器中删除已转换的对象。  
-   添加了的对 SQL Server 中的用户输入注释格式 SQL 模式。  
-   添加了对象转换中的改进。  
  
## <a name="november-2006"></a>2006 年 11 月  
SSMA for Access 的 2006 年 11 月版本包含以下更改：  
  
-   添加新的数据库迁移向导可指导您完成单个数据库的迁移从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
-   添加新的 Convert，负载，并将转换 Access 数据库的迁移命令加载到已转换的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并将迁移到数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]全部在一个步骤中。  
-   改进了的查询迁移。 现在将更多选择到视图的查询，请查询迁移。 有关详细信息，请参阅[转换访问数据库对象](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)。  
-   添加了在编辑表和索引属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**表**选项卡。  
-   添加新的全局设置：  
    -   您可以选择在编辑器窗口中显示行号。  
    -   你可以配置 SSMA 提示以替换重复的对象，或始终或永远不会将重复的对象为架构转换过程。  
-   添加新的转换选项，可以指定当一个复杂的查询包含通配符时，SSMA 是否显示警告。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月发布的适用于 Access 的 SSMA 是初次发布。
