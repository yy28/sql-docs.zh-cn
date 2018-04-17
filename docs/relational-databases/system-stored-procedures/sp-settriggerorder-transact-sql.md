---
title: sp_settriggerorder (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73a6c088b2d33c77877cadf6a80f030f8faeeaef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spsettriggerorder-transact-sql"></a>sp_settriggerorder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定第一个激发或最后一个激发的 AFTER 触发器。 在第一个和最后一个触发器之间激发的 AFTER 触发器将按未定义的顺序执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@triggername=** ] [ *triggerschema ***。**]*triggername * * ***  
 要设置或更改其顺序的触发器的名称及其所属的架构（如果适用）。 [*triggerschema ***。**]*triggername * 是**sysname**。 如果名称与触发器不对应，或者名称与 INSTEAD OF 触发器对应，则该过程将返回错误。 *triggerschema*不能指定 DDL 或登录触发器。  
  
 [ @order= ] 'value'****  
 触发器的新顺序的设置。 *值*是**varchar(10)**而且它可以是以下值之一。  
  
> [!IMPORTANT]  
>  **第一个**和**最后一个**触发器必须是两个不同的触发器。  
  
|“值”|Description|  
|-----------|-----------------|  
|**第一个**|触发器被第一个触发。|  
|**上一次**|触发器被最后一个触发。|  
|**InclusionThresholdSetting**|触发器以未定义的顺序触发。|  
  
 [  **@stmttype=** ] *****statement_type*****  
 指定触发触发器的 SQL 语句。 *statement_type*是**varchar(50)**和可以插入、 更新、 删除、 登录，或任何[!INCLUDE[tsql](../../includes/tsql-md.md)]中列出的语句事件[DDL 事件](../../relational-databases/triggers/ddl-events.md)。 不能指定事件组。  
  
 触发器可以指定为**第一个**或**最后一个**语句类型仅后该触发器已被定义为该语句类型的触发器的触发器。 例如，触发**TR1**可以指定**第一个**表插入**T1**如果**TR1**定义为 INSERT 触发器。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]如果返回错误**TR1**，其中已被定义为 INSERT 触发器，仅被设置为**第一个**，或**最后一个**，UPDATE 语句的触发器。 有关详细信息，请参见“备注”部分。  
  
 **@namespace=** { **'DATABASE'** | **SERVER** |NULL}  
 当*triggername*是 DDL 触发器， **@namespace**指定是否*triggername*创建与数据库作用域或服务器范围。 如果*triggername*是登录触发器，必须指定服务器。 有关 DDL 触发器作用域的详细信息，请参阅[DDL 触发器](../../relational-databases/triggers/ddl-triggers.md)。 如果未指定，或指定 NULL，则*triggername*是 DML 触发器。  
  
||  
|-|  
|SERVER 适用于：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
## <a name="return-code-values"></a>返回代码值  
 0 （成功） 和 1 （失败）  
  
## <a name="remarks"></a>注释  
  
## <a name="dml-triggers"></a>DML 触发器  
 可能只有一个**第一个**和一个**最后一个**为单个表上每个语句的触发器。  
  
 如果**第一个**表、 数据库或服务器上已经定义了触发器，不能指定为新触发器**第一个**为相同的表、 数据库或服务器相同*statement_type*. 此限制也适用**最后一个**触发器。  
  
 复制将为包含在立即更新订阅或排队更新订阅中的任意表自动生成第一个触发器。 复制要求其触发器为第一个触发器。 在尝试将带有第一个触发器的表包含在立即更新订阅或排队更新订阅中时，复制将引发错误。 如果在表已经包含在订阅中之后尝试使某个触发器成为第一个触发器， **sp_settriggerorder** 将返回错误。 如果在复制触发器上使用 ALTER TRIGGER 或者使用**sp_settriggerorder**若要更改复制触发器绑定到**最后一个**或**无**触发器，订阅执行无法正常工作。  
  
## <a name="ddl-triggers"></a>DDL 触发器  
 如果与数据库作用域的 DDL 触发器和 DDL 触发器具有服务器作用域存在对同一事件，你可以指定这两个触发器是**第一个**触发器或**最后一个**触发器。 但是，服务器作用域的触发器始终最先触发。 一般情况下，同一事件中 DDL 触发器的执行顺序如下：  
  
1.  服务器级触发器标记**第一个**。  
  
2.  其他服务器级触发器。  
  
3.  服务器级触发器标记**最后一个**。  
  
4.  数据库级别触发器标记**第一个**。  
  
5.  其他数据库级触发器。  
  
6.  数据库级别触发器标记**最后一个**。  
  
## <a name="general-trigger-considerations"></a>常规触发器注意事项  
 如果 ALTER TRIGGER 语句更改了第一个或最后一个触发器，**第一个**或**最后一个**最初在触发器上设置的属性已删除，并且值将由替换**无**。 必须通过使用重置顺序值**sp_settriggerorder**。  
  
 如果同一个触发器必须指定为多个语句类型，第一个或最后一个顺序**sp_settriggerorder**必须为每个语句类型执行。 此外，该触发器之前，必须首先定义语句类型可以将指定为**第一个**或**最后一个**触发器来激发该语句类型。  
  
## <a name="permissions"></a>权限  
 若要设置具有服务器作用域（使用 ON ALL SERVER 创建）的 DDL 触发器或登录触发器的顺序，需要具有 CONTROL SERVER 权限。  
  
 若要设置具有数据库作用域（使用 ON DATABASE 创建）的 DDL 触发器的顺序，需要具有 ALTER ANY DATABASE DDL TRIGGER 权限。  
  
 若要设置 DML 触发器的顺序，需要对要在其中定义该触发器的表或视图具有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>A. 设置 DML 触发器的触发顺序  
 以下示例指定触发器 `uSalesOrderHeader` 是对 `UPDATE` 表执行 `Sales.SalesOrderHeader` 操作后触发的第一个触发器。  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>B. 设置 DDL 触发器的触发顺序  
 以下示例指定触发器 `ddlDatabaseTriggerLog` 是对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库执行 `ALTER_TABLE` 操作后触发的第一个触发器。  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
