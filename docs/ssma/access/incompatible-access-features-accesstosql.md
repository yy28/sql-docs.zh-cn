---
title: 不兼容的 Access 功能 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 29b5225f95c6b2cb04f42c0e67c504ac2cb20e53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740887"
---
# <a name="incompatible-access-features-accesstosql"></a>不兼容的 Access 功能 (AccessToSQL)
并非所有访问数据库功能都都与兼容[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和访问具有不同的保留关键字集。 问题如这些可能会阻止成功迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 使用下表了解有关可能的迁移问题和如何应对这些信息。  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>数据库设置或可能会影响迁移的功能  
  
|访问数据库的设置或功能|迁移问题|  
|--------------------------------------|-------------------|  
|访问表没有唯一索引。|如果不具有唯一索引的表迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，迁移后，不能修改表。 这可能导致应用程序兼容性问题。<br /><br />在转换访问数据库对象时，输出窗口将列出不具有唯一索引的任何访问表。<br /><br />您可以配置访问上添加主键[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]转换期间的表。 有关详细信息，请参阅[项目设置 （转换）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)。|  
|访问表具有复制的列。|如果包括复制系统列的 Access 表迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，迁移后，Jet 复制功能将被破坏。<br /><br />迁移后，请考虑使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]复制维护的数据库的同步的副本。|  
|具有唯一索引访问表包含多个 null 值。|具有唯一索引与多个 null 值的访问表无法转移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，因为在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，唯一索引不允许多个 null 值。 这些表的情况下，迁移将会失败。<br /><br />SSMA 会标记在评估报告此问题。 若要创建评估报告，请参阅[评估访问数据库对象的转换](assessing-access-database-objects-for-conversion-accesstosql.md)。<br /><br />如果存在此问题，必须确保主键不具有重复的 null 值。 或者，你必须删除 primary key 或包含多个 null 值的唯一索引。|  
|访问表包含外出时的日期值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]范围。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Datetime**类型接受范围 1 到 31 Dec 的 1753 年 1 月中日期仅 9999。 访问接受到 31 年 12 月的 1 年 1 月 100年的范围中的日期到 9999。<br /><br />SSMA 会标记在评估报告此问题。 若要创建评估报告，请参阅[评估访问数据库对象的转换](assessing-access-database-objects-for-conversion-accesstosql.md)。<br /><br />你可以配置如何 SSMA 解决日期的是带[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]范围。 有关详细信息，请参阅[项目设置 （迁移）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。|  
|在访问索引长度超过 900 字节。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引的索引键列的总大小为 900 字节限制。 如果你访问的表使用索引越大，SSMA 将显示一条警告。<br /><br />如果继续进行数据迁移，迁移可能失败。|  
|访问对象名称都[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]关键字，也不能包含特殊字符。|访问和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有不同的保留的关键字和特殊字符。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将接受使用命名的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]关键字或包含特殊字符，如果使用带中括号或带引号的标识符，如"select"或 [选择].p。 有关详细信息，请参阅 》 中"带分隔符标识符 （数据库引擎）"[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。<br /><br />**注意**：若要使用引号分隔标识符，SET QUOTED_IDENTIFIER 必须为 ON。<br /><br />例如，`CREATE TABLE [schema](c1 [FOR])`是一个有效的语句，即使**架构**并**为**是保留的关键字。 此外，`CREATE TABLE [xxx*yyy](c1 x&y)`是一个有效的语句，即使表和列名称包含特殊字符 **\&#42;** 并 **&amp;** 。<br /><br />引用这些对象的所有查询还必须使用括号或引号中都使用的名称。 例如，以下查询`SELECT * FROM schema`将失败。 正确的查询是： `SELECT * FROM [schema]`。<br /><br />在转换访问数据库对象时，输出窗格将列出使用关键字或特殊字符的任何访问表。 您可以修改的表中的访问，然后删除并重新; 添加数据库或者，可以修改，以便查询使用括号或引号分隔标识符引用这些对象的查询。 如果不修改您的查询，将 Access 应用程序可能会返回错误，或有其他问题。|  
|主键/外键关系的不同字段大小。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持链接具有不同的数据类型或大小与外键约束的列的 Jet 的功能。<br /><br />在转换访问数据库对象时，输出窗口将列出不会转换为任何主/外键约束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以更改数据类型和访问列的大小，以便它们匹配，然后删除并重新添加 Access 数据库。 或者，您可以迁移数据，尽管这些约束不能中创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|访问关系中被引用的表没有主键或唯一索引。|访问接受其中所引用的表没有主键或唯一索引的表之间的关系。 但是，这不受[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br />在转换访问数据库对象时，输出窗口将列出任何关系，但不具有主键或唯一索引的表。 您可以更改要添加主键或唯一索引，然后删除并重新添加 Access 数据库的表。 或者，可以将数据迁移尽管表之间的关系将被破坏。|  
|访问表具有超链接列。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持**超链接**列。 相反，列一样访问 memo 列。 默认情况下，这些列将转换为**nvarchar （max)** 中的列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 可以自定义映射。 有关详细信息，请参阅[映射源和目标数据类型](mapping-source-and-target-data-types-accesstosql.md)。|  
|默认值或验证规则表达式包含无法转换为访问函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。|访问默认表达式或验证规则可能包括访问系统函数或用户定义的函数，不会映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 使用不会映射到的函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 将阻止您加载默认表达式或到的验证规则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。|  
  
## <a name="see-also"></a>请参阅  
[为迁移准备 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
