---
title: sp_helptrigger (TRANSACT-SQL) |Microsoft 文档
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
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 003d14b4c74775a891599f2c3a7451e6bf1928ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sphelptrigger-transact-sql"></a>sp_helptrigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回对当前数据库的指定表定义的 DML 触发器的类型。 sp_helptrigger 不能用于 DDL 触发器。 查询[系统存储过程](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)改用目录视图。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@tabname=** ] *****表*****  
 当前数据库中将为其返回触发器信息的表的名称。 *表*是**nvarchar(776)**，无默认值。  
  
 [ **@triggertype=** ] **'***type***'**  
 将为其返回有关信息的 DML 触发器的类型。 *类型*是**char(6)**，默认值为 NULL，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**DELETE**|返回 DELETE 触发器信息。|  
|**INSERT**|返回 INSERT 触发器信息。|  
|**UPDATE**|返回 UPDATE 触发器信息。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 下表显示了结果集中包含的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|触发器的名称。|  
|**trigger_owner**|**sysname**|对其定义触发器的表的所有者名称。|  
|**isupdate**|**int**|1=UPDATE 触发器<br /><br /> 0=不是 UPDATE 触发器|  
|**isdelete**|**int**|1=DELETE 触发器<br /><br /> 0=不是 DELETE 触发器|  
|**isinsert**|**int**|1=INSERT 触发器<br /><br /> 0=不是 INSERT 触发器|  
|**isafter**|**int**|1=AFTER 触发器<br /><br /> 0=不是 AFTER 触发器|  
|**isinsteadof**|**int**|1=INSTEAD OF 触发器<br /><br /> 0=不是 INSTEAD OF 触发器|  
|**trigger_schema**|**sysname**|该触发器所属的架构的名称。|  
  
## <a name="permissions"></a>权限  
 需要[元数据可见性配置](../../relational-databases/security/metadata-visibility-configuration.md)对表的权限。  
  
## <a name="examples"></a>示例  
 以下示例执行 `sp_helptrigger` 以生成有关对 `Person.Person` 表的触发器的信息。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER (Transact-SQL)](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
