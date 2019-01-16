---
title: System_function_schema 中不允许用户定义的函数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b7c21521fbdd4a4e80ed196c67c72f790341f020
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254272"
---
# <a name="user-defined-functions-are-not-allowed-in-systemfunctionschema"></a>system_function_schema 中不允许使用用户定义函数
  升级顾问检测到的未记录的用户所拥有的用户定义函数**system_function_schema**。 不能通过指定此用户创建用户定义的系统功能。 **System_function_schema**用户名不存在，并且这是与此名称关联的用户 ID (UID = 4) 保留供**sys**架构和被限制为仅供内部使用。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 系统对象存储和访问都已更改为以下方式：  
  
-   系统对象存储在只读**资源**数据库，然后直接更新系统对象不允许使用。  
  
     在逻辑上却显示系统对象**sys**每个数据库的架构。 这样便保留了通过指定由单个部分组成的函数名称来从任何数据库调用系统函数的能力。 例如，语句 `SELECT * FROM fn_helpcollations()` 可以从任何数据库运行。  
  
-   未记录的用户**system_function_schema**已删除。  
  
-   与 ID 关联的用户**system_function_schema** (UID = 4) 保留供**sys**架构和被限制为仅供内部使用。  
  
 这些更改将对用户定义系统函数具有下列影响：  
  
-   引用的数据定义语言 (DDL) 语句**system_function_schema**将失败。 例如，语句`CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` ...将不会成功。  
  
-   升级到之后[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，所拥有的现有对象**system_function_schema**仅包含在**sys**的架构**主**数据库。 由于不能修改系统对象，因此这些函数可以永远不会更改或删除从**主**数据库。 另外，不能通过仅指定由单个部分组成的函数名称来从其他数据库中调用这些函数。  
  
## <a name="corrective-action"></a>纠正措施  
 在升级之前，请完成以下任务：  
  
1.  更改现有用户定义函数的所有权**dbo**通过使用**sp_changeobjectowner**系统存储过程。  
  
2.  考虑重命名函数，使其不使用前缀“fn_”。 这样会避免与当前或未来的系统函数发生潜在名称冲突。  
  
3.  将修改后的函数的副本添加到使用这些函数的每个数据库中。  
  
4.  替换为对引用**system_function_schema**与**dbo**包含用户定义函数 DDL 语句的所有脚本中。  
  
5.  修改脚本，它们调用这些函数使用两个部分组成的名称 dbo **。**_function_name_，或三部分组成的名称_database_name_**。** dbo。*function_name*。  
  
 有关详细信息，请参阅 SQL Server 联机丛书的下列主题：  
  
-   “sp_changeobjectowner”  
  
-   “用户架构分离”  
  
-   “Resource 数据库”  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)   
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [删除用于修改系统对象的语句](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [删除用于删除系统对象的语句](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
