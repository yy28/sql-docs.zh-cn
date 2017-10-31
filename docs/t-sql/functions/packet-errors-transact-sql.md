---
title: "@@PACKET_ERRORS (Transact SQL) |Microsoft 文档"
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
- '@@PACKET_ERRORS'
- '@@PACKET_ERRORS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACKET_ERRORS function'
- number of packet errors
- packets [SQL Server], errors
- networking [SQL Server], packet errors
- connections [SQL Server], packets
ms.assetid: f7da1b80-5cbe-42fa-be71-40c6af16383a
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 57a215132b55d655752db867e0c3dadcced9e92e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40packeterrors-transact-sql"></a>& #x 40; 和 #x 40;PACKET_ERRORS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回自上次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 后在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接上发生的网络数据包错误数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@PACKET_ERRORS  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>注释  
 若要显示报表包含若干个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行统计信息，包括数据包错误**sp_monitor**。  
  
## <a name="examples"></a>示例  
 下面的示例显示了使用 `@@PACKET_ERRORS`。  
  
```  
SELECT @@PACKET_ERRORS AS 'Packet Errors';  
```  
  
 下面是一个结果集示例。  
  
```  
Packet Errors  
-------------  
0  
```  
  
## <a name="see-also"></a>另请参阅  
 [@@PACK_RECEIVED (Transact-SQL)](../../t-sql/functions/pack-received-transact-sql.md)   
 [@@PACK_SENT (Transact-SQL)](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系统统计函数 &#40;Transact SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

