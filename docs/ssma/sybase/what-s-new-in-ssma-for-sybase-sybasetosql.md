---
title: "什么 &#39; s SSMA for Sybase (SybaseToSQL) 中的新增功能 |Microsoft 文档"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 80642503480add90fc75573338760ab86139694c
ms.openlocfilehash: 1054c9279039eda01320e1afd9745b6a53200b3f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="what39s-new-in-ssma--for-sybase-sybasetosql"></a>什么 &#39; s SSMA for Sybase (SybaseToSQL) 中的新增功能
本主题列出每个版本中的 Sybase 更改 SSMA。 

## <a name="ssma-v74"></a>SSMA v7.4
Sybase 的 SSMA v7.4 版包含以下更改：
- **查询超时值**选项现已可用在源和目标架构对象发现期间。
![query timeout 选项](../media/query-timeout_red.png)
- 通过目标修补程序，根据客户反馈，改进了的质量和转换的度量值。

> [!IMPORTANT]
> .Net 4.5.2 是安装 SSMA v7.4 的先决条件。 此外，从 v7.4 开始，SSMA 的 32 位版本是要停止使用。  

## <a name="ssma-v73"></a>SSMA v7.3
Sybase 的 SSMA v7.3 版包含以下更改：
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
Sybase 的 SSMA 7.2 版版包含以下更改：
- 改进的质量和转换度量值根据客户反馈的目标修补程序。
- 遥测功能增强以提供更好的数据点，以解决客户问题和改进 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access 的 v7.1 版本包含以下更改：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 现在是一个用于迁移的支持的目标平台。 此功能在技术预览中，并支持架构和数据移动到目标 SQL 服务器。
- SSMA 现在支持自动更新，以下载最新版本的 SSMA，只要可用。
- SSMA 可安装二进制文件现在被通过 Windows installer 包文件 (.msi)。

**资源**

