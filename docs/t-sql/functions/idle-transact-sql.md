---
title: "@@IDLE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@IDLE_TSQL'
- '@@IDLE'
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], idle
- ticks [SQL Server]
- '@@IDLE function'
- status information [SQL Server], idle time
- idle time [SQL Server]
ms.assetid: 8f49c62a-8da5-4afd-a5eb-4df8ef8be755
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: ab308bcb1fd3ffdda8e901b2238111abaddecb81
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40idle-transact-sql"></a>& #x 40; & #x 40; 空闲 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自上次启动后的空闲时间。 结果以 CPU 时间增量或“时钟周期”表示，并且是所有 CPU 的累积，因此该值可能超过实际经过的时间。 乘以@TIMETICKS将转换为微秒为单位。  
  
> [!NOTE]  
>  如果时间中返回@CPU_BUSY，或 @@IO_BUSY超过大约 49 天的累积的 CPU 时间，您将收到一条算术溢出警告。 在这种情况下，值 @@CPU_BUSY，@@IO_BUSY和 @@IDLE变量不准确。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@IDLE  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>注释  
 若要显示报表包含若干个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]统计信息，运行**sp_monitor**。  
  
## <a name="examples"></a>示例  
 以下示例将返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自启动到当前时间的空闲毫秒数。 为了避免将值转换为微秒时出现算术溢出，此示例将其中一个值转换为 `float` 数据类型。  
  
```  
SELECT @@IDLE * CAST(@@TIMETICKS AS float) AS 'Idle microseconds',  
   GETDATE() AS 'as of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
I  
Idle microseconds  as of                   
----------------- ----------------------  
8199934           12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>另请参阅  
 [@@CPU_BUSY (Transact-SQL)](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [@@IO_BUSY (Transact-SQL)](../../t-sql/functions/io-busy-transact-sql.md)   
 [系统统计函数 &#40;Transact SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

