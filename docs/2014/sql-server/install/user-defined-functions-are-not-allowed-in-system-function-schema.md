---
title: System_function_schema 中不允许使用用户定义的函数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7242f9fda74288a2b7354ac0550ff4966e05c555
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058777"
---
# <a name="user-defined-functions-are-not-allowed-in-system_function_schema"></a>system_function_schema 中不允许使用用户定义函数
  升级顾问检测到由未记录的用户**system_function_schema**拥有的用户定义函数。 不能通过指定此用户创建用户定义的系统功能。 **System_function_schema**用户名不存在，而与此名称关联的用户 ID （UID = 4）将保留用于**sys**架构，且仅限内部使用。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 系统对象存储和访问都已更改为以下方式：  
  
-   系统对象存储在只读**资源**数据库中，不允许直接更新系统对象。  
  
     系统对象在逻辑上出现在每个数据库的**sys**架构中。 这样便保留了通过指定由单个部分组成的函数名称来从任何数据库调用系统函数的能力。 例如，语句 `SELECT * FROM fn_helpcollations()` 可以从任何数据库运行。  
  
-   已删除未记录的用户**system_function_schema** 。  
  
-   与**system_function_schema** （UID = 4）关联的用户 ID 为**sys**架构保留，并且仅限内部使用。  
  
 这些更改将对用户定义系统函数具有下列影响：  
  
-   引用**system_function_schema**的数据定义语言（DDL）语句将失败。 例如，语句 `CREATE FUNCTION system` _ `function` \_ `schema.fn` \_ `MySystemFunction` .。。不会成功。  
  
-   升级到后 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ， **system_function_schema**拥有的现有对象仅包含在**master**数据库的**sys**架构中。 由于无法修改系统对象，因此永远无法更改这些函数或将其从**master**数据库中删除。 另外，不能通过仅指定由单个部分组成的函数名称来从其他数据库中调用这些函数。  
  
## <a name="corrective-action"></a>纠正措施  
 在升级之前，请完成以下任务：  
  
1.  使用**sp_changeobjectowner**系统存储过程将现有用户定义函数的所有权更改为**dbo** 。  
  
2.  考虑重命名函数，使其不使用前缀“fn_”。 这样会避免与当前或未来的系统函数发生潜在名称冲突。  
  
3.  将修改后的函数的副本添加到使用这些函数的每个数据库中。  
  
4.  在包含用户定义函数 DDL 语句的所有脚本中，用**dbo**替换对**system_function_schema**的引用。  
  
5.  修改调用这些函数的脚本，以使用由两部分组成的名称 dbo **。**_function_name_或由三部分组成的名称_database_name_**。** 供.*function_name*。  
  
 有关详细信息，请参阅 SQL Server 联机丛书的下列主题：  
  
-   “sp_changeobjectowner”  
  
-   “用户架构分离”  
  
-   “Resource 数据库”  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)   
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [删除修改系统对象的语句](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [删除用于删除系统对象的语句](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
