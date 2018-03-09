---
title: "sp_cursorfetch (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9b33361094966dc180939f0cdf92ac951922139
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spcursorfetch-transact-sql"></a>sp_cursorfetch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从数据库中提取由一行或多行组成的缓冲区。 在此缓冲区中的行组被称为游标的*提取缓冲区*。 通过指定 ID 调用 sp_cursorfetch = 7 表格格式数据流 (TDS) 数据包中的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>参数  
 *cursor*  
 是*处理*生成值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，且返回 sp_cursoropen。 *光标*是必需的参数来调用**int**输入值。 有关详细信息，请参阅本主题后面的备注一节。  
  
 *fetchtype*  
 指定要提取的游标缓冲区。 *fetchtype*是需要一个以下整数输入值的可选参数。  
  
|值|Name|Description|  
|-----------|----------|-----------------|  
|0x0001|FIRST|提取的第一个缓冲区*nrows*行。 如果*nrows*等于 0 游标位于结果集之前，会返回任何行。|  
|0x0002|NEXT|提取的下一个缓冲区*nrows*行。|  
|0x0004|PREV|提取的上一个缓冲区*nrows*行。<br /><br /> 注意： 对于 FORWARD_ONLY 游标使用上一步返回一条错误消息，因为 FORWARD_ONLY 仅支持一个方向滚动。|  
|0x0008|LAST|提取的最后一个缓冲区*nrows*行。 如果*nrows*等于 0，则游标位于结果集，并会返回任何行之后。<br /><br /> 注意： 对于 FORWARD_ONLY 游标使用上一次返回一条错误消息，因为 FORWARD_ONLY 仅支持一个方向滚动。|  
|0x10|ABSOLUTE|提取的缓冲区*nrows*开头的行*rownum*行。<br /><br /> 注意： 使用绝对动态游标或 FORWARD_ONLY 光标返回一条错误消息，因为 FORWARD_ONLY 仅支持一个方向滚动。|  
|0x20|RELATIVE|提取的缓冲区*nrows*开头为指定的行的行*rownum*当前块中的第一行中的行的值。 在这种情况下*rownum*可以是负数。<br /><br /> 注意： 对于 FORWARD_ONLY 游标使用相对返回一条错误消息，因为 FORWARD_ONLY 仅支持一个方向滚动。|  
|0x80|REFRESH|重新填充基础表中的缓冲区。|  
|0x100|INFO|检索有关游标的信息。 通过使用返回此信息*rownum*和*nrows*参数。 因此，指定信息时， *rownum*和*nrows*成为输出参数。|  
|0x200|PREV_NOADJUST|用法类似于 PREV。 但是，如果过早遇到结果集顶部，结果可能有所不同。|  
|0x400|SKIP_UPDT_CNCY|必须用于的另一个*fetchtype*值，但信息除外。|  
  
> [!NOTE]  
>  不支持值 0x40。  
  
 有关详细信息，请参阅本主题后面的备注一节。  
  
 *rownum*  
 是一个可选参数，用于指定绝对超链接和信息的行位置*fetchtype*通过使用为输入和 / 或输出中，仅整数值的值。 *rownum*用作的行偏移量*fetchtype*位值相对。 *rownum*对于所有其他值，将忽略。 有关详细信息，请参阅本主题后面的备注一节。  
  
 *nrows*  
 一个可选参数，用于指定要提取的行数。 如果*nrows*未指定，则默认值为 20 行。 若要设置而无需返回数据的位置，请指定值为 0。 当*nrows*应用于*fetchtype*信息查询，它查询中返回的行总数。  
  
> [!NOTE]  
>  *nrows*刷新忽略*fetchtype*位值。  
>   
>  有关详细信息，请参阅本主题后面的备注一节。  
  
## <a name="return-code-values"></a>返回代码值  
 当指定位值 INFO 时，以下各表显示可能返回的值。  
  
> [!NOTE]  
>  ： 如果会不返回任何行，缓冲区内容保持不变。  
  
|*\<rownum >*|设置为|  
|------------------|------------|  
|如果未打开|0|  
|如果定位在结果集前面|0|  
|如果定位在结果集后面|-1|  
|对于 KEYSET 游标和 STATIC 游标|结果集中当前位置的绝对行号|  
|对于 DYNAMIC 游标|1|  
|对于 ABSOLUTE|-1 返回集中的最后一行。<br /><br /> -2 返回集中的倒数第二行，依此类推。<br /><br /> 注意： 如果在这种情况下提取请求多个行，将返回结果集的最后两行。|  
  
|*\<nrows >*|设置为|  
|-----------------|------------|  
|如果未打开|0|  
|对于 KEYSET 游标和 STATIC 游标|通常为当前键集大小。<br /><br /> **– m**如果光标位于中使用的异步创建*m*找到到目前为止的行。|  
|对于 DYNAMIC 游标|-1|  
  
## <a name="remarks"></a>注释  
  
## <a name="cursor-parameter"></a>cursor 参数  
 在执行任何提取操作之前，游标的默认位置位于结果集第一行的前面。  
  
