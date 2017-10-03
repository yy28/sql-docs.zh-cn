---
title: "什么 &#39; s SSMA for DB2 中的新增功能 (DB2ToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 09/30/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 8246a40f5fd59ae4d8a28f1e0315ea1a015e8e7d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/30/2017

---
# <a name="what39s-new-in-ssma-for-db2-db2tosql"></a>什么 &#39; s SSMA for DB2 中的新增功能 (DB2ToSQL)
本主题列出每个版本中的 DB2 更改 SSMA。  

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for DB2 的 v7.6 版本已得到增强，具有提高质量和转换的度量值的目标修补程序和 SQL Server 2017 （公共预览版） 支持。 对于 Windows 和 Linux 上的 SQL Server 2017 支持是在公共预览版中并不用于生产迁移。

> [!IMPORTANT]
> SSMA v7.4 和更高版本，.Net 4.5.2 的目标是安装先决条件，并已停止使用该工具的 32 位版本。

## <a name="ssma-v75"></a>SSMA v7.5 还是
SSMA for DB2 的 v7.5 都发布已得到增强几项改进，确保残障人士更大的可访问性。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.5 还是的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for DB2 的 v7.4 版本包含以下更改：
- **查询超时值**选项现已可用在源和目标架构对象发现期间。
![query timeout 选项](../media/query-timeout_red.png)

- 通过目标修补程序，根据客户反馈，改进了的质量和转换的度量值。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for DB2 的 v7.3 版本包含以下更改：
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
SSMA for DB2 的 7.2 版版本包含以下更改：
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
SSMA for DB2 的 2016 年 5 月版本包含以下更改：  

-  添加了对 SQL Server 2016 的支持。
-  添加的转换 DB2 内存中和常规表为 SQL Server 内存中和 hekaton 功能。
-  添加的转换 DB2 访问控制为 SQL Server 策略对象 （for DB2 的行级别安全性）。
-  向 SQL Server 临时表的 DB2 版本由系统控制表添加的转换。
-  改进的 DB2 分析器和冲突解决程序。
-  删除安装程序检查 for.Net 2.0。
-  从 Db2 安装程序中删除不必要的 *.dll。
-  "保存项目"固定和 SSMA 控制台的"打开项目"命令。
-  SSMA 控制台的固定"securepassword"命令。
-  固定的初始加载的对象计数。
-  全局设置中的已修复的 bug。
  
## <a name="march-2016"></a>2016 年 3 月  
DB2 SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
-  添加了对迁移到 SQL Server 2016 的支持。  
  
## <a name="january-2016"></a>2016 年 1 月  
DB2 SSMA 的 2016 年 1 月维护版本包含以下更改：  
  
-  添加了对许多标准功能的支持。  
-  修复了 DB2 分析器错误。  
-  固定的 DB2 v9 zOS 支持 (RFC 5690920)。  
-  固定的 DB2 无法在转换期间解析标识符错误。  
-  添加的视图日志菜单项的 SSMA (文档 RFC 5706203)。  
-  添加的遥测。
  
## <a name="november-2014"></a>2014 年 11 月  
2014 年 11 月发行版的 SSMA for DB2 是初次发布。
