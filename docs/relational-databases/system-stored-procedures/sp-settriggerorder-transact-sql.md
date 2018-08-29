---
title: sp_settriggerorder (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 22e1ef77030c54902f644cc63efc2d972ca8cf03
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43072667"
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
 [  **@triggername=** ] **'**[ *triggerschema ***。**]*triggername * * ***  
 要设置或更改其顺序的触发器的名称及其所属的架构（如果适用）。 [*triggerschema ***。**]* triggername * 是**sysname**。 如果名称与触发器不对应，或者名称与 INSTEAD OF 触发器对应，则该过程将返回错误。 *triggerschema*不能为 DDL 或登录触发器指定。  
  
 [ @order= ] 'value'****  
 触发器的新顺序的设置。 *值*是**varchar(10)** ，可以是下列值中的任何一个。  
  
> [!IMPORTANT]  
>  **第一个**并**最后一个**触发器必须是两个不同的触发器。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**第一个**|触发器被第一个触发。|  
|**上一次**|触发器被最后一个触发。|  
|**无**|触发器以未定义的顺序触发。|  
  
 [  **@stmttype=** ] **'***statement_type*****  
 指定触发触发器的 SQL 语句。 *statement_type*是**varchar(50)** 可以是 INSERT、 UPDATE、 DELETE、 LOGON 或任何[!INCLUDE[tsql](../../includes/tsql-md.md)]中列出的语句事件[DDL 事件](../../relational-databases/triggers/ddl-events.md)。 不能指定事件组。  
  
 触发器可以指定为**第一个**或**最后一个**为某个语句类型才为该语句类型的触发器已定义该触发器的触发器。 例如，触发**TR1**可以指定**第一个**表**T1**如果**TR1**定义为 INSERT 触发器。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]返回一个错误，如果**TR1**，其中已被定义为 INSERT 触发器，仅被设置为**第一个**，或**最后一个**，UPDATE 语句的触发器。 有关详细信息，请参见“备注”部分。  
  
 **@namespace=** { **'DATABASE'** | **SERVER** |NULL}  
 当*triggername*为 DDL 触发器时， **@namespace**指定是否*triggername*创建具有数据库作用域还是服务器作用域。 如果*triggername*是登录触发器，必须指定服务器。 有关 DDL 触发器作用域的详细信息，请参阅[DDL 触发器](../../relational-databases/triggers/ddl-triggers.md)。 如果未指定，或指定 NULL，则*triggername*是 DML 触发器。  
  
||  
|-|  
|SERVER 适用于：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
## <a name="return-code-values"></a>返回代码值  
 0 （成功） 和 1 （失败）  
  
## <a name="remarks"></a>Remarks  
  
## <a name="dml-triggers"></a>DML 触发器  
 可能只有一个**第一个**和一个**最后一个**对单个表的每个语句的触发器。  
  
 如果**第一个**表、 数据库或服务器上已定义触发器，不能指定为新的触发器**第一个**的同一个表、 数据库或服务器的相同*statement_type*. 此限制也适用**最后一个**触发器。  
  
 复制将为包含在立即更新订阅或排队更新订阅中的任意表自动生成第一个触发器。 复制要求其触发器为第一个触发器。 在尝试将带有第一个触发器的表包含在立即更新订阅或排队更新订阅中时，复制将引发错误。 如果在表已经包含在订阅中之后尝试使某个触发器成为第一个触发器， **sp_settriggerorder** 将返回错误。 如果您在复制触发器上使用 ALTER TRIGGER，或使用**sp_settriggerorder**若要更改将复制触发器改**上次**或**None**触发器，订阅执行无法正常工作。  
  
## <a name="ddl-triggers"></a>DDL 触发器  
 如果同一事件上存在具有数据库作用域的 DDL 触发器和具有服务器作用域内的 DDL 触发器，则可以指定这两种触发器是**第一个**触发器或**最后一个**触发器。 但是，服务器作用域的触发器始终最先触发。 一般情况下，同一事件中 DDL 触发器的执行顺序如下：  
  
1.  服务器级触发器标记**第一个**。  
  
2.  其他服务器级触发器。  
  
3.  服务器级触发器标记**最后一个**。  
  
4.  数据库级触发器标记**第一个**。  
  
5.  其他数据库级触发器。  
  
6.  数据库级触发器标记**最后一个**。  
  
## <a name="general-trigger-considerations"></a>常规触发器注意事项  
 如果 ALTER TRIGGER 语句更改了第一个或最后一个触发器，**第一个**或**上次**将删除最初在触发器上设置的属性，并且值被替换**None**。 必须使用重置顺序值**sp_settriggerorder**。  
  
 如果必须将同一触发器指定为多个语句类型的第一个或最后一个顺序**sp_settriggerorder**必须针对每个语句类型执行。 此外，触发器之前，必须首先定义为某个语句类型指定为**第一个**或**最后一个**触发器被激发该语句类型。  
  
## <a name="permissions"></a>Permissions  
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
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