## <a name="fetchtype-parameter"></a>fetchtype 参数  
 除 SKIP_UPD_CNCY， *fetchtype*是互相排斥的值。  
  
 如果指定 SKIP_UPDT_CNCY，则在提取或刷新行时，时间戳列的值不会写入到键集表中。 如果正在更新键集行，则时间戳列的值保持为先前的值。 如果正在插入键集行，则时间戳列的值不确定。  
  
 对于 KEYSET 游标，这意味着在执行最后一个非跳过 FETCH 的过程中（如果已执行一个），键集表设置了值。 否则，将在填充过程中设置值。  
  
 对于 DYNAMIC 游标，这意味着如果使用刷新来执行跳过，则它生成与 KEYSET 相同的结果。 对于任何其他提取类型，键集表会被截断。 这意味着正在插入行，且时间戳列的值不确定。 因此，当您针对 DYNAMIC 游标运行 sp_cursorfetch 时，对于除 REFRESH 之外的任何操作应避免使用 SKIP_UPDT_CNCY。  
  
 如果由于所请求的游标位置超出结果集而导致提取操作失败，则应将游标位置设置为恰好在最后一行的后面。 如果由于所请求的游标位置位于结果集的前面而导致提取操作失败，则应将游标位置设置在第一行的前面。  
  
## <a name="rownum-parameter"></a>rownum 参数  
 当你使用*rownum*，从指定的行填充缓冲区。  
  
 *Fetchtype*绝对指的位置的值*rownum*在整个结果内设置。 具有 ABSOLUTE 的负数指定该操作从结果集的末尾开始对行进行计数。  
  
 *Fetchtype*相对指的位置的值*rownum*相对于当前缓冲区开头光标的位置。 具有 RELATIVE 的负数指定该游标从当前游标位置向后计数。  
  
## <a name="nrows-parameter"></a>nrows 参数  
 *Fetchtype*值刷新和信息忽略此参数。  
  
 当指定*fetchtype*第一个具有的值*nrow*值为 0，将光标定位在提取缓冲区中具有任何行的结果集的前面。  
  
 当指定*fetchtype*具有的最后一个值*nrow*值为 0，光标位于当前提取缓冲区中具有任何行的结果集的后面。  
  
 有关*fetchtype*值的下一步、 上一步、 绝对、 相对和 PREV_NOADJUST， *nrow*为 0 的值无效。  
  
## <a name="rpc-considerations"></a>RPC 注意事项  
 RPC 返回状态指示键集大小参数是否为最终的（也即，键集表或临时表是否异步填充）。  
  
 RPC 状态参数设置为下表中显示的值之一。  
  
|值|说明|  
|-----------|-----------------|  
|0|过程已成功执行。|  
|0x0001|过程失败。|  
|0x0002|当处于负方向中的提取在逻辑上应位于结果集前面时，该提取可能导致将游标位置设置在结果集的开头。|  
|0x10|快进游标自动关闭。|  
  
 这些行将作为典型的结果集返回，也即：列格式 (0x2a)、行 (0xd1)，后跟完成 (0xfd)。 元数据标记使用与为 sp_cursoropen 指定的相同格式发送，也即：对于 SQL Server 7.0 用户为 0x81、0xa5 和 0xa4 等。 行状态指示器在具有列名称 rowstat 和数据类型 INT4 的每一行的末尾作为隐藏列发送（类似于 BROWSE 模式）。 此 rowstat 列具有下表中显示的值之一。  
  
|值|Description|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 因为 TDS 协议不提供发送尾随状态列而不发送先前列的方法，所以为缺少的行发送虚数据（根据需要，将可以为 Null 的字段设置为 Null，将固定长度的字段设置为 0、空白或该列的默认值）。  
  
 DONE 行计数将始终为零。 DONE 消息包含实际结果集行计数，在任何 TDS 消息之间可能出现错误消息或信息性消息。  
  
 若要请求在 TDS 流中返回有关游标选择列表的元数据，请将 RPC RETURN_METADATA 输入标志设置为 1。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>A. 使用 PREV 更改游标位置  
 假定游标 h2 将生成具有以下内容的结果集，且当前位置如下所示：  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 接下来，sp_cursorfetch PREV 具有*nrows*值为 5 将以逻辑方式放置光标两行结果集的第一行之前。 在此类情况下，游标将调整为从第一行开始，并返回请求的行数。 这通常意味着它将返回位于 PRIOR 提取缓冲区中的行。  
  
> [!NOTE]  
>  这是 RPC 状态参数设置为 2 时的确切情况。  
  
### <a name="b-using-prevnoadjust-to-return-fewer-rows-than-prev"></a>B. 使用 PREV_NOADJUST 返回少于 PREV 的行  
 PREV_NOADJUST 从不包括任何位于它返回的行块中当前游标位置或在其之后的行。 在上一步后当前的位置返回行的位置的情况下，PREV_NOADJUST 返回更少的行不是请求中*nrows*。 给定的当前定位在示例中更早版本，应用上一步时，sp_cursorfetch (h2，4，1，5) 提取以下行：  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 但是，PREV_NOADJUST 将应用，sp_cursorfetch (h2，512、 6、 5) 提取只有的以下行：  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_cursoropen &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
