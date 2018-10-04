---
title: 什么是适用于 DB2 的 SSMA 中的新增功能 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: deaaaf4141c363606abfc86720ba4ed043426af6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723805"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>什么是适用于 DB2 的 SSMA 中的新增功能 (DB2ToSQL)
本文列出了每个版本中的 DB2 更改 SSMA。  

## <a name="ssma-v710"></a>SSMA v7.10
SSMA for DB2 的 v7.10 版本包含以下更改：
- 可提供额外的安全和隐私保护功能以满足全局要求中的更改的目标的修补。
- BEGIN END 块转换为修补程序。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v79"></a>SSMA v7.9
SSMA for DB2 的 v7.9 版本包含以下更改：
- 提高质量和转换的度量值的目标的修补。
- 支持在 SSMA 命令行中更改数据类型映射和项目首选项。
- 有关迁移支持使用 SQL Server Integration Services (SSIS) 数据。 转换后的架构，则可以通过右键单击上下文菜单选项创建的 SSIS 包。
- SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在以前版本的 SSMA，Azure SQL 数据库前缀必须明确指出在项目设置。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v78"></a>SSMA 7.8 版
SSMA for DB2 的 7.8 版版本包含以下更改：
- 在项目设置中的突出显示的更改类型映射。
- 提供用户要禁用遥测数据的能力。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for DB2 的 v7.7 版本包含以下更改：
- 适用于 DB2 的 SSMA 已得到增强改进质量和转换的度量值的目标修补。
- 基于普遍的需求，返回是适用于 DB2 的 SSMA 的 32 位版本。 与以前的实现 （之前 v7.4) 相比，有两个安装程序软件包，但不能并行安装。 因此，必须选择最适合您的版本根据连接组件。 最好始终使用 64 位版本中，在可能的情况。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for DB2 的 v7.6 版本已得到增强，提高质量和转换的度量值的目标修补和支持 SQL Server 2017 （公共预览版）。 支持 Windows 和 Linux 上的 SQL Server 2017 处于公共预览状态，不应该用于生产迁移。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 的安装先决条件，并已停止使用该工具的 32 位版本。

## <a name="ssma-v75"></a>SSMA 版本 7.5
SSMA for DB2 版本 7.5 版本已得到增强了一些改进，以确保为残障人士使用的可访问性。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA 版本 7.5 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for DB2 的 v7.4 版本包含以下更改：
- **查询超时值**选项现可在源和目标架构对象发现期间访问。
![query timeout 选项](../media/query-timeout_red.png)

- 有所改进质量和转换指标，包括目标修补，根据客户反馈。

> [!IMPORTANT]
> .Net 4.5.2 是用于安装 SSMA v7.4 必备组件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停止。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for DB2 的 v7.3 版本包含以下更改：
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
SSMA for DB2 的 7.2 版版本包含以下更改：
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
SSMA for DB2 的 2016 年 5 月版本包含以下更改：  

-  添加了对 SQL Server 2016 的支持。
-  SQL Server 内存中和 hekaton 功能 DB2 内存中和常规表添加了的转换。
-  SQL Server 策略对象 （DB2 行级别安全性） 的 DB2 访问控件添加了的转换。
-  添加的转换 DB2 系统版本控制表为 SQL Server 的临时表。
-  改进的 DB2 分析器和冲突解决程序。
-  删除.Net 2.0 的安装程序检查。
-  从 Db2 安装程序中删除不必要的 *.dll。
-  修复了"保存项目"和 SSMA 控制台的"打开项目"命令。
-  SSMA 控制台中的固定"securepassword"命令。
-  修复了初始加载的对象的计数。
-  全局设置中修复了 bug。
  
## <a name="march-2016"></a>2016 年 3 月  
DB2 的 SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
-  添加了对迁移到 SQL Server 2016 的支持。  
  
## <a name="january-2016"></a>2016 年 1 月  
DB2 的 SSMA 的 2016 年 1 月维护版本包含以下更改：  
  
-  添加了的对多个标准函数。  
-  修复了 DB2 分析器错误。  
-  固定的 DB2 v9 zOS 支持 (RFC 5690920)。  
-  固定的 DB2 在转换过程中无法解析标识符的错误。  
-  SSMA (RFC 5706203) 添加了的视图日志菜单项。  
-  添加了遥测数据。
  
## <a name="november-2014"></a>2014 年 11 月  
SSMA for DB2 的 2014 年 11 月版本是初始版本。
