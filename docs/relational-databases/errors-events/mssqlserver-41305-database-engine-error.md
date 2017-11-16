---
title: MSSQLSERVER_41305 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 41305 (Database Engine error)
ms.assetid: a96e5083-ff97-4003-a900-07942454151d
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: a2e3fb8c1a110b81868d4803169cbcc40e7d3239
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver41305"></a>MSSQLSERVER_41305
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41305|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_TX_COMMIT_RR_VALIDATION|  
|消息正文|因某个可重复读取验证失败，当前事务无法提交。|  
  
## <a name="explanation"></a>解释  
事务遇到验证错误，已失败。  
  
有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="user-action"></a>用户操作  
重试失败的事务。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
