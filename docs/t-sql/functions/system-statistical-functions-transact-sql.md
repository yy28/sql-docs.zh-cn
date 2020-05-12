---
title: 系统统计函数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- statistical functions [SQL Server]
- system statistical functions [SQL Server]
- functions [SQL Server], statistical
ms.assetid: 45828c67-1b9a-4653-bb24-86246084d8ba
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: bc142e8df0c4e55b1cbd78ca0fa8b7dcb2923d34
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832149"
---
# <a name="system-statistical-functions-transact-sql"></a>系统统计函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下列标量函数返回系统的统计信息：  
  
|||  
|-|-|  
|[@@CONNECTIONS](../../t-sql/functions/connections-transact-sql.md)|[@@PACK_RECEIVED](../../t-sql/functions/pack-received-transact-sql.md)|  
|[@@CPU_BUSY](../../t-sql/functions/cpu-busy-transact-sql.md)|[@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)|  
|[fn_virtualfilestats](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)|[@@TIMETICKS](../../t-sql/functions/timeticks-transact-sql.md)|  
|[@@IDLE](../../t-sql/functions/idle-transact-sql.md)|[@@TOTAL_ERRORS](../../t-sql/functions/total-errors-transact-sql.md)|  
|[@@IO_BUSY](../../t-sql/functions/io-busy-transact-sql.md)|[@@TOTAL_READ](../../t-sql/functions/total-read-transact-sql.md)|  
|[@@PACKET_ERRORS](../../t-sql/functions/packet-errors-transact-sql.md)|[@@TOTAL_WRITE](../../t-sql/functions/total-write-transact-sql.md)|  
  
 所有的系统统计函数都具有不确定性。 这意味着即使同一组输入值，也不一定在每次调用这些函数时都返回相同的结果。 有关函数确定性的详细信息，请参阅[确定性函数和不确定性函数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)  
  
  
