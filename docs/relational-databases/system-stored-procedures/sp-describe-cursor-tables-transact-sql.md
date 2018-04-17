---
title: sp_describe_cursor_tables (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_tables_TSQL
- sp_describe_cursor_tables
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_tables
ms.assetid: 02c0f81a-54ed-4ca4-aa4f-bb7463a9ab9a
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b18e95e52ff4f7c44f11e9f8010e017c39dd85e4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spdescribecursortables-transact-sql"></a>sp_describe_cursor_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告由服务器游标引用的对象或基表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_describe_cursor_tables   
     [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
     , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
     , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>参数  
 [ @cursor_return=] *output_cursor_variable*输出  
 声明的用于接收游标输出的游标变量的名称。 *output_cursor_variable*是**光标**，没有默认值，且必须与不能与任何游标相关联的 sp_describe_cursor_tables 称为次。 返回的游标是可滚动的动态只读游标。  
  
 [ @cursor_source=] {N'local' |N'global' |N'variable'}  
 指定使用以下哪一名称来指定所报告的游标：本地游标、全局游标或游标变量的名称。 该参数是**nvarchar (30)**。  
  
 [ @cursor_identity=] N*local_cursor_name*  
 由具有 LOCAL 关键字或默认设置为 LOCAL 的 DECLARE CURSOR 语句所创建的游标的名称。 *local_cursor_name*是**nvarchar （128)**。  
  
 [ @cursor_identity=] N*global_cursor_name*  
 由具有 GLOBAL 关键字或默认设置为 GLOBAL 的 DECLARE CURSOR 语句创建的游标的名称。 *global_cursor_name*也可以是打开的 ODBC 应用程序然后名光标为通过调用 SQLSetCursorName API 服务器游标名称。*global_cursor_name*是**nvarchar （128)**。  
  
 [ @cursor_identity=] N*input_cursor_variable*  
 与打开的游标关联的游标变量的名称。 *input_cursor_variable*是**nvarchar （128)**。  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="cursors-returned"></a>返回的游标  
 sp_describe_cursor_tables 封装作为其报表[!INCLUDE[tsql](../../includes/tsql-md.md)]**光标**输出参数。 这样，[!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理、存储过程和触发器即可逐行处理输出。 这还意味着不能直接从 API 函数调用此过程。 **光标**输出参数必须绑定到程序变量中，但 Api 不支持绑定**光标**参数或变量。  
  
 下表显示 sp_describe_cursor_tables 所返回的游标的格式。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|table owner|**sysname**|表所有者的用户 ID。|  
|Table_name|**sysname**|对象或基表的名称。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，服务器游标始终返回用户指定的对象，而不是基表。|  
|Optimizer_hints|**int**|由下列一项或多项组成的位图：<br /><br /> 1 = 行级锁定 (ROWLOCK)<br /><br /> 4 = 页级锁定 (PAGELOCK)<br /><br /> 8 = 表锁 (TABLOCK)<br /><br /> 16 = 排他表锁 (TABLOCKX)<br /><br /> 32 = 更新锁 (UPDLOCK)<br /><br /> 64 = 无锁 (NOLOCK)<br /><br /> 128 = 快速第一行选项 (FASTFIRST)<br /><br /> 4096 = 与 DECLARE CURSOR 一起使用时用于读取可重复语义 (HOLDLOCK)<br /><br /> 如果提供多个选项，系统将使用限制性最高的选项。 但是，sp_describe_cursor_tables 将显示在查询中指定的标志。|  
|lock_type|**int**|为该游标的每个基表显式或隐式地请求的滚动锁类型。 该值可以是下列值之一：<br /><br /> 0 = 无<br /><br /> 1 = 共享<br /><br /> 3 = 更新|  
|server_name|**sysname，可以为 null**|驻留表的链接服务器的名称。 如果使用 OPENQUERY 或 OPENROWSET，则为 NULL。|  
|Objectid|**int**|表的对象 ID。 如果使用 OPENQUERY 或 OPENROWSET，则为 0。|  
|dbid|**int**|表所在的数据库的 ID。 如果使用 OPENQUERY 或 OPENROWSET，则为 0。|  
|dbname|**sysname**，**可以为 null**|表所在的数据库的名称。 如果使用 OPENQUERY 或 OPENROWSET，则为 NULL。|  
  
## <a name="remarks"></a>注释  
 sp_describe_cursor_tables 说明由服务器游标引用的基表。 要查看游标所返回的结果集的属性说明，请使用 sp_describe_cursor_columns。 要查看游标的全局特性（例如，其可滚动性和可更新性）的说明，请使用 sp_describe_cursor。 若要获得在连接时可见的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标的报表，请使用 sp_cursor_list。  
  
## <a name="permissions"></a>权限  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例打开一个全局游标，并使用 `sp_describe_cursor_tables` 报告该游标所引用的表。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
  
OPEN abc;  
GO  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_tables.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_tables into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_tables  
      @cursor_return = @Report OUTPUT,  
      @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_tables output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_tables.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [游标](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40;Transact SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR (Transact-SQL)](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_describe_cursor_columns &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
