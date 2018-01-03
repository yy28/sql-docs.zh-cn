---
title: "SSMA for MySQL (MySQLToSql) 中的新增 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 09/30/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: "21"
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6da0bf47b7976da1f21262d23bd29d8e093a0516
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL (MySQLToSql) 的新增功能
本主题列出每个版本中的 MySQL 更改 SSMA。 

## <a name="ssma-v76"></a>SSMA v7.6
MySQL 的 SSMA v7.6 版已得到增强，具有提高质量和转换的度量值的目标修补程序和 SQL Server 2017 （公共预览版） 支持。 对于 Windows 和 Linux 上的 SQL Server 2017 支持是在公共预览版中并不用于生产迁移。

> [!IMPORTANT]
> SSMA v7.4 和更高版本，.Net 4.5.2 的目标是安装先决条件，并已停止使用该工具的 32 位版本。

## <a name="ssma-v75"></a>SSMA v7.5 还是
MySQL 的 SSMA v7.5 还是版已得到增强几项改进，确保残障人士更大的可访问性。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.5 还是的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for MySQL 的 v7.4 版本包含以下更改：
- **查询超时值**选项现已可用在源和目标架构对象发现期间。
![query timeout 选项](../media/query-timeout_red.png)
- 通过目标修补程序，根据客户反馈，改进了的质量和转换的度量值。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。 

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for MySQL 的 v7.3 版本包含以下更改：
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
SSMA for MySQL 的 7.2 版版本包含以下更改：
- 改进的质量和转换度量值根据客户反馈的目标修补程序。
- 遥测功能增强以提供更好的数据点，以解决客户问题和改进 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access 的 v7.1 版本包含以下更改：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 现在是一个用于迁移的支持的目标平台。 此功能是 technical preview 中，并且允许架构和数据移动到目标 SQL 服务器。
- SSMA 现在支持自动更新，以下载最新版本的 SSMA，只要可用。
- SSMA 可安装二进制文件现在被通过 Windows installer 包文件 (.msi)。

**资源**

[将 SQL Server Migration Assistant 的转换功能扩展](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[评估并将数据从非 Microsoft 数据平台迁移到 SQL Server *（与 Oracle 示例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年 5 月  
SSMA for MySQL 的 2016 年 5 月版本包含以下更改:。

-  添加了对 SQL Server 2016 的支持。
-  改进的分析器和冲突解决程序。
-  删除安装程序检查 for.Net 2.0。
-  更新到.Net 4.0 通过.Net 3.5 的扩展包依赖性。
-  固定的默认 BigInt typemapping mysql。
-  "保存项目"固定和 SSMA 控制台的"打开项目"命令。
-  SSMA 控制台的固定"securepassword"命令。
-  固定的初始加载的对象计数。
-  加载的固定的 MsSql 对象。
-  全局设置中的已修复的 bug。
 
## <a name="march-2016"></a>2016 年 3 月  
MySQL SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
-  添加了对迁移到 SQL Server 2016 的支持。 
  
## <a name="january-2016"></a>2016 年 1 月  
MySQL SSMA 的 2016 年 1 月维护版本包含以下更改：  
  
-  添加的视图日志菜单项的 SSMA (文档 RFC 5706203)。  
-  添加的遥测。  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for MySQL 的 2014 年 7 月版本包含以下更改：  
  
-  改进的 Azure SQL DB 代码转换。 
-  扩展包功能移到架构以支持 Azure SQL DB。  
-  性能改进测试具有超过 10 k 的数据库对象。  
-  处理大量对象的用户界面改进。  
-  （以便它们可以在转换中被忽略），突出显示的"已知"LOB 架构。  
-  转换速度得到了改进。  
-  显示 UI 中的对象计数。  
-  报表大小减少了 25%以上。  
-  未分析构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for MySQL 的 2011 年 7 月版本包含以下更改：  
  
-  添加了 MS SQL Server 2014 的支持。  
-  有关转换到 Azure 的已修复的 bug  
-  有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for MySQL 的 2011 年 7 月版本包含以下更改：  
  
-   支持的限制的转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"偏移量。  
-   改进了的错误报告数据迁移过程。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for MySQL 的 2011 年 4 月版本包含以下更改：  
  
-   单一的"SSMA 为 MySQL"，它支持的可安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"和 Azure SQL。  
-   连接的能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   增强的客户端数据迁移引擎，支持的数据的并行迁移。  
-   提高的数据迁移性能与简单和大容量日志恢复模式。  
-   MySQL 控制台版本的 SSMA 支持向后兼容性。 你可以打开到 SSMA 5.0 版之前的版本创建的项目。  
-   可以是 5.0 版产品的 MySQL 的 SSMA 装有 SSMA 产品的较旧版本的并行 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for MySQL 的 2010 年 7 月版本包含以下功能：  
  
1.  **对用户界面的改进：**  
  
    -   SQL 模式选项卡上的 MySQL 数据库对象  
    -   MySQL 数据库对象的设置选项卡  
    -   数据选项卡上的 MySQL 表  
    -   转换和迁移页中的更新的项目设置  
    -   在表级别的数据迁移设置  
  
2.  **若要连接到 MySQL 和 SQL Server 的改进：**  
  
    -   在 MySQL 中的 SSL 连接  
    -   SQL Server 中的加密的连接  
  
3.  **到 MySQL 元数据库资源管理器改进：**  
  
    -   正在加载 MySQL 数据库的所有对象和其相应的选项卡。  
  
4.  **对象转换为改进：**  
  
    -   MySQL 元数据库对象 – 过程、 函数、 视图、 触发器和语句的转换。  
    -   对表中的空间数据类型的有限的支持。  
    -   若要将 MySQL 函数转换为 SQL Server 存储过程的选项  
    -   若要应用对象转换期间的 SQL 模式和 Charset 映射的选项  
  
5.  **对数据迁移的改进：**  
  
    -   使用服务器端和客户端数据迁移引擎的数据迁移的支持  
    -   对空间数据迁移的支持  
    -   对于表的数据迁移的自定义 SQL  
  
6.  **SSMA for MySQL 控制台：**  
  
    -   有关 MySQL 的 SSMA 支持控制台功能  
    -   脚本级别进行连接的支持  
  
## <a name="january-2010"></a>2010 年 1 月  
2010 年 1 月发行版的 SSMA mysql 是初次发布。 它包含以下功能：  
  
-   添加了对迁移到同时支持本地 SQL Server 和 Azure SQL。  
  
-   **功能的快照：**架构和数据迁移的 MySQL 表/索引/约束。
