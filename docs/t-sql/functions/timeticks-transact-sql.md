---
title: "@@TIMETICKS (Transact SQL) |Microsoft 文档"
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
- '@@TIMETICKS_TSQL'
- '@@TIMETICKS'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- '@@TIMETICKS function'
- microseconds per tick [SQL Server]
- time [SQL Server], ticks
- number of microseconds per tick
ms.assetid: 9d036633-837f-4309-9c45-3d9600258018
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 51139d84f42be25fe41c42907ddc6640b95899e3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40timeticks-transact-sql"></a>& #x 40; 和 #x 40;TIMETICKS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回每个时钟周期的微秒数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@TIMETICKS  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>注释  
 每个时钟周期的时间量依赖于计算机。 操作系统的一个时钟周期是 31.25 毫秒，或是三十分之一秒。  
  
## <a name="examples"></a>示例  
  
```  
SELECT @@TIMETICKS AS 'Time Ticks';  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统统计函数 &#40;Transact SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

