---
title: SSMA for Access(AccessToSQL) 的新增功能 |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
ms.custom: ''
ms.date: 03/01/2018
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
ms.openlocfilehash: cdd8f3f3898dcfd2f3233132ba7ecb4ea7861ab3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>SSMA for Access (AccessToSQL) 的新增功能
本主题列出每个版本中的访问权限更改 SSMA。  

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for Access 的 v7.7 版本包含以下更改：
- 访问的 SSMA 已得到增强提高质量和转换的度量值的目标修补程序。
- SSMA for Access 的 32 位版本基于普遍需求，已恢复。 与以前的实现 （之前 v7.4) 相比，有两个安装包，但它们不能并行安装。 因此，你必须选择最适合您的版本基于连接组件。 最好始终使用 64 位版本，如有可能。

> [!IMPORTANT]
> SSMA v7.4 和更高版本，.Net 4.5.2 是安装先决条件。

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for Access 的 v7.6 版本已得到增强，具有提高质量和转换的度量值的目标修补程序和 SQL Server 2017 （公共预览版） 支持。 对于 Windows 和 Linux 上的 SQL Server 2017 支持是在公共预览版中并不用于生产迁移。

> [!IMPORTANT]
> SSMA v7.4 和更高版本，.Net 4.5.2 的目标是安装先决条件，并已停止使用该工具的 32 位版本。

## <a name="ssma-v75"></a>SSMA v7.5 还是
SSMA for Access 的 v7.5 还是版本已得到增强几项改进，确保残障人士更大的可访问性。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.5 还是的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Access 的 v7.4 版本包含以下更改：
- **查询超时值**选项现已可用在源和目标架构对象发现期间。
![query timeout 选项](../media/query-timeout_red.png)

- 通过目标修补程序，根据客户反馈，改进了的质量和转换的度量值。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Access 的 v7.3 版本包含以下更改：
- 改进的质量和转换度量值根据客户反馈的目标修补程序。
- SSMA 扩展性框架公开通过以下各项：
  - 导出到 SQL Server Data Tools (SSDT) 项目的功能。
    -   你现在可以将架构脚本从 SSMA 导出到 SSDT 项目。 可以使用架构脚本进行其他架构更改和部署你的数据库。
