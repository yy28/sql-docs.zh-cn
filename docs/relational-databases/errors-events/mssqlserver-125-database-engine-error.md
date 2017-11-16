---
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "125"
helpviewer_keywords: 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 490c1814d82718080864427ceca229494390607e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver125"></a>MSSQLSERVER_125
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|125|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|Case 表达式只能嵌套到 %d 层。|  
  
## <a name="explanation"></a>解释  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仅允许在 CASE 表达式中嵌套 10 个级别。  
  
## <a name="user-action"></a>用户操作  
将 CASE 语句的级别减少到 10 级或更低的级数。  
  
## <a name="see-also"></a>另请参阅  
[CASE (Transact-SQL)](~/t-sql/language-elements/case-transact-sql.md)  
  
