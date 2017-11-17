---
title: "ALTER TRIGGER (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER TRIGGER
- ALTER_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, modifying
- triggers [SQL Server], modifying
- modifying triggers
- ALTER TRIGGER statement
- DML triggers, modifying
ms.assetid: 2a99c7c1-ac2f-4637-aa7c-3d1bf514e500
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ae43399e1154e326ccee3d8760d59c71b73de5b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-trigger-transact-sql"></a>ALTER TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  修改 CREATE TRIGGER 语句以前创建的 DML、DDL 或登录触发器的定义。 触发器是通过使用 CREATE TRIGGER 创建的。 它们可直接从创建[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或从方法中创建的程序集[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]公共语言运行时 (CLR) 并上载到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 ALTER TRIGGER 语句中使用的参数的详细信息，请参阅[CREATE TRIGGER &#40;Transact SQL &#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table | view )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
[ NOT FOR REPLICATION ]   
AS { sql_statement [ ; ] [ ...n ] | EXTERNAL NAME <method specifier>   
[ ; ] }   
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table 
-- (DML Trigger on memory-optimized tables)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table  )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [ ...n ] }   
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ <EXECUTE AS Clause> ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, 
-- or UPDATE statement (DDL Trigger)  
  
ALTER TRIGGER trigger_name   
ON { DATABASE | ALL SERVER }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement [ ; ] | EXTERNAL NAME <method specifier>   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on a LOGON event (Logon Trigger)  

ALTER TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  
  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
```  
  
```  
-- Windows Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)   
  
ALTER TRIGGER schema_name. trigger_name   
ON (table | view )   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [...n ] }   
  
<dml_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]   
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, or UPDATE statement (DDL Trigger)   
  
ALTER TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 DML 触发器所属架构的名称。 DML 触发器的作用域是为其创建该触发器的表或视图的架构。 *架构**_name*仅当 DML 触发器和其相应的表或视图所属的默认架构是可选的。 *schema_name*不能指定 DDL 或登录触发器。  
  
 *trigger_name*  
 要修改的现有触发器。  
  
 *表* | *视图*  
 对其执行 DML 触发器的表或视图。 可以选择指定表或视图的完全限定名称。  
  
 DATABASE  
 将 DDL 触发器的作用域应用于当前数据库。 如果指定，该触发器将触发*event_type*或*event_group*当前数据库中发生。  
  
 ALL SERVER  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 将 DDL 或登录触发器的作用域应用于当前服务器。 如果指定，该触发器将触发*event_type*或*event_group*当前服务器中的任何位置发生。  
  
 WITH ENCRYPTION  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 对包含 ALTER TRIGGER 语句的文本的 sys.syscommentssys.sql_modules 条目进行加密。 使用 WITH ENCRYPTION 可以防止将触发器作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制的一部分进行发布。 不能为 CLR 触发器指定 WITH ENCRYPTION。  
  
> [!NOTE]  
>  如果触发器是使用 WITH ENCRYPTION 创建的，则要使该选项保持启用，必须在 ALTER TRIGGER 语句中再次指定。  
  
 EXECUTE AS  
 指定用于执行该触发器的安全上下文。 让您能够控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例在验证对触发器引用的任何数据库对象的权限时使用的用户帐户。  
  
 有关详细信息，请参阅 [EXECUTE AS 子句 (Transact-SQL)](../../t-sql/statements/execute-as-clause-transact-sql.md)。  
  
 NATIVE_COMPILATION  
 指示已本机编译触发器。  
  
 此选项是必需的内存优化表上的触发器。  
  
 SCHEMABINDING  
 可确保不能删除或更改了触发器引用的表。  
  
 此选项，才能使用内存优化表上的触发器，并不支持传统的表上的触发器。  
  
 AFTER  
 指定只有在触发 SQL 语句成功执行后，才会激发触发器。 所有的引用级联操作和约束检查都成功完成后，才能激发此触发器。  
  
 如果仅指定了 FOR 关键字，那么 AFTER 是默认设置。  
  
 只能对表定义 DML AFTER 触发器。  
  
 INSTEAD OF  
 指定执行 DML 触发器而不是触发 SQL 语句，因此，其优先级高于触发语句的操作。 不能为 DDL 或登录触发器指定 INSTEAD OF。  
  
 对于表或视图，每个 INSERT、UPDATE 或 DELETE 语句最多可定义一个 INSTEAD OF 触发器。 但是，可以为具有自己的 INSTEAD OF 触发器的多个视图定义视图。  
  
 不允许在使用 WITH CHECK OPTION 创建的视图上定义 INSTEAD OF 触发器。 将 INSTEAD OF 触发器添加到为其指定了 WITH CHECK OPTION 的视图时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将引发错误。 用户必须用 ALTER VIEW 删除该选项后才能定义 INSTEAD OF 触发器。  
  
 { [DELETE] [,] [INSERT] [,] [UPDATE] } | { [INSERT] [,] [UPDATE]}  
 指定数据修改语句在试图修改表或视图时，激活 DML 触发器。 必须至少指定一个选项。 在触发器定义中允许使用以任意顺序组合的这些选项。 如果指定的选项多于一个，需用逗号分隔这些选项。  
  
 对于 INSTEAD OF 触发器，不允许对具有指定级联操作 ON DELETE 的引用关系的表使用 DELETE 选项。 同样，也不允许对具有指定级联操作 ON UPDATE 的引用关系的表使用 UPDATE 选项。 有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 *event_type*  
 执行之后将导致激发 DDL 触发器的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语言事件的名称。 中列出的 DDL 触发器的有效事件[DDL 事件](../../relational-databases/triggers/ddl-events.md)。  
  
 *event_group*  
 预定义的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语言事件分组的名称。 在执行任何后激发 DDL 触发器[!INCLUDE[tsql](../../includes/tsql-md.md)]所属的语言事件*event_group*。 DDL 触发器的有效事件组中列出[DDL 事件组](../../relational-databases/triggers/ddl-event-groups.md)。 ALTER TRIGGER 已经完成运行后, *event_group*还可充当宏通过将事件类型添加它 sys.trigger_events 目录视图的介绍。  
  
 NOT FOR REPLICATION  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 表示当复制代理修改触发器所涉及的表时，不应执行该触发器。  
  
 *sql_statement*  
 触发条件和操作。  
  
 为内存优化表上的触发器的唯一*sql_statement*允许在顶级块是原子块。 T-SQL 原子块内部允许受 T-SQL 本机过程内允许的限制。  
  
 外部名称\<method_specifier >  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定要与触发器绑定的程序集的方法。 该方法不能带有任何参数，并且必须返回空值。 *class_name*必须为有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符并且必须具有程序集可见性的程序集中的类作为存在。 该类不能为嵌套类。  
  
