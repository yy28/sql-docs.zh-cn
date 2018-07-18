---
title: SQL Server 的最大容量规范 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [SQL Server]
- number capacity specifications [SQL Server]
- size [SQL Server], capacity specifications
- number of objects
- capacity specifications [SQL Server]
- maximum capacity specifications [SQL Server]
- size [SQL Server]
- replication capacity specifications [SQL Server]
- objects [SQL Server], capacity specifications
- Database Engine [SQL Server], capacity specifications
ms.assetid: 13e95046-0e76-4604-b561-d1a74dd824d7
caps.latest.revision: 76
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 08997fa0dd4fe66b4e3c22fd6447105d11991c29
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37296037"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>SQL Server 的最大容量规范
  以下各表指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件中定义的各种对象的最大大小和最大数量。 若要导航到某种 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 技术相应的表，请单击其链接：  
  
 [SQL Server 数据库引擎对象](#Engine)  
  
 [SQL Server 实用工具对象](#Utility)  
  
 [SQL Server 数据层应用程序对象](#DAC)  
  
 [SQL Server 复制对象](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] 对象  
 下表指定在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中定义的或在 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句中引用的各种对象的最大大小和最大数量。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 对象 (object)|最大大小/数量[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]（32 位）|最大大小/数量 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] （64 位）|  
|---------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|批大小<br /><br /> 注意： 网络数据包大小是使用应用程序和关系之间进行通信的表格格式数据流 (TDS) 数据包的大小[!INCLUDE[ssDE](../includes/ssde-md.md)]。 默认的数据包大小为 4 KB，由“网络数据包大小”配置选项控制。|65,536 * 网络数据包大小|65,536 * 网络数据包大小|  
|每个短字符串列的字节数|8,000|8,000|  
|每个 GROUP BY、ORDER BY 的字节数|8,060|8,060|  
|每个索引键的字节数<br /><br /> 注意： 最大的任何索引键中的字节数不能超过 900 中的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 可以使用最大大小合计超过 900 的可变长度列定义键，前提是这些列中所插入行的数据都不超过 900 字节。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，可将非键列包含于非聚集索引中以避免最大索引键大小 900 字节的限制。|900|900|  
|每个外键的字节数|900|900|  
|每个主键的字节数|900|900|  
|每行的字节数<br /><br /> 注意：<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支持行溢出存储，行溢出存储使长度可变的列可以被推送到行外。 只有 24 字节的根存储在推送出行外的可变长度列的主记录中；因此，此版本中的有效行限制高于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]早期版本中的有效行限制。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书中的“行溢出数据超过 8 KB”这一主题。|8,060|8,060|  
|内存优化表中的每行字节数<br /><br /> 注意：<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 内存中 OLTP 不支持行溢出存储。 可变长度列不会推送到行外。 这将您可在内存优化表中指定的可变长度列的最大宽度限制为最大行大小。 有关详细信息，请参阅 [内存优化表中的表和行大小](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)。|不支持|8,060|  
|存储过程源文本中的字节数|批处理大小中的较小者或 250 MB|批处理大小中的较小者或 250 MB|  
|每个 `varchar(max)`、`varbinary(max)`、`xml`、`text` 或 `image` 列的字节数|2^31-1|2^31-1|  
|每个 `ntext` 或 `nvarchar(max)` 列的字符数|2^30-1|2^30-1|  
|每个表的聚集索引数|@shouldalert|@shouldalert|  
|GROUP BY、ORDER BY 中的列数|仅受字节数限制|仅受字节数限制|  
|GROUP BY WITH CUBE 或 WITH ROLLUP 语句中的列数或表达式数目|10|10|  
|每个索引键的列数<br /><br /> 注意： 如果表包含一个或多个 XML 索引，用户表的聚集键是限制为 15 列因为 XML 列添加到主 XML 索引的聚集键。 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，可以将非键列包含在非聚集索引，以避免 16 键列的最大限制。 有关详细信息，请参阅 [Create Indexes with Included Columns](../relational-databases/indexes/create-indexes-with-included-columns.md)。|16|16|  
|每个外键的列数|16|16|  
|每个主键的列数|16|16|  
|每个非宽表的列数|1,024|1,024|  
|每个宽表的列数|30,000|30,000|  
|每个 SELECT 语句的列数|4,096|4,096|  
|每个 INSERT 语句的列数|4096|4096|  
|每个客户端的连接个数|已配置连接的最大值|已配置连接的最大值|  
|数据库大小|524,272 TB|524,272 TB|  
|每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|32,767|32,767|  
|每个数据库的文件组个数|32,767|32,767|  
|每个数据库的内存优化数据文件组个数|不支持|@shouldalert|  
|每个数据库的文件个数|32,767|32,767|  
|文件大小（数据）|16 TB|16 TB|  
|文件大小（日志）|2 TB|2 TB|  
|每个数据库的内存优化数据文件个数|不支持|4.096|  
|每个内存优化数据文件的差异文件|不支持|@shouldalert|  
|每个表的外键表引用数<br /><br /> 注意： 尽管表可以包含无限的数量的 FOREIGN KEY 约束，但建议最大值为 253。 根据承载 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的硬件配置，指定额外的 FOREIGN KEY 约束对查询优化器的处理而言可能开销很大。|253|253|  
|标识符长度（以字符计）|128|128|  
|每台计算机的实例数|所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本的独立服务器上为 50 个实例。<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 25 个实例在故障转移群集时使用的共享的群集磁盘的存储选项作为群集安装支持[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]支持 50 个实例在故障转移群集，如果选择 SMB 文件共享作为你的群集安装的存储选项有关详细信息，请参阅[的硬件和软件要求安装 SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)。|独立服务器上为 50 个实例。<br /><br /> 在使用共享群集磁盘作为您的群集安装的存储选项时，在故障转移群集上支持 25 个实例。如果您为群集安装选择 SMB 文件共享作为存储选项，则 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在故障转移群集上支持 50 个实例。|  
|每个内存优化表的索引个数|不支持|8|  
|包含 SQL 语句的字符串的长度（批大小）<br /><br /> 注意： 网络数据包大小是使用应用程序和关系之间进行通信的表格格式数据流 (TDS) 数据包的大小[!INCLUDE[ssDE](../includes/ssde-md.md)]。 默认的数据包大小为 4 KB，由“网络数据包大小”配置选项控制。|65,536 * 网络数据包大小|65,536 * 网络数据包大小|  
|每个连接的锁数|每个服务器的最大锁数|每个服务器的最大锁数|  
|每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> 注意： 此值是针对静态锁分配。 动态锁仅受内存限制。|最多 2,147,483,647|仅受内存限制|  
|嵌套存储过程级别数<br /><br /> 注意： 如果存储的过程访问 64 个以上的数据库，或者交替的数据库多于 2，您将收到错误。|32|32|  
|嵌套子查询个数|32|32|  
|嵌套触发器层数|32|32|  
|每个表的非聚集索引数|999|999|  
|存在以下任意子句的情况下 GROUP BY 子句中的非重复表达式数目：CUBE、ROLLUP、GROUPING SETS、WITH CUBE、WITH ROLLUP|32|32|  
|GROUP BY 子句中的运算符生成的分组集数目|4,096|4,096|  
|每个存储过程的参数个数|2,100|2,100|  
|每个用户定义函数的参数个数|2,100|2,100|  
|每个数据表的 REFERENCE 个数|253|253|  
|每个数据表的行数|受可用存储空间限制|受可用存储空间限制|  
|每个数据库的表数<br /><br /> 注意： 数据库对象包括表、 视图、 存储的过程、 用户定义的函数、 触发器、 规则、 默认值和约束等对象。 数据库中所有对象的数量总和不能超过 2,147,483,647。|受数据库中对象数限制|受数据库中对象数限制|  
|每个分区表或索引的分区数|1,000<br /><br /> **\*\* 重要\* \* **创建具有超过 1,000 个分区的表或索引可以在 32 位系统上，但不是受支持。|15,000|  
|非索引列的统计信息条数|30,000|30,000|  
|每个 SELECT 语句的表个数|仅受可用资源限制|仅受可用资源限制|  
|每个表的触发器数<br /><br /> 注意： 数据库对象包括表、 视图、 存储的过程、 用户定义的函数、 触发器、 规则、 默认值和约束等对象。 数据库中所有对象的数量总和不能超过 2,147,483,647。|受数据库中对象数限制|受数据库中对象数限制|  
|每个 UPDATE 语句（宽表）的列数|4096|4096|  
|用户连接|32,767|32,767|  
|XML 索引|249|249|  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具对象  
 下表指定了在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具中测试的各种对象的最大大小和最大数量。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具对象|最大大小/数量[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]（32 位）|最大大小/数量 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] （64 位）|  
