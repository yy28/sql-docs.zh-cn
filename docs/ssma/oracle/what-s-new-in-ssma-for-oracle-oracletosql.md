---
title: "什么 &#39; s SSMA for Oracle (OracleToSQL) 中的新增功能 |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 191fe2e11c43f4c190a87ee52df9ff87c259ea7d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-oracle-oracletosql"></a>什么 &#39; s SSMA for Oracle (OracleToSQL) 中的新增功能
本主题列出每个版本中的 Oracle 更改 SSMA。  

## <a name="may-2016"></a>2016 年 5 月  
适用于 Oracle 的 SSMA 的 2016 年 5 月版本包含以下更改：  

1.  添加了对 SQL Server 2016 支持
2.  添加的转换 Oracle 闪回存档表为 SQL Server 临时表
3.  Oracle VPD 策略将转换为 SQL Server 策略对象 （适用于 Oracle 的行级别安全性） 的添加的转换
4.  适用于 Oracle 的初始加载的降低的时间
5.  改进的分析器和冲突解决程序
6.  删除安装程序检查 for.Net 2.0
7.  更新的扩展包依赖项从.Net 3.5 到.Net 4.0
8.  "保存项目"固定和 SSMA 控制台的"打开项目"命令
9.  SSMA 控制台的固定"securepassword"命令
10. 固定的初始加载的对象计数
11. 固定为 Oracle 的字符数据类型转换
12. 全局设置中的已修复的 bug
  
## <a name="march-2016"></a>2016 年 3 月  
适用于 Oracle 的 SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
1.  支持迁移到 SQL Server 2016  
  
2.  对迁移 Oracle 行级别安全性 （有一些限制） 的支持  
  
3.  支持迁移到 SQL Server 列存储在内存中的 Oracle 表  
  
## <a name="january-2016"></a>2016 年 1 月  
2014 年 1 月的适用于 Oracle 的 SSMA 维护版本包含以下更改：  
  
1.  添加了对聚集索引支持  
  
2.  固定速度慢的 Oracle 架构查询 (RFC 5076207)  
  
3.  固定从控制台连接到 Azure  
  
4.  添加的视图日志菜单项的 SSMA (文档 RFC 5706203)  
  
5.  添加的遥测  
  
## <a name="july-2014"></a>2014 年 7 月  
适用于 Oracle 的 SSMA 的 2014 年 7 月版本包含以下更改：  
  
1.  针对 Azure SQL 数据库的支持  
  
2.  扩展包功能移到架构以支持 Azure SQL DB  
  
3.  对 Oracle 具体化视图的支持  
  
4.  支持 SQL Server 2014 内存优化表  
  
5.  测试具有超过 10 k 的数据库对象的性能改进  
  
6.  处理大量对象的用户界面改进  
  
7.  突出显示的"已知"LOB 架构  
  
8.  转换速度提高  
  
9. 显示 UI 中的对象计数  
  
10. 由多个 25%的报表大小缩减  
  
11. 未分析构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
适用于 Oracle 的 SSMA 的 2014 年 4 月版本包含以下更改：  
  
1.  添加了 MS SQL Server 2014 的支持。  
  
2.  添加了支持的 Oracle 12 和查询优化。  
  
3.  有关转换到 Azure 的已修复的 bug。  
  
4.  有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
适用于 Oracle 的 SSMA 的 2012 年 1 月版本包含以下更改：  
  
-   支持 RowType 和 RecordType 输入的参数默认为 NULL。  
  
## <a name="july-2011"></a>2011 年 7 月  
适用于 Oracle 的 SSMA 的 2011 年 7 月版本包含以下更改：  
  
-   支持转换到的 Oracle 序列[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"序列生成器。  
  
-   改进了的错误报告数据迁移过程。  
  
-   使用保留的字的语句的改进的转换。  
  
-   改进的函数中的日期值的隐式转换。  
  
## <a name="april-2011"></a>2011 年 4 月  
适用于 Oracle 的 SSMA 的 2011 年 4 月版本包含以下更改：  
  
-   合并"SSMA 为 Oracle"产品，它支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
  
-   对连接和迁移到支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
  
-   增强型客户端数据迁移引擎，支持的数据的并行迁移。  
  
-   提高的数据迁移性能与简单和大容量日志恢复模式。  
  
-   后向兼容性的 SSMA （v4.0 和 v4.2） 的早期版本创建的项目。  
  
-   SSMA for Oracle 5.0 版产品可以是使用较旧版本的 SSMA （v4.0 和 v4.2） 安装并行 (SxS)。  
  
-   对报表 （包括子类型、 VARRAY、 嵌套表、 对象表和对象视图） 的用户定义类型和它们的用法 PL/SQL 块使用特殊的错误消息中的支持。  
  
## <a name="july-2010"></a>2010 年 7 月  
适用于 Oracle 的 SSMA 2010 年 7 月版本包含以下更改：  
  
-   有关将迁移到 SQL Server 2008 R2 的支持  
  
-   新的 SSMA 控制台应用程序命令行执行  
  
-   使用服务器端和客户端数据迁移引擎的数据迁移的支持  
  
-   "自定义选择"语句中数据迁移的支持  
  
-   从 Oracle 11g R2 进行迁移的支持  
  
## <a name="june-2008"></a>2008 年 6 月  
适用于 Oracle 的 SSMA 2008 年 6 月版本包含以下更改：  
  
-   完成评估报表中的改进了。 它包括有关同义词的其他信息、 分析对象、 面板和 SQL Server 徽标删除操作，和布局持久性的原始源。  
  
-   在对象转换中的改进：  
  
    -   包 DBMS_LOB、 DBMS_SQL 转换添加。  
  
    -   联接修订的转换。  
  
    -   修改集合和记录转换，现在简单的情况下释放通过为每个字段的单独变量中的记录的转换。  
  
    -   记录和集合实现的改进。  
  
    -   添加的开窗聚合函数。  
  
    -   汇总/多维数据集添加子句。  
  
    -   NEXTVAL/CURVAL 的改善。  
  
    -   在 SET 子句中分组的列，对集进行分组和分组 ID 已添加。  
  
    -   MERGE 语句添加。  
  
    -   新的日期时间类型和记录和集合转换为添加的 CLR 数据类型的支持。  
  
-   未添加新功能的测试人员。 现在可以使用测试人员对象作为测试表，可以更改测试用例中的几个可测试对象的调用顺序，用户可以测试过程和函数与记录和集合作为参数和返回值，并添加了分析器来检查依赖关系仅使用表。  
  
## <a name="august-2007"></a>2007 年 8 月  
适用于 Oracle 的 SSMA 的 2007 年 8 月版本包含以下更改：  
  
-   新的测试人员组件可让您创建、 管理和运行测试用例来验证转换后的 SQL 代码。  
  
-   Oracle 子类型、 集合和本地模块的转换已添加到 SQL 转换器。  
  
-   新的同步功能允许你将特定对象与 SQL Server 数据库同步。  
  
-   添加了新的转换选项。  
  
## <a name="april-2007"></a>2007 年 4 月  
2007 年 4 月版本的适用于 Oracle 的 SSMA 是初次发布。  
  

