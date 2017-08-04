---
title: "什么 &#39; s SSMA for Sybase (SybaseToSQL) 中的新增功能 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
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
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9d97e03212e6985ce9d506774bfff0aa2f4ec8d1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-sybase-sybasetosql"></a>什么 &#39; s SSMA for Sybase (SybaseToSQL) 中的新增功能
本主题列出每个版本中的 Sybase 更改 SSMA。  

## <a name="may-2016"></a>2016 年 5 月  
Sybase 的 SSMA 2016 年 5 月版包含以下更改：  

1.  添加了对 SQL Server 2016 支持
2.  删除安装程序检查 for.Net 2.0
3.  更新的扩展包依赖项从.Net 3.5 到.Net 4.0
4.  "保存项目"固定和 SSMA 控制台的"打开项目"命令
5.  SSMA 控制台的固定"securepassword"命令
6.  固定的初始加载的对象计数
7.  全局设置中的已修复的 bug

## <a name="march-2016"></a>2016 年 3 月  
Sybase SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
1.  支持迁移到 SQL Server 2016  
  
## <a name="january-2016"></a>2016 年 1 月  
Sybase 的 SSMA 2016 年 1 月维护版包含以下更改：  
  
1.  添加的视图日志菜单项的 SSMA (文档 RFC 5706203)  
  
2.  添加的遥测  
  
## <a name="july-2014"></a>2014 年 7 月  
Sybase 的 SSMA 2014 年 7 月版包含以下更改：  
  
1.  改进了的 Azure SQL DB 代码转换  
  
2.  扩展包功能移到架构以支持 Azure SQL DB  
  
3.  测试具有超过 10 k 的数据库对象的性能改进  
  
4.  处理大量对象的用户界面改进  
  
5.  突出显示的"已知"LOB 架构 （以便它们可以在转换中被忽略）  
  
6.  转换速度提高  
  
7.  显示 UI 中的对象计数  
  
8.  由多个 25%的报表大小缩减  
  
9. 未分析构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
Sybase 的 SSMA 2014 年 4 月版包含以下更改：  
  
-   添加了 MS SQL Server 2014 的支持。  
  
-   有关转换到 Azure 的已修复的 bug  
  
-   有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
Sybase 的 SSMA 2012 年 1 月版包含以下更改：  
  
-   对回滚触发器转换的支持。  
  
-   为转换提供修复@ROWCOUNT和 @@ERROR在同一组语句。  
  
## <a name="july-2011"></a>2011 年 7 月  
Sybase 的 SSMA 2011 年 7 月版包含以下更改：  
  
-   改进了的错误报告数据迁移过程。  
  
## <a name="april-2011"></a>2011 年 4 月  
Sybase 的 SSMA 2011 年 4 月版包含以下更改：  
  
-   合并"Sybase 的 SSMA"产品，它支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"和 SQL Azure。  
  
-   对连接和迁移到支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
  
-   将转换并将 Sybase 数据库迁移到 SQL Azure 的全新功能。  
  
-   增强型客户端数据迁移引擎，支持的数据的并行迁移。  
  
-   提高的数据迁移性能与简单和大容量日志恢复模式。  
  
-   区分大小写的 Sybase 数据库可以正确转换和迁移到区分大小写的 SQL Server。  
  
-   转换到 SQL Server ANSI join 语句的 Sybase ASE 非 ANSI join 语句的支持已得到扩展，删除和更新语句。  
  
-   用于连接到 Sybase ASE 服务器使用 Sybase ASE ODBC 访问接口和 Sybase ASE ADO.Net 提供程序的其他连接性选项。  
  
-   删除依赖于一个单独的数据库调用**SysDB**其中包含 Sybase 仿真函数 （作为扩展包的一部分安装）。  
  
-   Sybase 扩展包的 SSMA 现在可以安装在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]群集。  
  
-   后向兼容性的 SSMA （v4.0 和 v4.2） 的早期版本创建的项目。  
  
-   可以是 5.0 版产品的 Sybase 的 SSMA 安装与旧版本的 SSMA （v4.0 和 v4.2） 的并行 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月  
Sybase 的 SSMA 2010 年 7 月版包含以下更改：  
  
-   有关将迁移到 SQL Server 2008 R2 的支持  
  
-   新的 SSMA 控制台应用程序命令行执行  
  
-   使用服务器端和客户端数据迁移引擎的数据迁移的支持  
  
-   "自定义选择"语句中数据迁移的支持  
  
-   从 Sybase ASE 15.0.3 和 15.5 迁移的支持  
  
## <a name="june-2008"></a>2008 年 6 月  
Sybase 的 SSMA 2008 年 6 月版包含以下更改：  
  
-   SSMA 测试人员添加，它自动测试数据库对象转换和所做的 SSMA 数据迁移。 已完成所有 SSMA 迁移步骤后，使用 SSMA 测试人员来验证已转换的对象相同的方式工作，所有数据已正确都传输。  
  
-   添加预 SQL 转换。 用户现在可以指定临时表 （和其他对象） 为每个源过程在转换中使用的声明。  
  
-   在对象转换中的改进：  
  
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
  
-   保存项目，加载数据库内容时，更快。  
  
-   支持的 SQL Server 格式化 SQL 模式的用户输入的注释。  
  
-   在对象转换中的改进。  
  
请注意，对于此版本未更新的帮助文件。 有关详细信息，请参阅本主题中后面的文档说明部分。  
  
## <a name="november-2006"></a>2006 年 11 月  
Sybase 的 SSMA 2006 年 11 月版包含以下更改：  
  
-   新的全局设置：  
  
    -   你可以选择在编辑器窗口中显示行号。  
  
    -   你可以配置 SSMA 提示替换重复的对象，或在架构转换期间始终或永远不会替换重复的对象。  
  
-   新转换选项允许你配置 SSMA 处理以下情况的方式：  
  
    -   包含二进制字符串的 CAST 或 CONVERT 语句  
  
    -   检查相等表达式中的 null 值  
  
    -   代理表  
  
    -   用户的 RAISERROR 的消息错误号  
  
    -   包含未解析的标识符的 UPDATE 语句  
  
-   新的迁移选项，你指定 SSMA 应如何处理之外的日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]日期范围。  
  
-   A**格式化 SQL**上设置**SQL**选项卡上，后者将提高可读性的代码格式设置。  
  
-   包括以下的 bug 修复：  
  
    -   SSMA 现在将转换锁定表*表*IN {共享 |通过将 TABLOCK 或 TABLOCKX 提示添加到后续的独占} 模式语句选择对表的查询。  
  
    -   在字符表达式中使用二进制类型时，现在已添加必要的强制转换。  
  
    -   内存和性能改进。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月发布的用于 Sybase 的 SSMA 是初次发布。  
  
## <a name="see-also"></a>另请参阅  
[用于 Sybase &#40; 入门 SSMASybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  