|----------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具的计算机数（物理计算机或虚拟计算机）|100|100|  
|每台计算机的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例数|5|5|  
|每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例总数|200*|200*|  
|每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的用户数据库数（包括数据层应用程序）|50|50|  
|每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具的用户数据库总数|1,000|1,000|  
|每个数据库的文件组数|@shouldalert|@shouldalert|  
|每个文件组的数据文件数|@shouldalert|@shouldalert|  
|每个数据库的日志文件数|@shouldalert|@shouldalert|  
|每台计算机的卷数|3|3|  
  
 * 的托管实例的最大数[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]受[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实用程序可能根据服务器的硬件配置而有所不同。 有关入门信息，请参阅 [SQL Server 实用工具功能和任务](../relational-databases/manage/sql-server-utility-features-and-tasks.md)。 并非在每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本中均提供 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 实用工具控制点。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据层应用程序对象  
 下表指定在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据层应用程序 (DAC) 中测试的各种对象的最大大小和最大数量。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC 对象|最大大小/数量[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]（32 位）|最大大小/数量 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] （64 位）|  
|------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|每个 DAC 的数据库数|@shouldalert|@shouldalert|  
|每个 DAC 的对象数*|受数据库中对象数或可用内存限制。|受数据库中对象数或可用内存限制。|  
  
 *限制中包含的对象类型为用户、表、视图、存储过程、用户定义函数、用户定义数据类型、数据库角色、架构和用户定义表类型。  
  
