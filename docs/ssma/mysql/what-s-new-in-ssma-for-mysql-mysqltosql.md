---
title: 什么是 SSMA for MySQL (MySQLToSql) 中的新增功能 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d5b17e7b054552c96c6fb3ff861c22b4e87e394f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674825"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL 中的新增功能 (MySQLToSql)
本文列出了每个版本中的 MySQL 更改 SSMA。 

## <a name="ssma-v710"></a>SSMA v7.10
SSMA for MySQL 的 v7.10 版本包含以下更改：
- 可提供额外的安全和隐私保护功能以满足全局要求中的更改的目标的修补。
- 函数名称和参数列表之间的空格转换为修补程序。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v79"></a>SSMA v7.9
SSMA for MySQL 的 v7.9 版本包含以下更改：
- 提高质量和转换的度量值的目标的修补。
- 对迁移从 MySQL 到 Azure SQL 数据库的空间数据类型的部分支持。
- 支持在 SSMA 命令行中更改数据类型映射和项目首选项。
- 有关迁移支持使用 SQL Server Integration Services (SSIS) 数据。 转换后的架构，则可以通过右键单击上下文菜单选项创建的 SSIS 包。
- SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在以前版本的 SSMA，Azure SQL 数据库前缀必须明确指出在项目设置。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v78"></a>SSMA 7.8 版
SSMA for MySQL 的 7.8 版版本包含以下更改：
- 在项目设置中的突出显示的更改类型映射。
- 提供用户要禁用遥测数据的能力。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for MySQL 的 v7.7 版本包含以下更改：
- 适用于 MySQL 的 SSMA 已得到增强改进质量和转换的度量值的目标修补。
- 基于普遍的需求，返回是适用于 MySQL 的 SSMA 的 32 位版本。 与以前的实现 （之前 v7.4) 相比，有两个安装程序软件包，但不能并行安装。 因此，必须选择最适合您的版本根据连接组件。 最好始终使用 64 位版本中，在可能的情况。
- 适用于 MySQL 的 SSMA 现在具有 ODBC 连接字符串连接模式，以便您可以使用任何第三方 ODBC 驱动程序兼容与 MySQL 配合使用。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for MySQL 的 v7.6 版本已得到增强，提高质量和转换的度量值的目标修补和支持 SQL Server 2017 （公共预览版）。 对 Windows 和 Linux 上的 SQL Server 2017 的支持处于公共预览状态，并不用于生产的迁移。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 的安装先决条件，并已停止使用该工具的 32 位版本。

## <a name="ssma-v75"></a>SSMA 版本 7.5
SSMA for MySQL 的版本 7.5 版本已得到增强了一些改进，以确保为残障人士使用的可访问性。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA 版本 7.5 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for MySQL 的 v7.4 版本包含以下更改：
- **查询超时值**选项现可在源和目标架构对象发现期间访问。
![query timeout 选项](../media/query-timeout_red.png)
- 有所改进质量和转换指标，包括目标修补，根据客户反馈。

> [!IMPORTANT]
> .Net 4.5.2 是用于安装 SSMA v7.4 必备组件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停止。 

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for MySQL 的 v7.3 版本包含以下更改：
- 改进的质量和转换度量值与目标修补，根据客户反馈。
- 通过以下各项公开的 SSMA 可扩展性框架：
  - 导出到 SQL Server Data Tools (SSDT) 项目的功能。
    -   现在，您可以到 SSDT 项目从 SSMA 导出架构脚本。 架构脚本可用于进行附加的架构更改和部署你的数据库。
