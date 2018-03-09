---
title: "ALTER 序列 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/08/2015
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
- ALTER_SEQUENCE_TSQL
- ALTER SEQUENCE
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, altering
- ALTER SEQUENCE statement
ms.assetid: decc0760-029e-4baf-96c9-4a64073df1c2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 66960ed0ae27cb7ecbe2d39d0e30d1ec12dcc3cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="alter-sequence-transact-sql"></a>ALTER SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  修改现有序列对象的参数。 如果使用序列创建了**缓存**选项，因此更改序列将重新创建缓存。  
  
 通过使用创建序列对象[创建序列](../../t-sql/statements/create-sequence-transact-sql.md)语句。 序列是整数值，可以是返回整数的任何数据类型。 使用 ALTER SEQUENCE 语句无法更改数据类型。 若要更改数据类型，请删除或创建序列对象。  
  
 序列对象是用户定义的绑定到架构的对象，用于可根据规范生成数值序列。 通过调用 NEXT VALUE FOR 函数，从序列中生成新值。 使用 **sp_sequence_get_range** 同时获取多个序列号。 有关信息和使用这两个创建序列中，方案**sp_sequence_get_range**，和 NEXT VALUE FOR 函数，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER SEQUENCE [schema_name. ] sequence_name  
    [ RESTART [ WITH <constant> ] ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE <constant> } | { NO MINVALUE } ]  
    [ { MAXVALUE <constant> } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *sequence_name*  
 指定数据库中标识序列的唯一名称。 类型是**sysname**。  
  
 重新启动 [WITH\<常量 >]  
 将由序列对象返回的下一个值。 如果提供，则 RESTART WITH 值必须是小于或等于序列对象的最大值并大于或等于其最小值的整数。 如果忽略 WITH 值，则序列编号将根据原始 CREATE SEQUENCE 选项重新开始。  
  
 递增通过\<常量 >  
 用于在每次调用 NEXT VALUE FOR 函数时递增（如果为负数，则为递减）序列对象的基值的值。 如果增量是负值，则序列对象为降序，否则为升序。 增量不能为 0。  
  
 [MINVALUE\<常量 > |没有 MINVALUE]  
 指定序列对象的边界。 如果指定 NO MINVALUE，则使用序列数据类型的最小可能值。  
  
 [MAXVALUE\<常量 > |没有 MAXVALUE  
 指定序列对象的边界。 如果指定 NO MAXVALUE，则使用序列数据类型的最大可能值。  
  
 [ CYCLE | NO CYCLE ]  
 此属性指定当超过序列对象的最小值或最大值时，序列对象是应从最小值（对于降序对象，则为最大值）重新开始，还是应引发异常。  
  
> [!NOTE]  
>  在循环后，下一个值为最小值或最大值，而不是序列的 START VALUE（起始值）。  
  
 [缓存 [\<常量 >] |无缓存]  
 通过最大限度地减少将生成的值持久保存到系统表中所需的 IO 数，可以提高使用序列对象的应用程序的性能。  
  
 缓存的行为的详细信息，请参阅[创建序列 &#40;Transact SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
## <a name="remarks"></a>注释  
 有关如何创建序列以及如何管理序列缓存的信息，请参阅[创建序列 &#40;Transact SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 不能将表示升序的 MINVALUE 和表示降序的 MAXVALUE 更改为不允许序列的 START WITH 值的值。 如果要将升序的 MINVALUE 更改为一个大于 START WITH 值的数字，或者将降序的 MAXVALUE 更改为小于 START WITH 值的数字，请加入 RESTART WITH 参数，以便在最小值和最大值范围内的所需点重新开始序列。  
  
## <a name="metadata"></a>元数据  
 有关序列的信息，请查询 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要**ALTER**在序列上的权限或**ALTER**拥有架构的权限。 若要授予**ALTER**序列中，使用权限**ALTER ON 对象**采用以下格式：  
  
```  
GRANT ALTER ON OBJECT::Test.TinySeq TO [AdventureWorks\Larry]  
```  
  
 可以使用传输序列对象的所有权**ALTER AUTHORIZATION**语句。  
  
### <a name="audit"></a>审核  
 审核**ALTER SEQUENCE**，监视器**SCHEMA_OBJECT_CHANGE_GROUP**。  
  
## <a name="examples"></a>示例  
 有关创建序列和使用的示例**NEXT VALUE FOR**函数来生成序列号，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
### <a name="a-altering-a-sequence"></a>A. 更改序列  
 下面的示例创建名为 Test 的架构和 TestSeq 使用命名序列**int**具有介于 0 到 255 之间的数据类型。 序列以 125 开始，每次生成数字时递增 25。 因为该序列配置为可循环，所以，当值超过最大值 200 时，序列将从最小值 100 重新开始。  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.TestSeq  
    AS int   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
GO  
```  
  
 下面的示例将更改 TestSeq 序列能够从 0 到 255 的范围。 序列以 100 重新开始编号系列，每次生成数字时递增 50。  
  
```  
ALTER SEQUENCE Test. TestSeq  
    RESTART WITH 100  
    INCREMENT BY 50  
    MINVALUE 50  
    MAXVALUE 200  
    NO CYCLE  
    NO CACHE  
;  
GO  
```  
  
 序列不将循环，因为**NEXT VALUE FOR**序列超过 200 时，函数将导致错误。  
  
### <a name="b-restarting-a-sequence"></a>B. 重新开始序列  
 下面的示例创建一个名为 CountBy1 的序列。 该序列使用默认值。  
  
```  
CREATE SEQUENCE Test.CountBy1 ;  
```  
  
 若要生成序列值，所有者随后应执行下列语句：  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1  
```  
  
 -9223372036854775808 的返回的值是最低的可能值为**bigint**数据类型。 所有者意识到他想要从 1 开始的序列，但未指明**开始**子句时他创建序列。 若要更正此错误，所有者应执行下面的语句。  
  
```  
ALTER SEQUENCE Test.CountBy1 RESTART WITH 1 ;  
```  
  
 然后，所有者再次执行下列语句以生成序列号。  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1;  
```  
  
 数字现在是 1，与预期相符。  
  
 使用默认值为 NO 周期，因此它将停止生成数量 9223372036854775807 后操作创建 CountBy1 序列。 对序列对象的后续调用将返回错误 11728。 下面的语句将序列对象更改为循环，并将缓存设置为 20。  
  
```  
ALTER SEQUENCE Test.CountBy1  
    CYCLE  
    CACHE 20 ;  
  
```  
  
 现在，当序列对象达到 9,223,372,036,854,775,807 时，它将循环，循环后的下一个编号将为此数据类型的最小值，即 -9,223,372,036,854,775,808。  
  
 所有者实现**bigint**数据类型在使用它每次都使用 8 个字节。 **Int**使用 4 个字节的数据类型就足够了。 但是，不能更改序列对象的数据类型。 若要将更改为**int**数据类型，所有者必须删除该序列对象，并使用正确的数据类型重新创建对象。  
  
## <a name="see-also"></a>另请参阅  
 [创建序列 &#40;Transact SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [拖放序列 &#40;Transact SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [下一个值 &#40;Transact SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [sp_sequence_get_range &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
