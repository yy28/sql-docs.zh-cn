---
title: "什么 &#39; s SSMA for MySQL (MySQLToSql) 中的新增功能 |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 42706f2ce71fc540d8538f9614f1db17b4f70ea7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma-for-mysql-mysqltosql"></a>什么 &#39; s SSMA for MySQL (MySQLToSql) 中的新增功能
本主题列出每个版本中的 MySQL 更改 SSMA。  

## <a name="may-2016"></a>2016 年 5 月  
SSMA for MySQL 的 2016 年 5 月版本包含以下更改:。

1.  添加了对 SQL Server 2016 支持
2.  改进的分析器和冲突解决程序
3.  删除安装程序检查 for.Net 2.0
4.  更新的扩展包依赖项从.Net 3.5 到.Net 4.0
5.  固定的默认 BigInt typemapping mysql
6.  "保存项目"固定和 SSMA 控制台的"打开项目"命令
7.  SSMA 控制台的固定"securepassword"命令
8.  固定的初始加载的对象计数
9.  加载的固定的 MsSql 对象
10. 全局设置中的已修复的 bug 
 
## <a name="march-2016"></a>2016 年 3 月  
MySQL SSMA 的 2016 年 3 月预览版本包含以下更改：  
  
1.  支持迁移到 SQL Server 2016  
  
## <a name="january-2016"></a>2016 年 1 月  
MySQL SSMA 的 2016 年 1 月维护版本包含以下更改：  
  
1.  添加的视图日志菜单项的 SSMA (文档 RFC 5706203)  
  
2.  添加的遥测  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for MySQL 的 2014 年 7 月版本包含以下更改：  
  
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
SSMA for MySQL 的 2011 年 7 月版本包含以下更改：  
  
1.  添加了 MS SQL Server 2014 的支持。  
  
2.  有关转换到 Azure 的已修复的 bug  
  
3.  有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for MySQL 的 2011 年 7 月版本包含以下更改：  
  
-   支持的限制的转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"偏移量。  
  
-   改进了的错误报告数据迁移过程。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for MySQL 的 2011 年 4 月版本包含以下更改：  
  
-   单一的"SSMA 为 MySQL"，它支持的可安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"和 SQL Azure。  
  
-   连接的能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
  
-   增强型客户端数据迁移引擎，支持的数据的并行迁移。  
  
-   提高的数据迁移性能与简单和大容量日志恢复模式。  
  
-   MySQL 控制台版本的 SSMA 支持向后兼容性。 你将能够打开到 SSMA 5.0 版之前的版本创建的项目。  
  
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
  
-   支持迁移到本地 SQL Server 和 SQL Azure。  
  
-   **功能的快照：**架构和数据迁移的 MySQL 表/索引/约束。  
  