![将另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  - 可供执行的自定义转换 SSMA 的库。
    - 现在可以构造自定义语法转换和转换之前未处理的 SSMA 能处理的代码。
      - 在此博客文章提供了有关如何构造自定义转换器说明[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 下载此转换的示例项目[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA 7.2 版
SSMA for MySQL 的 7.2 版版本包含以下更改：
- 改进的质量和转换度量值与目标修补，根据客户反馈。
- 遥测数据增强功能提供更好的数据点来解决客户问题并提高 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access v7.1 版本包含以下更改：
- SQL Server 2017 的 Windows 和 Linux CTP1 现在是用于迁移的支持的目标平台。 此功能是 technical preview 中，使架构和数据移动到目标 SQL 服务器。
- SSMA 现在支持自动更新，以下载最新版本的 SSMA 立即可用。
- SSMA 可安装二进制文件现在被通过 Windows installer 包文件 (.msi)。

**资源**

[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[评估并将数据从非 Microsoft 数据平台迁移到 SQL Server *（与 Oracle 的示例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年 5 月  
SSMA for MySQL 的 2016 年 5 月版本包含以下更改:。

-  添加了对 SQL Server 2016 的支持。
-  改进了的分析器和冲突解决程序。
-  删除.Net 2.0 的安装程序检查。
-  已更新的扩展包依赖项从.Net 3.5 到.Net 4.0。
-  固定的默认值为 MySql 的 BigInt typemapping 所。
-  修复了"保存项目"和 SSMA 控制台的"打开项目"命令。
-  SSMA 控制台中的固定"securepassword"命令。
-  修复了初始加载的对象的计数。
-  正在加载固定的 MsSql 对象。
-  全局设置中修复了 bug。
 
## <a name="march-2016"></a>2016 年 3 月  
MySQL 的 SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
-  添加了对迁移到 SQL Server 2016 的支持。 
  
## <a name="january-2016"></a>2016 年 1 月  
MySQL 的 SSMA 的 2016 年 1 月维护版本包含以下更改：  
  
-  SSMA (RFC 5706203) 添加了的视图日志菜单项。  
-  添加了遥测数据。  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for MySQL 的 2014 年 7 月版本包含以下更改：  
  
-  改进了的 Azure SQL DB 代码转换。 
-  扩展包功能移到架构以支持 Azure SQL DB。  
-  性能改进测试具有超过 10 k 的数据库对象。  
-  处理大量对象的 UI 改进。  
-  （因此也可以在转换过程中忽略），突出显示的"已知"LOB 架构。  
-  转换速度得到了改进。  
-  显示在 UI 中的对象计数。  
-  超过 25%减小报表大小。  
-  未分析的构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for MySQL 的 2011 年 7 月版本包含以下更改：  
  
-  MS SQL Server 2014 添加了的支持。  
-  有关转换到 Azure 的已修复的 bug  
-  有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for MySQL 的 2011 年 7 月版本包含以下更改：  
  
-   支持限制转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"偏移量。  
-   改进了的错误报告数据迁移过程。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for MySQL 的 2011 年 4 月版本包含以下更改：  
  
-   可安装的"SSMA for MySQL"，它支持单[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali"和 Azure SQL。  
-   连接的能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。  
-   增强的客户端的数据迁移引擎，支持并行迁移的数据。  
-   改进的数据迁移性能与简单和大容量日志恢复模式。  
-   适用于 MySQL 控制台版本的 SSMA 支持向后兼容性。 您可以打开到 SSMA 5.0 版之前的版本所创建的项目。  
-   SSMA for MySQL 5.0 版产品可以是使用较旧版本的 SSMA 产品安装并排 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for MySQL 的 2010 年 7 月版本包含以下功能：  
  
1.  **用户界面有所改进：**  
  
    -   SQL 模式选项卡上的 MySQL 数据库对象  
    -   MySQL 数据库对象的设置选项卡  
    -   数据选项卡上的 MySQL 表  
    -   转换和迁移页中的已更新的项目设置  
    -   在表级别的数据迁移设置  
  
2.  **若要连接到 MySQL 和 SQL Server 的改进：**  
  
    -   在 MySQL 中的 SSL 连接性  
    -   SQL Server 中的加密的连接  
  
3.  **MySQL 元数据库资源管理器的改进：**  
  
    -   正在加载所有 MySQL 数据库对象和其各自的选项卡。  
  
4.  **对象转换为改进：**  
  
    -   MySQL 元数据库对象 – 过程、 函数、 视图、 触发器和语句的转换。  
    -   针对表中的空间数据类型的有限的支持。  
    -   将 MySQL 函数转换为 SQL Server 存储过程  
    -   若要应用对象转换期间的 SQL 模式和字符集映射的选项  
  
5.  **数据迁移的改进：**  
  
    -   使用服务器端和客户端的数据迁移引擎数据迁移的支持  
    -   对空间数据迁移的支持  
    -   自定义 SQL 表的数据迁移  
  
6.  **SSMA for MySQL 控制台：**  
  
    -   有关适用于 MySQL 的 SSMA 支持控制台功能  
    -   支持脚本级别进行连接  
  
## <a name="january-2010"></a>2010 年 1 月  
SSMA for MySQL 的 2010 年 1 月版本是初始版本。 它包含以下功能：  
  
-   添加了对迁移到同时支持在本地 SQL Server 和 Azure SQL。  
  
-   **功能的快照：** 架构和数据迁移的 MySQL 表/索引/约束。
