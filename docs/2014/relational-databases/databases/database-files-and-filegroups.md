---
title: 数据库文件和文件组 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 780bfc2f1a9c1654f913995a84460f85e19d386a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205459"
---
# <a name="database-files-and-filegroups"></a>数据库文件和文件组
  每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库至少具有两个操作系统文件：一个数据文件和一个日志文件。 数据文件包含数据和对象，例如表、索引、存储过程和视图。 日志文件包含恢复数据库中的所有事务所需的信息。 为了便于分配和管理，可以将数据文件集合起来，放到文件组中。  
  
## <a name="database-files"></a>数据库文件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库具有三种类型的文件，如下表所示：  
  
|文件|Description|  
|----------|-----------------|  
|主|主要数据文件包含数据库的启动信息，并指向数据库中的其他文件。 用户数据和对象可存储在此文件中，也可以存储在次要数据文件中。 每个数据库有一个主要数据文件。 主要数据文件的建议文件扩展名是 .mdf。|  
|辅助副本|次要数据文件是可选的，由用户定义并存储用户数据。 通过将每个文件放在不同的磁盘驱动器上，次要文件可用于将数据分散到多个磁盘上。 另外，如果数据库超过了单个 Windows 文件的最大大小，可以使用次要数据文件，这样数据库就能继续增长。<br /><br /> 次要数据文件的建议文件扩展名是 .ndf。|  
|事务日志|事务日志文件保存用于恢复数据库的日志信息。 每个数据库必须至少有一个日志文件。 事务日志的建议文件扩展名是 .ldf。|  
  
 例如，可以创建一个简单的数据库 **Sales** ，其中包括一个包含所有数据和对象的主要文件和一个包含事务日志信息的日志文件。 也可以创建一个更复杂的数据库 **Orders** ，其中包括一个主要文件和五个次要文件。 数据库中的数据和对象分散在所有六个文件中，而四个日志文件包含事务日志信息。  
  
 默认情况下，数据和事务日志被放在同一个驱动器上的同一个路径下。 这是为处理单磁盘系统而采用的方法。 但是，在生产环境中，这可能不是最佳的方法。 建议将数据和日志文件放在不同的磁盘上。  
  
## <a name="filegroups"></a>文件组  
 每个数据库有一个主要文件组。 此文件组包含主要数据文件和未放入其他文件组的所有次要文件。 可以创建用户定义的文件组，用于将数据文件集合起来，以便于管理、数据分配和放置。  
  
 例如，可以分别在三个磁盘驱动器上创建三个文件 Data1.ndf、Data2.ndf 和 Data3.ndf，然后将它们分配给文件组 **fgroup1**。 然后，可以明确地在文件组 **fgroup1**上创建一个表。 对表中数据的查询将分散到三个磁盘上，从而提高了性能。 通过使用在 RAID（独立磁盘冗余阵列）条带集上创建的单个文件也能获得同样的性能提高。 但是，文件和文件组使您能够轻松地在新磁盘上添加新文件。  
  
 下表列出了存储在文件组中的所有数据文件。  
  
|文件组|Description|  
|---------------|-----------------|  
|主|包含主要文件的文件组。 所有系统表都被分配到主要文件组中。|  
|用户定义|用户首次创建数据库或以后修改数据库时明确创建的任何文件组。|  
  
### <a name="default-filegroup"></a>默认文件组  
 如果在数据库中创建对象时没有指定对象所属的文件组，对象将被分配给默认文件组。 不管何时，只能将一个文件组指定为默认文件组。 默认文件组中的文件必须足够大，能够容纳未分配给其他文件组的所有新对象。  
  
 PRIMARY 文件组是默认文件组，除非使用 ALTER DATABASE 语句进行了更改。 但系统对象和表仍然分配给 PRIMARY 文件组，而不是新的默认文件组。  
  
## <a name="related-content"></a>相关内容  
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
 [ALTER DATABASE 文件和文件组选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
 [数据库分离和附加 (SQL Server)](database-detach-and-attach-sql-server.md)  
  
  