![将另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)

  - 可用于执行自定义转换供 SSMA 的库。
    - 你现在可以构造自定义的语法转换和先前未由 SSMA 处理的转换可以处理的代码。
      - 在此博客文章中，提供了有关如何构造的自定义转换器说明[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 用于转换的示例项目可以下载这个[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA 7.2 版
SSMA for Access 的 7.2 版版本包含以下更改：
- 改进的质量和转换度量值根据客户反馈的目标修补程序。
- 遥测功能增强以提供更好的数据点，以解决客户问题和改进 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access 的 v7.1 版本包含以下更改：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 现在是一个用于迁移的支持的目标平台。 此功能在技术预览中，并支持架构和数据移动到目标 SQL 服务器。
- SSMA 现在支持自动更新，以下载最新版本的 SSMA，只要可用。
- SSMA 可安装二进制文件现在被通过 Windows installer 包文件 (.msi)。

**资源**

[将 SQL Server Migration Assistant 的转换功能扩展](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>2016 年 5 月  
SSMA for Access 的 2016 年 5 月版本包含以下更改：  
  
-  添加了对 SQL Server 2016 正式支持
-  删除安装程序检查 for.Net 2.0。
-  "保存项目"固定和 SSMA 控制台的"打开项目"命令。
-  SSMA 控制台的固定"securepassword"命令。
-  固定的初始加载的对象计数。
-  固定的表数据的加载 UI 选项卡的访问。
-  全局设置中的已修复的 bug。 
   
## <a name="march-2016"></a>2016 年 3 月  
SSMA for Access 的 2016 年 3 月预览版本包含以下更改：  
  
-  添加了对迁移到 SQL Server 2016 的支持。  
   
## <a name="january-2016"></a>2016 年 1 月  
SSMA for Access 的 2016 年 1 月维护版本包含以下更改：  
  
-  默认值为 GUID 字段 (RFC 3894811) 的固定无效函数。  
-  将记录导入到 SQL Database (Azure) (RFC 4919573) 的固定的挂起。  
-  添加的视图日志菜单项的 SSMA (文档 RFC 5706203)。  
-  添加的遥测。  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for Access 的 2014 年 7 月版本包含以下更改：  
  
-   改进的 Azure SQL DB 代码转换。  
-   移动到架构以支持 Azure SQL DB 扩展包功能。  
-   具有超过 10 万个对象的数据库的经过测试的性能改进。  
-   添加了对具有大量对象的处理 UI 改进。  
-   添加了对突出显示的"已知"LOB 架构 （以便它们可以在转换中被忽略） 的支持。  
-   添加的转换速度得到了改进。
-   添加了对显示对象支持对用户界面中进行计数。
-   降低的报表大小超过 25%。
-   未分析构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for Access 的 2014 年 4 月版本包含以下更改：  
  
-   添加了对 MS SQL Server 2014 的支持。  
-   有关转换到 Azure 的已修复的 bug。  
-   有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
SSMA for Access 的 2012 年 1 月版本包含以下更改：  
  
-   提供的选项不会保留用户名和密码在迁移之后，MS 访问链接表。  
-   设置为 No Action 的循环引用的级联操作。  
-   提供正确的消息，指出循环引用的级联操作已设置为 No Action。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for Access 的 2011 年 7 月版本包含以下更改：  
  
-   改进了的错误报告数据迁移过程。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for Access 的 2011 年 4 月版本包含以下更改：  
  
-   添加单个"SSMA 的访问"，它支持的可安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"和 Azure SQL。  
-   添加连接的能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   有关访问控制台版本添加的 SSMA 支持向后兼容性。 你可以打开到 SSMA 5.0 版之前的版本创建的项目。
-   添加与旧版本的 SSMA 产品安装 SSMA 5.0 版产品并行 (SxS) 的功能。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for Access 2010 年 7 月版本包含以下更改：  
  
-   添加了对迁移到 SQL Server 2008 R2 和 Azure SQL 的支持。
-   添加到 SQL Server 和 Azure SQL 的安全连接。  
-   添加了对 Access 2010 数据库的支持。
-   添加的新的 SSMA 控制台应用程序命令行执行。
-   添加了对 SQL Server DateTime2 数据类型的支持。
  
## <a name="june-2008"></a>2008 年 6 月  
SSMA for Access 的 2008 年 6 月版本包含以下更改：  
  
-   添加了对 Access 2007 数据库的支持。  
  
## <a name="may-2007"></a>2007 年 5 月  
SSMA for Access 2007 年 5 月版本包含以下更改：  
  
-   添加了对使用工作组策略的 Access 数据库的支持。  
-   提供从 SQL Server 元数据资源管理器中删除已转换的对象的能力。  
-   添加了对用户输入的注释中的 SQL Server 支持格式化 SQL 模式。  
-   添加了对象转换中的改进。  
  
## <a name="november-2006"></a>2006 年 11 月  
SSMA for Access 的 2006 年 11 月版本包含以下更改：  
  
-   添加新的数据库迁移向导，指导您完成迁移的单个数据库从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
-   添加新的 Convert，负载，并将转换的 Access 数据库，迁移命令加载到已转换的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然后将迁移到的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]全部位于一个步骤。  
-   提高了的查询迁移。 现在将更多选择到视图的查询，请查询迁移。 有关详细信息，请参阅[转换访问数据库对象](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)。  
-   添加上编辑表和索引属性的能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**表**选项卡。  
-   添加新的全局设置：  
    -   你可以选择在编辑器窗口中显示行号。  
    -   你可以配置 SSMA 提示替换重复的对象，或在架构转换期间始终或永远不会替换重复的对象。  
-   添加一个新的转换选项，可以指定当复杂查询包含通配符，SSMA 是否显示警告。  
  
## <a name="july-2006"></a>2006 年 7 月  
SSMA for Access 的 2006 年 7 月版本是初次发布。
