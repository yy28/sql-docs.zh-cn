---
title: 经过修改的功能（包含数据库）| Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database, modifications to DBs
ms.assetid: a2942509-39a2-4903-b504-ae80a300a9de
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f78f4bdf08b9a5caf9b2654289bf181080efff02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871511"
---
# <a name="modified-features-contained-database"></a>经过修改的功能（包含数据库）
  为了获得部分包含的数据库的支持，已对以下功能进行了修改。 经常会对功能进行修改，以便它们不会超出数据库范围。  
  
 有关详细信息，请参阅 [Contained Databases](contained-databases.md)。  
  
## <a name="alter-database"></a>ALTER DATABASE  
  
### <a name="application-level"></a>应用程序级别  
 在包含数据库内部使用 ALTER DATABASE 语句时，其语法不同于用于非包含数据库的语法。 这种差异包括对语句元素的限制超出了数据库级别而作用于实例。 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
### <a name="instance-level"></a>实例级别  
 在包含数据库外部使用时，ALTER DATABASE 的语法与用于非包含数据库时不同。 这些更改可防止超出数据库范围。 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="create-database"></a>CREATE DATABASE  
 包含数据库的 CREATE DATABASE 语法与非包含数据库的不同。 有关新的语法要求和考虑事项的信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)。  
  
## <a name="temporary-tables"></a>临时表  
 包含数据库中允许使用局部临时表，但它们的行为不同于非包含数据库中的局部临时表。 在非包含数据库中，临时表数据是按照 **tempdb**的排序规则调整的。 在包含数据库中，临时表数据是按照包含数据库的排序规则调整的。  
  
 与临时表相关联的所有元数据（例如表名称和列名称、索引等）将在目录排序规则中。  
  
 命名约束可能不在临时表中使用。  
  
 临时表可能不引用用户定义类型、XML 架构集合或用户定义函数。  
  
## <a name="collation"></a>排序规则  
 在非包含数据库模型中，有三种不同的排序规则：数据库排序规则、 实例排序规则和 tempdb 排序规则。 包含数据库只使用两种排序规则：数据库排序规则和新目录排序规则。 有关包含数据库排序规则的详细信息，请参阅 [Contained Database Collations](contained-database-collations.md) 。  
  
## <a name="user-options"></a>用户选项  
 启用包含数据库时，对于 [的实例而言，](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) user options Option [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须设置为 0。  
  
## <a name="see-also"></a>请参阅  
 [Contained Database Collations](contained-database-collations.md)   
 [Contained Databases](contained-databases.md)  
  
  
