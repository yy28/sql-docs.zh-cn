---
title: 在升级过程中，验证是否为所有数据文件和日志文件启用了自动增长 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], size
- data files [SQL Server], size
- tempdb [SQL Server], size
- autogrow [SQL Server]
ms.assetid: a5860904-e2be-4224-8a51-df18a10d3fb9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0217d959759a59e49ce76e4a841c5d52e958e9ce
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091220"
---
# <a name="verify-autogrow-is-turned-on-for-all-data-and-log-files-during-the-upgrade-process"></a>升级期间，确保为所有数据文件和日志文件启用了自动增长功能
  升级顾问检测到未设置为自动增长的数据或日志文件。 新增功能和增强功能需要额外的磁盘空间来用于用户数据库和**tempdb**系统数据库。 为了确保在升级和后续生产操作期间资源可以容纳更大的大小，建议在升级前将所有用户数据和日志文件以及**tempdb**数据和日志文件的自动增长设置为 ON。  
  
 升级并测试工作负载后，可能需要关闭用户数据和日志文件的自动增长，或者相应地对 FILEGROWTH 增量进行调整。 建议对**tempdb**系统数据库保持启用自动增长。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“tempdb 容量规划”。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 **数据文件**  
  
 下表列出对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的更改，这些更改导致用户定义数据文件需要更多的磁盘空间。  
  
|功能|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引入的更改|  
|-------------|-----------------------------------------------------|  
|全文|文档 ID (DOCID) 映射存储在数据文件中，而不是全文目录中。|  
|`text`、`ntext` 和 `image` 列|定义为 `text`、`ntext` 或 `image` 数据类型的大型对象 (LOB) 列要求为每列额外增加 40 字节的磁盘空间。 在每个 LOB 列的第一次更新过程中会出现这种一次性空间增长。|  
|metadata|在每个用户数据库的 PRIMARY 文件组中，将针对数据库对象和用户权限创建和维护附加的系统元数据。 例如，在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，与授权者或被授权者相关联的权限作为位图存储在单独一行中。 位图已扩展为多行。<br /><br /> 在升级过程中，必须有足够的磁盘空间来存储旧元数据和新元数据。 在升级完成后，删除旧的元数据。|  
  
 **事务日志文件**  
  
 下表列出对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的更改，这些更改导致用户定义的事务日志文件需要更多的磁盘空间。  
  
|功能|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引入的更改|  
|-------------|-----------------------------------------------------|  
|还原和恢复|在崩溃恢复的撤消阶段，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许用户访问数据库。 这是因为崩溃发生时未提交的事务将重新获取它们在崩溃前持有的所有锁。 在回滚事务时，它们的锁会防止用户干扰。 必须在事务日志中维护此附加锁定信息。|  
  
 **tempdb 数据和日志文件**  
  
 在的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早期版本中， **tempdb**数据库用于存储下列对象：  
  
-   显式创建的临时对象，例如表、存储过程、表变量或游标。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]创建的内部工作表。  
  
-   创建或重建索引时来自临时排序的结果（如果指定了 SORT_IN_TEMPDB）。  
  
 其他对象也使用**tempdb**数据库。 下表列出了对导致**tempdb**数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和日志文件的额外磁盘空间需求的功能的更改或添加。  
  
|功能|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引入的更改|  
|-------------|-----------------------------------------------------|  
|行版本控制|行版本控制是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的常规框架，可以用于：<br /><br /> 支持触发器：生成触发器中插入的和删除的表。 对任何由触发器修改的行都将生成副本。 这包括由启动触发器的语句修改的行，以及由触发器进行的任何数据修改。 AFTER 触发器使用**tempdb**的版本存储区来保存触发器更改的行的前像。 当您在启用触发器的情况下大容量加载数据时，将在版本存储区中为每一行添加一个副本。<br /><br /> 支持多个活动的结果集 (MARS)。 如果 MARS 会话发出一条数据修改语句（例如 INSERT、UPDATE 或 DELETE）时存在活动的结果集，则对受修改语句影响的行都将生成副本。<br /><br /> 支持指定 ONLINE 选项的索引操作。 联机索引操作使用行版本控制来使索引操作不受其他事务所做的修改的影响。 这就不需要对已经读取的行请求共享锁。 此外，在联机索引操作期间，并发用户更新和删除操作需要对**tempdb**中的版本记录进行空间。<br /><br /> 支持基于行版本控制的事务隔离级别：新的已提交读隔离级别的实现，该实现使用行版本控制来提供语句级读取一致性。 新快照隔离级别，提供事务级的读取一致性。<br /><br /> <br /><br /> 行版本保存在**tempdb**版本存储区中的时间足以满足在基于行版本控制的隔离级别下运行的事务的要求。<br /><br /> 有关行版本控制和版本存储区的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“了解基于行版本控制的隔离级别”主题。|  
|缓存临时表和临时变量元数据|对于缓存在元数据缓存中的临时表和临时变量的每[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]个元数据，将为**tempdb**分配两个额外的页。<br /><br /> 如果存储过程或触发器创建临时表或临时变量，则在存储过程或触发器完成执行时不会删除临时对象， 而是将临时对象截断至一页，并在下次执行过程或触发器时重新使用。|  
|对已分区表的索引|当[!INCLUDE[ssDE](../../includes/ssde-md.md)]执行排序以生成已分区索引时，如果指定了 SORT_IN_TEMPDB 索引选项，则**tempdb**中需要足够的空间来保存每个分区的中间排序运行。|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|[!INCLUDE[ssSB](../../includes/sssb-md.md)]在保留无法保留在内存中的现有对话框上下文（每个对话框大约为 1 KB）时显式使用**tempdb** 。<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)]在查询执行的上下文中通过缓存对象隐式地使用**tempdb** 。 例如，会为计时器事件和后台传递的会话使用工作表。<br /><br /> 数据库邮件、事件通知和查询通知功能会隐式地使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。|  
|大型对象（LOB）数据类型<br /><br /> LOB 变量和参数|`varchar(max)`数据类型`nvarchar(max)`（即**varbinary （max）文本**、 `ntext` `image,`和`xml` ）是大型对象类型。<br /><br /> 如果对数据库启用了基于行版本控制的事务隔离级别并且对大型对象进行了修改，则 LOB 的已更改片段将被复制到**tempdb**中的版本存储区。<br /><br /> 定义为大型对象数据类型的参数存储在**tempdb**中。|  
|公用表表达式（Cte）|执行公用表表达式查询时，会在**tempdb**中创建用于假脱机操作的临时工作表。|  
  
## <a name="corrective-action"></a>纠正措施  
 若要将数据或日志文件设置为自动增长，请修改下列语句以指定数据库的数据和日志。 应当将 FILEGROWTH 增量调整为适合您的环境的值。  
  
```  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = tempdev,  
    FILEGROWTH = 20MB);  
GO  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = templog,  
    FILEGROWTH = 10MB);  
```  
  
 数据文件的默认增量为 1 MB。 日志文件默认为 10%。 建议在设置 FILEGROWTH 增量时遵循以下通用原则：  
  
|文件大小|FILEGROWTH 增量|  
|---------------|--------------------------|  
|0-50MB|10MB|  
|100-200MB|MB|  
|500MB 或更多|10%|  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
