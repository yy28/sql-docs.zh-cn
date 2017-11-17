---
title: "@@CPU_BUSY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CPU_BUSY_TSQL'
- '@@CPU_BUSY'
dev_langs:
- TSQL
helpviewer_keywords:
- CPU [SQL Server]
- status information [SQL Server], CPU
- ticks [SQL Server]
- time [SQL Server], CPU activity
- '@@CPU_BUSY function'
- statistical information [SQL Server], CPU
- CPU [SQL Server], activity
ms.assetid: 81ae0e64-79fa-4a74-9aa5-37045c4cd211
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 9263eac53d78da42752704019d95e72431eabcc0
ms.contentlocale: zh-cn
ms.lasthandoff: 10/12/2017

---
# <a name="x40x40cpubusy-transact-sql"></a>& #x 40; 和 #x 40;CPU_BUSY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自上次启动后的工作时间。 其结果以 CPU 时间增量或“滴答数”表示，此值为所有 CPU 时间的累积，因此，可能会超出实际占用的时间。 乘以@TIMETICKS将转换为微秒为单位。
  
> [!NOTE]  
>  如果时间中返回@CPU_BUSY或 @@IO_BUSY超过大约 49 天的累积的 CPU 时间，您将收到一条算术溢出警告。 在这种情况下，值 @@CPU_BUSY，@@IO_BUSY和 @@IDLE变量不准确。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>返回类型
**integer**
  
## <a name="remarks"></a>注释  
若要显示报表包含若干个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]统计信息，包括 CPU 活动运行[sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)。
  
## <a name="examples"></a>示例  
以下示例显示了返回当前日期和时间之前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU 活动。 为了避免将值转换为微秒时出现算术溢出，此示例将其中一个值转换为 `float` 数据类型。
  
```sql
SELECT @@CPU_BUSY * CAST(@@TIMETICKS AS float) AS 'CPU microseconds',   
   GETDATE() AS 'As of' ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
CPU microseconds As of
---------------- -----------------------
18406250         2006-12-05 17:00:50.600
```
  
## <a name="see-also"></a>另请参阅
[sys.dm_os_sys_info &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE (Transact-SQL)](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY (Transact-SQL)](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[系统统计函数 &#40;Transact SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  

