---
title: sp_describe_cursor_columns (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_columns
- sp_describe_cursor_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_columns
ms.assetid: 6eaa54af-7ba4-4fce-bf6c-6ac67cc1ac94
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d1a39ab87291a51f272966bb60e407d89b4f2cb2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260270"
---
# <a name="spdescribecursorcolumns-transact-sql"></a>sp_describe_cursor_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告服务器游标结果集中的列属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_describe_cursor_columns   
   [ @cursor_return = ] output_cursor_variable OUTPUT   
    { [ , [ @cursor_source = ] N'local' ,   
          [ @cursor_identity = ] N'local_cursor_name' ]   
    | [ , [ @cursor_source = ] N'global' ,   
          [ @cursor_identity = ] N'global_cursor_name' ]   
    | [ , [ @cursor_source = ] N'variable' ,   
          [ @cursor_identity = ] N'input_cursor_variable' ]   
   }  
```  
  
## <a name="arguments"></a>参数  
 [ @cursor_return=] *output_cursor_variable*输出  
 声明的用于接收游标输出的游标变量的名称。 *output_cursor_variable*是**光标**，没有默认值，且必须与不能与任何游标相关联的 sp_describe_cursor_columns 称为次。 返回的游标是可滚动的动态只读游标。  
  
 [ @cursor_source=] {N'local' |N'global' |N'variable'}  
 指定使用以下哪一名称来指定所报告的游标：本地游标、全局游标或游标变量的名称。 该参数是**nvarchar (30)**。  
  
 [ @cursor_identity=] N*local_cursor_name*  
 由具有 LOCAL 关键字或默认设置为 LOCAL 的 DECLARE CURSOR 语句创建的游标名称。 *local_cursor_name*是**nvarchar （128)**。  
  
 [ @cursor_identity=] N*global_cursor_name*  
 由具有 GLOBAL 关键字或默认设置为 GLOBAL 的 DECLARE CURSOR 语句创建的游标名称。 *global_cursor_name*是**nvarchar （128)**。  
  
 *global_cursor_name*也可以是 API 服务器游标，然后通过调用 SQLSetCursorName 名为并且打开 ODBC 应用程序的名称。  
  
 [ @cursor_identity=] N*input_cursor_variable*  
 与打开的游标关联的游标变量的名称。 *input_cursor_variable*是**nvarchar （128)**。  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="cursors-returned"></a>返回的游标  
 sp_describe_cursor_columns 封装作为其报表[!INCLUDE[tsql](../../includes/tsql-md.md)]**光标**输出参数。 这样，[!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理、存储过程和触发器即可逐行处理输出。 这也意味着无法直接从数据库 API 函数调用该过程。 **光标**输出参数必须绑定到程序变量中，但数据库 Api 不支持绑定**光标**参数或变量。  
  
 下表显示了通过使用 sp_describe_cursor_columns 返回的游标的格式。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|column_name|**sysname** (可以为 null)|为结果集列分配的名称。 如果指定列时不带 AS 子句，则该列为 NULL。|  
|ordinal_position|**int**|从结果集最左边一列算起的相对位置。 首列的位置为 0。|  
|column_characteristics_flags|**int**|一个位掩码，它指示存储在 OLE DB 的 DBCOLUMNFLAGS 中的信息。 可以是下列选项之一或组合：<br /><br /> 1 = 书签<br /><br /> 2 = 固定长度<br /><br /> 4 = 可为空值<br /><br /> 8 = 行版本控制<br /><br /> 16 = 可更新列（为没有 FOR UPDATE 子句的游标的提取列设置，如果存在这样的列，则每个游标只能有一列）。<br /><br /> 当位值被合并时，将应用合并位值的特征。 例如，如果位值为 6，则列为一个固定长度 (2) 的可空 (4) 列。|  
|column_size|**int**|此列中的值最大的可能大小。|  
|data_type_sql|**int**|表示列的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型的数字。|  
|column_precision|**tinyint**|为每个列的最大精度*bPrecision* OLE DB 中的值。|  
|column_scale|**tinyint**|小数点右侧的数字个数**数值**或**十进制**数据类型为每个*bScale* OLE DB 中的值。|  
|order_position|**int**|如果此列参与结果集排序，则表示它在排序键中相对于最左边的列的位置。|  
|order_direction|**varchar(1)**(可以为 null)|A = 该列位于排序键中，按升序排列。<br /><br /> D = 该列位于排序键中，按降序排列。<br /><br /> NULL = 该列没有参与排序。|  
|hidden_column|**int**|0 = 此列出现在选择列表中。<br /><br /> 1 = 保留以供将来使用。|  
|columnid|**int**|基列的列 ID。 如果结果集列由表达式生成，则 columnid 为 -1。|  
|objectid|**int**|提供列的对象或基表的对象 ID。 如果结果集列由表达式生成，则 objectid 为 -1。|  
|dbid|**int**|包含提供列的基表的数据库 ID。 如果结果集列由表达式生成，则 dbid 为 -1。|  
|dbname|**sysname**<br /><br /> （可为 null）|包含提供列的基表的数据库名称。 如果结果集列由表达式生成，则 dbname 为 NULL。|  
  
## <a name="remarks"></a>注释  
 sp_describe_cursor_columns 描述服务器游标结果集中的列属性，例如每个游标的名称和数据类型。 使用 sp_describe_cursor 描述服务器游标的全局特性。 使用 sp_describe_cursor_tables 报告游标引用的基表。 若要获取连接中可见的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标的报表，请使用 sp_cursor_list。  
  
## <a name="permissions"></a>权限  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例将打开一个全局游标，并使用 `sp_describe_cursor_columns` 报告该游标中使用的列。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person;  
GO  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_columns.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_columns into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_columns  
    @cursor_return = @Report OUTPUT  
    ,@cursor_source = N'global'   
    ,@cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_columns output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_columns.  
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
 [sp_describe_cursor &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_tables &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