##  <a name="Replication"></a> 复制对象  
 下表指定了在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 复制中定义的各种对象的最大大小和最大数量。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 复制对象|最大大小/数量 － SQL Server（32 位）|最大大小/数量 SQL Server（64 位）|  
|--------------------------------------------------|---------------------------------------------------|---------------------------------------------------|  
|项目（合并发布）|256|256|  
|项目（快照发布或事务发布）|32,767|32,767|  
|表中的列数*（合并发布）|246|246|  
|表中的列数**（[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 快照发布或事务发布）|1,000|1,000|  
|表中的列数**（Oracle 快照发布或事务发布）|995|995|  
|行筛选器中使用的列的字节数（合并发布）|1,024|1,024|  
|行筛选器中使用的列的字节数（快照发布或事务发布）|8,000|8,000|  
  
 *如果将行跟踪用于冲突检测（默认设置），则基表最多可以包含 1,024 列，但必须从项目中对这些列进行筛选，以便最多可发布 246 列。 如果使用列跟踪，则基表最多可包含 246 列。  
  
 **基表可以包含发布数据库中允许的最大数量的列（在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中为 1,024），但如果这些列的数目超过为发布类型指定的最大值，则必须从项目中筛选这些列。  
  
## <a name="see-also"></a>请参阅  
 [硬件和软件要求安装 SQL Server 2014 的](install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [系统配置检查器的检查参数](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [SQL Server 实用工具功能和任务](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
