---
title: sp_cursor (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
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
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a6e55691bc045a8de84084498a501983bcc5a11a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spcursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  请求定位更新。 此过程对游标的提取缓冲区内的一行或多行执行操作。 sp_cursor 调用通过指定 ID = 1 表格格式数据流 (TDS) 数据包中的。  
  
||  
|-|  
|**适用于**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>参数  
 *cursor*  
 游标句柄。 *光标*是必需的参数来调用**int**输入值。 *光标*是*处理*值生成的 SQL Server 和 sp_cursoropen 过程返回的。  
  
 *optype*  
 一个必需参数，它指定游标将执行的操作。 *optype*需要以下项之一**int**输入值。  
  
|“值”|名称|Description|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|用于更新提取缓冲区中的一行或多行。  中指定的行*rownum*重新访问并更新。|  
|0x0002|DELETE|用于删除提取缓冲区中的一行或多个行。 中指定的行*rownum*重新访问和删除。|  
|0X0004|Insert|将数据插入而不生成 SQL**插入**语句。|  
|0X0008|REFRESH|用于从基础表中重新填充缓冲区，并且可用于刷新行（如果由于乐观并发控制导致更新或删除失败或在某个 UPDATE 之后）。|  
|0X10|LOCK|会导致使用 SQL Server U-锁来获取包含指定的行的页面上。 此锁与 S 锁兼容，但不与 X 锁或其他 U 锁兼容。 可用于实现短期锁定。|  
|0X20|SETPOSITION|仅当程序将要发出后续的 SQL Server 定位 DELETE 或 UPDATE 语句使用。|  
|0X40|ABSOLUTE|仅能与 UPDATE 或 DELETE 结合使用。  ABSOLUTE 仅与 KEYSET 游标结合使用（对于 DYNAMIC 游标将忽略，并且无法更新 STATIC 游标）。<br /><br /> 注意： 如果不提取键集中行上指定 ABSOLUTE，该操作可能会失败并发检查，并且返回的结果不能保证。|  
  
 *rownum*  
 指定提取缓冲区中游标将对其执行操作、更新或删除的行。  
  
> [!NOTE]  
>  这不会影响任何 RELATIVE、NEXT 或 PREVIOUS 提取操作的起点，也不影响任何使用 sp_cursor 执行的更新或删除。  
  
 *rownum*是必需的参数来调用**int**输入值。  
  
 1  
 指示提取缓冲区中的第一行。  
  
 2  
 指示提取缓冲区中的第二行。  
  
 3, 4, 5  
 指示第三行，依此类推。  
  
 n  
 指示提取缓冲区中的第 n 行。  
  
 0  
 指示提取缓冲区中的所有行。  
  
> [!NOTE]  
>  仅适用于更新、 删除、 刷新或锁*optype*值。  
  
 *table*  
 标识的表的表名， *optype*游标定义涉及到联接或返回不明确的列名称时，适用于*值*参数。 如果未指定特定的表，则默认为 FROM 子句中的第一个表。 *表*是一个可选参数需要字符串输入的值。 可以将此字符串指定为任何字符或 UNICODE 数据类型。 *表*可以是多个部分组成的表名称。  
  
 *值*  
 用于插入或更新值。 *值*字符串参数仅用于更新和插入*optype*值。 可以将此字符串指定为任何字符或 UNICODE 数据类型。  
  
> [!NOTE]  
>  参数命名为*值*可以由用户分配。  
  
## <a name="return-code-values"></a>返回代码值  
 当使用 RPC，缓冲区数字 0 的定位的 DELETE 或 UPDATE 操作将返回具有的完成消息*行计数*为 0 （失败） 或 1 （成功） 提取缓冲区中的每一行。  
  
## <a name="remarks"></a>注释  
  
## <a name="optype-parameter"></a>optype 参数  
 除了使用更新、 删除、 刷新或锁，则 SETPOSITION 的组合或使用 UPDATE 或 DELETE，绝对*optype*是互相排斥的值。  
  
 从构造的更新值的 SET 子句*值*参数。  
  
 使用插入的一个优点*optype*值是你可以避免将非字符数据转换为插入的字符格式。 指定值的方式与 UPDATE 相同。 如果不包含任何所需的列，则 INSERT 失败。  
  
-   SETPOSITION 值不影响任何 RELATIVE、NEXT 或 PREVIOUS 提取操作的起点，也不会使用 sp_cursor 接口执行任何更新或删除。 任何未在提取缓冲区中指定行的编号都将导致位置设置为 1，且不返回错误。 一旦执行 SETPOSITION，位置仍然有效，直到下一步 sp_cursorfetch 操作 T-SQL**提取**操作或通过相同的游标 sp_cursor SETPOSITION 操作。 在其他游标调用将不会影响此位置的值时，后续 sp_cursorfetch 操作将游标的位置设置为新提取缓冲区中的第一行。 SETPOSITION 可由 OR 子句链接到 REFRESH、UPDATE、DELETE 或 LOCK，以便将位置的值设置为上次修改的行。  
  
 如果提取缓冲区中的行未指定通过*rownum*参数，该位置将设置为 1，并且不返回的错误。 一旦设置了此位置，它将保持有效，直至对同一游标执行下一个 sp_cursorfetch 操作、T-SQL FETCH 操作或 sp_cursor SETPOSITION 操作。  
  
 SETPOSITION 可由 OR 子句与 REFRESH、UPDATE、DELETE 或 LOCK 进行链接，以便将游标位置设置为上一次修改的行。  
  
## <a name="rownum-parameter"></a>rownum 参数  
 如果指定， *rownum*参数可以解释为而不是提取缓冲区内的行号键集内的行号。 用户负责确保维护并发控制。 这意味着，对于 SCROLL_LOCKS 游标，您必须独立维护给定行的锁（此操作可通过一个事务完成）。 对于 OPTIMISTIC 游标，您必须事先提取行以执行此操作。  
  
## <a name="table-parameter"></a>table 参数  
 如果*optype*值是更新或插入的完整的更新或 insert 语句将作为提交*值*参数，为指定的值*表*将被忽略。  
  
> [!NOTE]  
>  与视图相关，仅可修改一个参与视图的表。 *值*参数列名称必须反映在视图中，列名称，但表名称可以是基础基表 （在此情况下 sp_cursor 将替代视图名称）。  
  
## <a name="value-parameter"></a>value 参数  
 有两种使用的规则可替代*值*如参数部分中前面所述：  
  
1.  你可以使用的名称 @ select 列表中列的任何命名名称前面附加*值*参数。 此替代方法的一个优点是可能不需要进行数据转换。  
  
2.  使用参数来提交完整的 UPDATE 或 INSERT 语句或使用多个参数来提交的 UPDATE 或 INSERT 语句的 SQL Server 将然后生成到一个完整的语句部分。 此类示例可在本主题后面的“示例”部分中找到。  
  
## <a name="examples"></a>示例  
  
### <a name="alternative-value-parameter-uses"></a>备选 value 参数用法  
 对于 UPDATE：  
  
 当使用单个参数时，可以使用以下语法提交 UPDATE 语句：  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,…n]`  
  
> [!NOTE]  
>  如果更新\<表名称 > 指定，则为指定任何值*表*参数将被忽略。  
  
 当使用多个参数时，第一个参数必须为采用以下形式的字符串：  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 并且后续参数必须为以下形式：  
  
 `<column name> = expression  [,...n]`  
  
 在这种情况下，\<表名 > 在构造更新语句是指定或默认为通过*表*参数。  
  
 对于 INSERT：  
  
 当使用单个参数时，可以使用以下语法提交 INSERT 语句：  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  如果插入*\<表名 >* 为指定任何值的指定*表*参数将被忽略。  
  
 当使用多个参数时，第一个参数必须为采用以下形式的字符串：  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 并且后续参数必须为以下形式：  
  
 `expression [,...n]`  
  
 除了指定 VALUES 之外，在此情况下，在最后一个表达式后面必须带一个尾随“)”。 在这种情况下， *\<表名 >* 在构造更新语句是指定或默认为通过*表*参数。  
  
> [!NOTE]  
>  可以提交一个参数作为命名参数，也即“`@VALUES`”。 在此情况下，不能使用其他命名参数。  
  
## <a name="see-also"></a>另请参阅  
 [sp_cursoropen &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
