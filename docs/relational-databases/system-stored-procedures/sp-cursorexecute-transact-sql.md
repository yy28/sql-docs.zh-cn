---
title: sp_cursorexecute (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cae17034cdcc2d048e539961bf07971acb3b3410
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spcursorexecute-transact-sql"></a>sp_cursorexecute (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  基于 sp_cursorprepare 创建的执行计划创建并填充游标。 此过程中，结合了 sp_cursorprepare，具有与 sp_cursoropen，相同的功能，但拆分为两个阶段。 通过指定 ID 调用 sp_cursorexecute = 表格格式数据流 (TDS) 数据包中的 4。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>参数  
 *prepared_handle*  
 是已准备的语句*处理*sp_cursorprepare 返回值。 *prepared_handle*是必需的参数来调用**int**输入值。  
  
 *cursor*  
 为 SQL Server 生成的游标标识符。 *光标*是必须作用于光标，如 sp_cursorfetch 的所有后续过程提供所需的参数  
  
 *scrollopt*  
 滚动选项。 *scrollopt*是需要一个可选参数**int**输入值。 Sp_cursorexecute*scrollopt*参数具有与那些为 sp_cursoropen 相同的值选项。  
  
> [!NOTE]  
>  不支持 PARAMETERIZED_STMT 值。  
  
> [!IMPORTANT]  
>  如果*scrollopt*未指定值，则默认值为键集而不考虑*scrollopt* sp_cursorprepare 中指定的值。  
  
 *ccopt*  
 币种控制选项。 *ccopt*是需要一个可选参数**int**输入值。 Sp_cursorexecute*ccopt*参数具有与那些为 sp_cursoropen 相同的值选项。  
  
> [!IMPORTANT]  
>  如果*ccopt*未指定值，默认值为而不考虑 OPTIMISTIC *ccopt* sp_cursorprepare 中指定的值。  
  
 *行计数*  
 一个可选参数，指示要用于 AUTO_FETCH 的提取缓冲区行数。 默认值为 20 行。 *行计数*时指定为返回值与输入值的行为有所不同。  
  
|作为输入值|作为返回值|  
|--------------------|---------------------|  
|当与 FAST_FORWARD 游标指定 AUTO_FETCH*行计数*表示要将放置在提取缓冲区的行数。|表示结果集中的行数。 当*scrollopt*指定 AUTO_FETCH 值，*行计数*返回到提取缓冲区提取的行数。|  
  
 *bound_param*  
 指示可选使用其他参数。  
  
> [!NOTE]  
>  第五个参数之后的任何参数都将作为输入参数传递到语句计划。  
  
## <a name="code-return-value"></a>代码返回值  
 *行计数*可能会返回以下值。  
  
|“值”|Description|  
|-----------|-----------------|  
|-1|未知的行数。|  
|-n|异步填充生效。|  
  
## <a name="remarks"></a>注释  
  
## <a name="scrollopt-and-ccopt-parameters"></a>scrollopt 和 ccopt 参数  
 *scrollopt*和*ccopt*当缓存的计划用于服务器缓存，这意味着，必须重新编译准备的句柄标识语句被占用时非常有用。 *Scrollopt*和*ccopt*参数值必须匹配到 sp_cursorprepare 的原始请求中发送的值。  
  
> [!NOTE]  
>  PARAMETERIZED_STMT 不应分配给*scrollopt*。  
  
 如果无法提供匹配值，则将导致重新编译计划，而取消 prepare 和 execute 操作。  
  
## <a name="rpc-and-tds-considerations"></a>RPC 和 TDS 注意事项  
 RPC RETURN_METADATA 输入标志可设置为 1，以请求在 TDS 流中返回游标选择列表元数据。  
  
## <a name="see-also"></a>另请参阅  
 [sp_cursoropen &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
