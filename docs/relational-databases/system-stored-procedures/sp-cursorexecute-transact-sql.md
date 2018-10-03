---
title: sp_cursorexecute (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fcc62c09d42adb10f8984a8f48d8b70e2f5c78de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854035"
---
# <a name="spcursorexecute-transact-sql"></a>sp_cursorexecute (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  基于 sp_cursorprepare 创建的执行计划创建并填充游标。 此过程与 sp_cursorprepare 结合，具有相同的功能与 sp_cursoropen，但它拆分为两个阶段。 sp_cursorexecute 调用通过指定 ID = 4 在表格格式数据流 (TDS) 包中的。  
  
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
 已准备的语句*处理*，由 sp_cursorprepare 返回的值。 *prepared_handle*是一个必需的参数，为调用**int**输入值。  
  
 *cursor*  
 为 SQL Server 生成的游标标识符。 *游标*是一个必需的参数，必须对所有对游标，如 sp_cursorfetch 执行操作的后续过程  
  
 *scrollopt*  
 滚动选项。 *scrollopt*是一个可选参数，需要**int**输入值。 Sp_cursorexecute*scrollopt*参数具有相同的值选项与用于 sp_cursoropen。  
  
> [!NOTE]  
>  不支持 PARAMETERIZED_STMT 值。  
  
> [!IMPORTANT]  
>  如果*scrollopt*未指定值，默认值为 KEYSET，而不考虑*scrollopt*在 sp_cursorprepare 中指定的值。  
  
 *ccopt*  
 币种控制选项。 *ccopt*是一个可选参数，需要**int**输入值。 Sp_cursorexecute*ccopt*参数具有相同的值选项与用于 sp_cursoropen。  
  
> [!IMPORTANT]  
>  如果*ccopt*未指定值，默认值为 OPTIMISTIC，而不考虑*ccopt*在 sp_cursorprepare 中指定的值。  
  
 *行计数*  
 一个可选参数，指示要用于 AUTO_FETCH 的提取缓冲区行数。 默认值为 20 行。 *行计数*以不同的方式指定为输入值与返回值时的行为。  
  
|作为输入值|作为返回值|  
|--------------------|---------------------|  
|当使用 FAST_FORWARD 游标指定 AUTO_FETCH 时*rowcount*表示要放入提取缓冲区的行数。|表示结果集中的行数。 当*scrollopt*指定 AUTO_FETCH 值，则*rowcount*返回提取到提取缓冲区的行数。|  
  
 *bound_param*  
 指示可选使用其他参数。  
  
> [!NOTE]  
>  第五个参数之后的任何参数都将作为输入参数传递到语句计划。  
  
## <a name="code-return-value"></a>代码返回值  
 *行计数*可能会返回以下值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|-1|未知的行数。|  
|-n|异步填充生效。|  
  
## <a name="remarks"></a>备注  
  
## <a name="scrollopt-and-ccopt-parameters"></a>scrollopt 和 ccopt 参数  
 *scrollopt*并*ccopt*缓存的计划优先于服务器缓存，这意味着，必须重新编译标识语句准备的句柄时非常有用。 *Scrollopt*并*ccopt*参数值必须匹配给 sp_cursorprepare 的原始请求中发送的值。  
  
> [!NOTE]  
>  PARAMETERIZED_STMT 不应分配给*scrollopt*。  
  
 如果无法提供匹配值，则将导致重新编译计划，而取消 prepare 和 execute 操作。  
  
## <a name="rpc-and-tds-considerations"></a>RPC 和 TDS 注意事项  
 RPC RETURN_METADATA 输入标志可设置为 1，以请求在 TDS 流中返回游标选择列表元数据。  
  
## <a name="see-also"></a>请参阅  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
