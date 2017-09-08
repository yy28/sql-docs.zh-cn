---
title: "@@IO_BUSY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@IO_BUSY'
- '@@IO_BUSY_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- I/O [SQL Server], time spent performing operations
- '@@IO_BUSY function'
- output operations [SQL Server]
- input operations [SQL Server]
- time [SQL Server], I/O operations
ms.assetid: 3c26770c-41ae-4e34-8c82-7bef920ffbca
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ef13f65af269167eba7c8df53c35ecfd992df6e0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="iobusy-transact-sql"></a>@@IO_BUSY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回自从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最近一次启动以来，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已经用于执行输入和输出操作的时间。 其结果是 CPU 时间增量（时钟周期），并且是所有 CPU 的累积值，所以，它可能超过实际消逝的时间。 乘以@TIMETICKS将转换为微秒为单位。  
  
> [!NOTE]  
>  如果时间中返回@CPU_BUSY，或 @@IO_BUSY超过大约 49 天的累积的 CPU 时间，您将收到一条算术溢出警告。 在这种情况下，值 @@CPU_BUSY，@@IO_BUSY和 @@IDLE变量不准确。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@IO_BUSY  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>注释  
 若要显示包含几种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 统计信息的报告，请运行 sp_monitor。  
  
## <a name="examples"></a>示例  
 下面的示例返回在开始时间和当前时间之间 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已经用于执行输入/输出操作的毫秒数。 若要将值转换为微秒时避免算术溢出，该示例将转换到的值之一**float**数据类型。  
  
```  
SELECT @@IO_BUSY*@@TIMETICKS AS 'IO microseconds',   
   GETDATE() AS 'as of';  
```  
  
 下面是典型的结果集：  
  
```  
  
IO microseconds as of                   
--------------- ----------------------  
4552312500      12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_os_sys_info &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY (Transact-SQL)](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系统统计函数 &#40;Transact SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
