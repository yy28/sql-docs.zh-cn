---
title: "不兼容的访问功能 (AccessToSQL) |Microsoft 文档"
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
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b60bab1d71142a74c8558ce05a6ca96451e7cfc9
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="incompatible-access-features-accesstosql"></a>不兼容的访问功能 (AccessToSQL)
并非所有访问数据库功能都都与兼容[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]以及具有不同的保留关键字集的访问权限。 问题如这些可能会阻止成功迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 使用下表来了解可能的迁移问题，有关它们的信息可以执行什么操作。  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>数据库的设置或可能会对迁移造成影响的功能  
  
|访问数据库的设置或功能|迁移问题|  
|--------------------------------------|-------------------|  
|访问表没有唯一索引。|如果没有唯一索引的表迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，不能在迁移之后修改表。 这可能导致应用程序兼容性问题。<br /><br />在转换访问数据库对象时，输出窗口将列出没有唯一索引的任何访问表。<br /><br />你可以配置访问上添加为主键[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]转换期间的表。 有关详细信息，请参阅[项目设置 （转换）](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)。|  
|访问表已复制列。|如果将包含复制系统列访问表迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Jet 复制功能在迁移后将会中断。<br /><br />迁移后，请考虑使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]复制来维护你的数据库的同步的副本。|  
|具有唯一索引的访问表包含多个 null 值。|无法将具有与多个 null 值的唯一索引的访问表转移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，因为在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，唯一索引不允许多个 null 值。 这些表的情况下，迁移将会失败。<br /><br />SSMA 将标记中评估报告，此问题。 若要创建评估报表，请参阅[评估访问数据库对象的转换](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441)。<br /><br />如果存在此问题，则必须确保主键不具有重复的 null 值。 或者，你必须删除 primary key 或包含多个 null 值的唯一索引。|  
|访问表包含外的日期值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]范围。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Datetime**接受类型的日期范围内的 1 到 31 日的 1753 年 1 月仅 9999。 访问接受范围内的 1 年 1 月 100 到 31 日的日期 9999。<br /><br />SSMA 将标记中评估报告，此问题。 若要创建评估报表，请参阅[评估访问数据库对象的转换](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441)。<br /><br />你可以配置如何 SSMA 解决日期都外[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]范围。 有关详细信息，请参阅[项目设置 （迁移）](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)。|  
|在 Access 中的索引长度超过 900 个字节。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]索引具有索引键列的总大小为 900 字节的限制。 如果你访问的表使用更大的索引，SSMA 将显示警告。<br /><br />如果继续进行数据迁移，迁移可能会失败。|  
|访问对象名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]关键字，或包含特殊字符。|访问和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]具有不同的保留的关键字和特殊字符。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]将接受使用命名的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]关键字或包含特殊字符，如果你使用被括号括起来或带引号的标识符，例如，"select"或 [选择].p。 有关详细信息，请参阅 》 中"带分隔符标识符 （数据库引擎）"[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。<br /><br />**注意：**若要使用引号分隔标识符，SET QUOTED_IDENTIFIER 必须为 ON。<br /><br />例如，`CREATE TABLE [schema](c1 [FOR])`为有效的语句，即使**架构**和**为**都是保留的关键字。 此外，`CREATE TABLE [xxx*yyy](c1 x&y)`即使表和列名称包含特殊字符是有效的语句，  **\&#42;**和 **&amp;** 。<br /><br />引用这些对象的所有查询也必须都使用随括号或引号内的名称。 例如，以下查询`SELECT * FROM schema`将失败。 正确的查询是： `SELECT * FROM [schema]`。<br /><br />在转换访问数据库对象时，输出窗格将列出使用关键字或特殊字符的任何访问表。 你可以修改表在 Access 中，然后删除并再次添加数据库也可以修改，以便查询使用括号或引号分隔标识符引用这些对象的查询。 如果不修改你的查询，你访问应用程序可能返回错误或具有其他问题。|  
|主键/外键关系的不同字段大小。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不支持链接具有不同的数据类型或大小的外键约束的列的 Jet 的功能。<br /><br />在转换访问数据库对象时，输出窗口将列出将不会转换到任何主键/外键约束[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 以便它们匹配，然后删除并重新添加 Access 数据库，可以更改数据类型和上访问列大小。 或者，你可以迁移数据，虽然这些约束将不会创建在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|访问关系中的引用的表具有主键和唯一索引都不。|访问接受其中被引用的表没有主键或唯一索引的表之间的关系。 但是，这不支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br />在转换访问数据库对象时，输出窗口将列出具有关系但没有主键或唯一索引的任何表。 您可以修改以添加主键或唯一索引，然后删除并重新添加 Access 数据库的表。 或者，你可以迁移数据，尽管表之间的关系将会中断。|  
|访问表具有超链接列。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不支持**超链接**列。 相反，列一样访问 memo 列。 默认情况下，这些列将转换为**nvarchar (max)**中的列[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 你可以自定义映射。 有关详细信息，请参阅[映射源和目标数据类型](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)。|  
|默认值或验证规则表达式包含访问函数，不能转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。|访问默认表达式或验证规则可能包括访问系统函数或未映射到的用户定义函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 使用不映射到的函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 将阻止你从加载默认表达式或验证规则到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。|  
  
## <a name="see-also"></a>另請參閱  
[为迁移准备的 Access 数据库](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