## <a name="remarks"></a>注释  
 ALTER TRIGGER 有关的详细信息，请参阅中的备注[CREATE TRIGGER &#40;Transact SQL &#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
> [!NOTE]  
>  EXTERNAL_NAME 和 ON_ALL_SERVER 选项在包含数据库中不可用。  
  
## <a name="dml-triggers"></a>DML 触发器  
 通过表和视图上的 INSTEAD OF 触发器，ALTER TRIGGER 支持可手动更新的视图。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以相同的方式对所有类型的触发器（AFTER、INSTEAD-OF）应用 ALTER TRIGGER。  
  
 可以使用 sp_settriggerorder 来指定要对表执行的第一个和最后一个 AFTER 触发器。 对一个表只能指定第一个和最后一个 AFTER 触发器。 如果在同一个表上还有其他 AFTER 触发器，这些触发器将随机执行。  
  
 如果 ALTER TRIGGER 语句更改了第一个或最后一个触发器，将删除所修改触发器上设置的第一个或最后一个属性，并且必须使用 sp_settriggerorder 重置顺序值。  
  
 只有在成功执行触发 SQL 语句之后，才会执行 AFTER 触发器。 判断执行成功的标准是：执行了所有与已更新对象或已删除对象相关联的引用级联操作和约束检查。 AFTER 触发器操作要检查触发语句的效果，也包括所有由触发语句引起的 UPDATE 和 DELETE 引用级联操作。  
  
 如果一个子表或引用表上的 DELETE 操作是由于父表的 CASCADE DELETE 操作所引起的，并且子表上定义了 DELETE 的 INSTEAD OF 触发器，那么将忽略该触发器并执行 DELETE 操作。  
  
## <a name="ddl-triggers"></a>DDL 触发器  
 与 DML 触发器不同，DDL 触发器的作用域不是架构。 因此，在查询有关 DDL 触发器的元数据时，不能使用 OBJECT_ID、OBJECT_NAME、OBJECTPROPERTY 和 OBJECTPROPERTY(EX)。 请改用目录视图。 有关详细信息，请参阅[将信息获取有关 DDL 触发器](../../relational-databases/triggers/get-information-about-ddl-triggers.md)。  
  
## <a name="logon-triggers"></a>登录触发器  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 不支持针对登录事件的触发器。  
  
## <a name="permissions"></a>Permissions  
 若要更改 DML 触发器，需要对于定义该触发器所在的表或视图拥有 ALTER 权限。  
  
 若要更改定义了服务器范围 (ON ALL SERVER) 的 DDL 触发器或者更改登录触发器，需要对该服务器拥有 CONTROL SERVER 权限。 若要更改定义了数据库范围 (ON DATABASE) 的 DDL 触发器，需要对当前数据库拥有 ALTER ANY DATABASE DDL TRIGGER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 DML 触发器在 AdventureWorks 2012 数据库中，当用户尝试添加或更改中的数据打印到客户端用户定义的消息`SalesPersonQuotaHistory`表。 然后使用 `ALTER TRIGGER` 对该触发器进行了修改，以便只将其应用于 `INSERT` 活动。 此触发器十分有用，因为它可提醒向此表中插入行或更新行的用户也要通知 `Compensation` 部门。  
  
```  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  

-- Now, change the trigger.  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DROP TRIGGER (Transact-SQL)](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER (Transact-SQL)](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER (Transact-SQL)](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_helptrigger (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [创建存储过程](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sp_addmessage &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [事务](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [获取有关 DML 触发器的信息](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [获取有关 DDL 触发器的信息](../../relational-databases/triggers/get-information-about-ddl-triggers.md)   
 [sys.triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events (Transact-SQL)](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)   
 [对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  

