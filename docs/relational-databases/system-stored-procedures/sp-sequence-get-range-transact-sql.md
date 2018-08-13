---
title: sp_sequence_get_range (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_sequence_get_range
- sp_sequence_get_range_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sp_sequence_get_range procedure
- sp_sequence_get_range
ms.assetid: 8ca6b0c6-8d9c-4eee-b02f-51ddffab4492
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 0ffae66700ffefe60602ba1e296bae6d903a3baa
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39549157"
---
# <a name="spsequencegetrange-transact-sql"></a>sp_sequence_get_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  从序列对象中返回一系列序列值。 序列对象生成和发出请求的值数目，并为应用程序提供与该系列序列值相关的元数据。  
  
 有关序列号的详细信息，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_sequence_get_range [ @sequence_name = ] N'<sequence>'   
     , [ @range_size = ] range_size  
     , [ @range_first_value = ] range_first_value OUTPUT   
    [, [ @range_last_value = ] range_last_value OUTPUT ]  
    [, [ @range_cycle_count = ] range_cycle_count OUTPUT ]  
    [, [ @sequence_increment = ] sequence_increment OUTPUT ]  
    [, [ @sequence_min_value = ] sequence_min_value OUTPUT ]  
    [, [ @sequence_max_value = ] sequence_max_value OUTPUT ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@sequence_name** =] **N**'*序列*  
 序列对象的名称。 架构是可选的。 *sequence_name*是**nvarchar(776)**。  
  
 [ **@range_size** =] *range_size*  
 要从序列中提取的值数目。 **@range_size** 是**bigint**。  
  
 [ **@range_first_value** = ] *range_first_value*  
 一个输出参数，它返回序列对象的第一个（最小或最大）值以用于计算请求的范围。 **@range_first_value** 是**sql_variant**具有与请求中使用的序列对象相同的基类型。  
  
 [ **@range_last_value** = ] *range_last_value*  
 一个可选的输出参数，它返回请求的范围中的最后一个值。 **@range_last_value** 是**sql_variant**具有与请求中使用的序列对象相同的基类型。  
  
 [ **@range_cycle_count** =] range_cycle_count  
 一个可选的输出参数，它返回为了返回所请求的范围而需要循环访问序列对象的次数。 **@range_cycle_count** 是**int**。  
  
 [ **@sequence_increment** = ] *sequence_increment*  
 一个可选的输出参数，它返回序列对象的增量以用于计算请求的范围。 **@sequence_increment** 是**sql_variant**具有与请求中使用的序列对象相同的基类型。  
  
 [ **@sequence_min_value** = ] *sequence_min_value*  
 一个可选的输出参数，它返回序列对象的最小值。 **@sequence_min_value** 是**sql_variant**具有与请求中使用的序列对象相同的基类型。  
  
 [ **@sequence_max_value** = ] *sequence_max_value*  
 一个可选的输出参数，它返回序列对象的最大值。 **@sequence_max_value** 是**sql_variant**具有与请求中使用的序列对象相同的基类型。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>Remarks  
 sys sp_sequence_get_rangeis。 架构，可以作为 sys.sp_sequence_get_range 引用。  
  
### <a name="cycling-sequences"></a>循环序列  
 如果需要，序列对象将循环相应的次数以处理请求的范围。 将通过 `@range_cycle_count` 参数向调用方返回循环次数。  
  
> [!NOTE]  
>  在进行循环时，序列对象从序列对象最小值（升序）或最大值（降序）重新开始，而不是从序列对象的开始值重新开始。  
  
### <a name="non-cycling-sequences"></a>非循环序列  
 如果请求的范围中的值数目大于序列对象中的剩余可用值数目，并不会从序列对象中缩减请求的范围，将返回下面的错误 11732：  
  
 `The requested range for sequence object '%.*ls' exceeds the maximum or minimum limit. Retry with a smaller range.`  
  
## <a name="permissions"></a>Permissions  
 要求对序列对象或序列对象架构具有 UPDATE 权限。  
  
## <a name="examples"></a>示例  
 以下示例使用名为 Test.RangeSeq 的序列对象。 使用以下语句来创建 Test.RangeSeq 序列。  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.RangeSeq  
    AS int   
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 25  
    CYCLE  
    CACHE 10  
;  
```  
  
### <a name="a-retrieving-a-range-of-sequence-values"></a>A. 检索序列值的范围  
 下面的语句从 Test.RangeSeq 序列对象中获取四个序列号，并向用户返回第一个编号。  
  
```  
DECLARE @range_first_value sql_variant ,   
        @range_first_value_output sql_variant ;  
  
EXEC sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 4  
, @range_first_value = @range_first_value_output OUTPUT ;  
  
SELECT @range_first_value_output AS FirstNumber ;  
  
```  
  
### <a name="b-returning-all-output-parameters"></a>B. 返回所有输出参数  
 下面的示例从 sp_sequence_get_range 过程返回所有输出值。  
  
```  
DECLARE    
  @FirstSeqNum sql_variant  
, @LastSeqNum sql_variant  
, @CycleCount int  
, @SeqIncr sql_variant  
, @SeqMinVal sql_variant  
, @SeqMaxVal sql_variant ;  
  
EXEC sys.sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 5  
, @range_first_value = @FirstSeqNum OUTPUT   
, @range_last_value = @LastSeqNum OUTPUT   
, @range_cycle_count = @CycleCount OUTPUT  
, @sequence_increment = @SeqIncr OUTPUT  
, @sequence_min_value = @SeqMinVal OUTPUT  
, @sequence_max_value = @SeqMaxVal OUTPUT ;  
  
-- The following statement returns the output values  
SELECT  
  @FirstSeqNum AS FirstVal  
, @LastSeqNum AS LastVal  
, @CycleCount AS CycleCount  
, @SeqIncr AS SeqIncrement  
, @SeqMinVal AS MinSeq  
, @SeqMaxVal AS MaxSeq ;  
  
```  
  
 将 `@range_size` 参数更改为较大的数字（例如 75）将导致循环访问序列对象。 请检查 `@range_cycle_count` 参数以确定是否循环访问序列对象以及循环次数。  
  
### <a name="c-example-using-adonet"></a>C. 使用 ADO.NET 的示例  
 下面的示例使用 ADO.NET 从 Test.RangeSeq 获取范围。  
  
```  
SqlCommand cmd = new SqlCommand();  
cmd.Connection = conn;  
cmd.CommandType = CommandType.StoredProcedure;  
cmd.CommandText = "sys.sp_sequence_get_range";  
cmd.Parameters.AddWithValue("@sequence_name", "Test.RangeSeq");  
cmd.Parameters.AddWithValue("@range_size", 10);  
  
// Specify an output parameter to retreive the first value of the generated range.  
SqlParameter firstValueInRange = new SqlParameter("@range_first_value", SqlDbType.Variant);  
firstValueInRange.Direction = ParameterDirection.Output;  
cmd.Parameters.Add(firstValueInRange);  
  
conn.Open();  
cmd.ExecuteNonQuery();  
  
// Output the first value of the generated range.  
Console.WriteLine(firstValueInRange.Value);  
  
```  
  
## <a name="see-also"></a>请参阅  
 [CREATE SEQUENCE (Transact-SQL)](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE (Transact-SQL)](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE (Transact-SQL)](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR (Transact-SQL)](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