[将 SQL Server Migration Assistant 的转换功能扩展](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[评估并将数据从非 Microsoft 数据平台迁移到 SQL Server *（与 Oracle 示例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年 5 月  
Sybase 的 SSMA 2016 年 5 月版包含以下更改：  

-  添加了对 SQL Server 2016 的支持。
-  删除安装程序检查 for.Net 2.0。
-  更新到.Net 4.0 通过.Net 3.5 的扩展包依赖性。
-  "保存项目"固定和 SSMA 控制台的"打开项目"命令。
-  SSMA 控制台的固定"securepassword"命令。
-  固定的初始加载的对象计数。
-  全局设置中的已修复的 bug。

## <a name="march-2016"></a>2016 年 3 月  
Sybase SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
-  添加了对迁移到 SQL Server 2016 的支持。  
  
## <a name="january-2016"></a>2016 年 1 月  
Sybase 的 SSMA 2016 年 1 月维护版包含以下更改：  
  
-  添加的视图日志菜单项的 SSMA (文档 RFC 5706203)。  
-  添加的遥测。 
  
## <a name="july-2014"></a>2014 年 7 月  
Sybase 的 SSMA 2014 年 7 月版包含以下更改：  
  
-  改进的 Azure SQL DB 代码转换。  
-  移动到架构以支持 Azure SQL DB 扩展包功能。  
-  添加的性能改进测试具有超过 10 k 的数据库对象。  
-  添加了对具有大量对象的处理 UI 改进。  
-  增加了功能，以突出显示"已知"LOB 架构 （以便它们可以在转换中被忽略）。  
-  添加的转换速度得到了改进。  
-  添加在用户界面中将显示对象计数的功能。 
-  降低的报表大小超过 25%。  
-  未分析构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
Sybase 的 SSMA 2014 年 4 月版包含以下更改：  
  
-   添加了 MS SQL Server 2014 的支持。  
-   有关转换到 Azure 的已修复的 bug。  
-   有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
Sybase 的 SSMA 2012 年 1 月版包含以下更改：  
  
-   添加了对回滚触发器转换的支持。  
-   为转换提供修复@ROWCOUNT和 @@ERROR在同一组语句。  
  
## <a name="july-2011"></a>2011 年 7 月  
Sybase 的 SSMA 2011 年 7 月版包含以下更改：  
  
-   改进了的错误报告数据迁移过程。  
  
## <a name="april-2011"></a>2011 年 4 月  
Sybase 的 SSMA 2011 年 4 月版包含以下更改：  
  
-   合并"Sybase 的 SSMA"产品，它支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"和 Azure SQL。  
-   增加了对连接并将迁移到支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   添加用于转换和迁移到 Azure SQL 的 Sybase 数据库的新功能。  
-   增强的客户端数据迁移引擎，支持的数据的并行迁移。  
-   提高的数据迁移性能与简单和大容量日志恢复模式。  
-   添加正确转换和迁移到区分大小写的 SQL Server 的区分大小写的 Sybase 数据库的能力。  
-   添加了对转换到 SQL Server ANSI join 语句的 Sybase ASE 非 ANSI join 语句的支持已得到扩展，删除和更新语句。  
-   提供用于连接到 Sybase ASE 服务器使用 Sybase ASE ODBC 访问接口和 Sybase ASE ADO.Net 提供程序的其他连接性选项。  
-   删除名为的单独数据库的依赖**SysDB**，其中包含 Sybase 仿真函数 （作为扩展包的一部分安装）。  
-   添加的功能上安装 Sybase 扩展包 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]群集。  
-   添加了早期版本的 SSMA （v4.0 和 v4.2） 创建的项目的向后兼容性。  
-   添加与旧版本的 SSMA （v4.0 和 v4.2） 安装 SSMA for Sybase 5.0 版产品的并行 (SxS) 的能力。  
  
## <a name="july-2010"></a>2010 年 7 月  
Sybase 的 SSMA 2010 年 7 月版包含以下更改：  
  
-   添加了对将迁移到 SQL Server 2008 R2 的支持。  
-   添加的新的 SSMA 控制台应用程序命令行执行。  
-   添加了对使用服务器端和客户端数据迁移引擎的数据迁移的支持。  
-   添加了对"自定义选择"语句中数据迁移的支持。  
-   添加了对从 Sybase ASE 15.0.3 和 15.5 迁移的支持。  
  
## <a name="june-2008"></a>2008 年 6 月  
Sybase 的 SSMA 2008 年 6 月版包含以下更改：  
  
-   添加的 SSMA Tester，自动测试数据库对象转换，以及所做的 SSMA 数据迁移。 已完成所有 SSMA 迁移步骤后，使用 SSMA 测试人员来验证已转换的对象相同的方式工作，所有数据已正确都传输。  
-   添加的预 SQL 转换。 用户现在可以指定临时表 （和其他对象） 为每个源过程在转换中使用的声明。  
-   添加了对象转换中的改进：  
    -   联接修订的转换。  
    -   聚合和非聚合而无需具有/组 by 子句。  
    -   使用 SELECT INTO 语句 IDENTITY 函数。  
    -   群集的约束和索引数据仅锁定。  
    -   由 SELECT INTO 创建的临时表。  
    -   约束 / 临时表的索引。  
    -   新[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]支持 2008 datetime 类型。  
    -   Sybase 15.0 连接和数据类型支持。  
  
## <a name="may-2007"></a>2007 年 5 月  
Sybase 的 SSMA 2007 年 5 月版包含以下更改：  
  
-   添加将项目保存时更快加载数据库内容的功能。  
-   添加了对用户输入的注释中的 SQL Server 支持格式化 SQL 模式。  
-   添加了对象转换中的改进。  
  
对于此版本未更新的帮助文件。 有关详细信息，请参阅本主题中后面的文档说明部分。  
  
## <a name="november-2006"></a>2006 年 11 月  
Sybase 的 SSMA 2006 年 11 月版包含以下更改：  
  
-   添加新的全局设置：  
    -   你可以选择在编辑器窗口中显示行号。  
    -   你可以配置 SSMA 提示替换重复的对象，或在架构转换期间始终或永远不会替换重复的对象。  
-   添加一个新的转换选项，允许你配置 SSMA 处理以下情况的方式：  
    -   包含二进制字符串的 CAST 或 CONVERT 语句。  
    -   相等表达式中的 null 值的检查。  
    -   代理表。  
    -   用户消息的 RAISERROR 错误号。  
    -   更新包含无法解析的标识符的语句。  
-   添加一个新的迁移选项，允许您指定 SSMA 应如何处理之外的日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]日期范围。  
-   添加**格式化 SQL**上设置**SQL**选项卡上，后者将提高可读性的代码格式设置。  
-   包括以下的 bug 修复：  
    -   SSMA 现在将转换锁定表*表*IN {共享 |通过将 TABLOCK 或 TABLOCKX 提示添加到后续的独占} 模式语句选择对表的查询。  
    -   在字符表达式中使用二进制类型时，现在已添加必要的强制转换。  
    -   内存和性能改进。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月发布的用于 Sybase 的 SSMA 是初次发布。  
  
## <a name="see-also"></a>另請參閱  
[用于 Sybase &#40; 入门 SSMASybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
